---
layout: post
title: Autoupdate bricked my phone
date: 2024-02-02 17:22 +0100
---
Starting from this year I decided not to spend time building and running my own infrastructure.
Until the end of Jan 2023 I would always build the rom from scratch rather than depending on the maintainer to release a new build of the rom.

Today morning I allowed my phone to be updated to the latest build of ArrowOS, what I didnt know was that it was an automatic monthly build.This ended up bricking my phone.

![My phone is dead](/wp-contents/uploads/2024/02/phone_dead.gif)

My first action was trying to revert it back to an older build.Checking the ArrowOS download website for previous builds, resulted in nothing.Looks like older build links were removed from the website. I checked my machine for an older build and I found one however do the mismatch in the security patch level prevented recovery from sideloading the older build.

Looking on the telegram group, I didnt see much activity from the maintainer. I decided to pull up my sleeves and built the rom from scratch.
This time I setup a machine on [clouding.io](https://clouding.io), they are a local(Spain) cloud hosting service which is fairly priced.The best part about them is that they have fast NVMe disks, must have for building roms and their snapshot pricing is much lower than others even 5-10x cheaper than the big guys like Google, DigitalOcean etc.

I ended up building the rom, I removed the offending commit which resulted in the issue.Seems like those commits did not have any side-effects as I am running the rom now without any issues.

One of the reasons to write this post was to document my steps so I dont need to spend as much time.
```
# Install bare essentials
sudo apt-get update
sudo apt install -y git jq

git config --global user.email "surajshirvankar@gmail.com"
git config --global user.name "Suraj Shirvankar"


# Install scripts has all of the AOSP depedencies
cd ~/
git clone https://github.com/akhilnarang/scripts
cd scripts
./setup/android_build_env.sh

# Create bin file to download repo
mkdir -p ~/bin
# fetch repo from google
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```
Need to add repo to the search path
```
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```
Time to fetch all the code
```
mkdir arrow
cd arrow
# Depth reduces disk and network requirements by fetching only the latest commit
repo init --depth=1 -u https://github.com/ArrowOS/android_manifest.git -b arrow-13.1
# Download all of the git repos. Takes some time
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
source build/envsetup.sh

# Fetch relevant device repos.Python script might fail
lunch arrow_apollo-userdebug
```
Since the script failed for me I had to manually comment out the offending lines from 202 to 207
```
         if exists_in_tree(mlm, repo_target) != None:
             existing_m_project = exists_in_tree(mlm, repo_target)
         elif exists_in_tree(arrowm, repo_target) != None:
             existing_m_project = exists_in_tree(arrowm, repo_target)
         elif exists_in_tree(halm, repo_target) != None:
             existing_m_project = exists_in_tree(halm, repo_target)
```

Since the repo configuration was built for the maintainer he had decided to use repo which were private and only visible to him.Device specific repos are stored in the `.repo/local_manifests/roomservice.xml`.We can change them in this file to point to my repos.

```
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project path="device/xiaomi/apollo" remote="ArrowOS-Devices" name="android_device_xiaomi_apollo" revision="arrow-13.1" />
  <project path="device/xiaomi/sm8250-common" remote="github" name="ArrowOS-Devices/android_device_xiaomi_sm8250-common" revision="arrow-13.1-apollo" />
  <project path="vendor/xiaomi" remote="github" name="ArrowOS-Devices/android_vendor_xiaomi_apollo" revision="arrow-13.1" />
  <project path="kernel/xiaomi/sm8250" remote="github" name="PixelExperience-Devices/kernel_xiaomi_sm8250" revision="thirteen" />
  <project path="hardware/xiaomi" remote="github" name="Dobsgw/android_hardware_xiaomi" revision="arrow-13.1" />
  <project path="packages/apps/GCamGOPreBuilt" remote="github" name="ArrowOS-Devices/android_packages_apps_GCamGOPrebuilt" revision="arrow-13.1" />
  <project path="vendor/xiaomi-firmware/apollo" remote="gitlab" name="h0lyalg0rithm/vendor_xiaomi-firmware_apollo" revision="arrow-13.1" />
</manifest>

```
The configuration about the build is present in `vendor/arrow/config/version.mk`.Here is where you can setup the build config like including google apps, updater etc
```
# Time to build the rom
repo sync -c -j48 --force-sync --no-clone-bundle --no-tags
export ARROW_GAPPS=true
export ARROW_OFFICIAL=true
# You should see the build file name(ARROW_VERSION) contain OFFICIAL and GAPPS
lunch arrow_apollo-userdebug
mka bacon -j60 # This machine is pretty beafy
```
