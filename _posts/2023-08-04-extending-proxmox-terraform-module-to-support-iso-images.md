---
layout: post
title: Extending Proxmox terraform module to support iso images
date: 2023-08-04 22:38 +0200
---
Today I was trying to setup my kubernetes cluster from scratch.This time I decided to write down all of the steps as a terraform plan rather than regular bash scripts.

To start I looked up for the terraform provider on github and came across this [Telmate/terraform-provider-proxmox](https://github.com/Telmate/terraform-provider-proxmox)
Looking at the documentation I didnt come across a way to upload an iso to proxmox, so I decided to work on this feature for the provider.

This was the first time I wrote an extension for proxmox, so I had to deep a lot deeper into the code and [documentation](https://developer.hashicorp.com/terraform/plugin/sdkv2).

First thing I had to do was define how the user api was going to be.
I decided on the following

```
resource "proxmox_storage_iso" "unique_resource_name" {
  storage  = "local"                        // Where should this be stored in proxmox
  filename = "image.iso"                    // Name of the image
  pve_node = "pve"                          // Target node where the storage points too
  url      = "http://example.com/image.iso" // URL to the image iso
}
```

Next was time to build the Resource to TF State integration.
```
func resourceStorageIso() *schema.Resource {
	return &schema.Resource{
		Create: resourceStorageIsoCreate,
		Read:   resourceStorageIsoRead,
		Delete: resourceStorageIsoDelete,
        Schema: map[string]*schema.Schema{
                "filename": {
                        Type:     schema.TypeString,
                        Required: true,
                }
        }
    }
}
```

The Proxmox plugin has callbacks for the different actions that a resource might have to work with.
These callbacks are pretty straight forward as their meaning maps to their verb.
The schema on the other hand are the different fields that can be provided to the resource.

Terraform resources also have a special ResourceData field called Id which is used to uniquely identity a resource.

In the create callback, we call the proxmox-go-api library to create an ISO resource.One of the things I had to do was fetch the iso and store it in a temporary file and then upload it using the api.
Once the iso is created in proxmox, we call the api again to validate if the image has been saved correctly.I then set the `Id` field to the `volId` field from the api response which is the unique identifier 
from proxmox.

The delete callback was a bit tricky since the proxmox-go-api didnt have a delete api, so I called it using the generic client delete method present in the library.
Since proxmox doesnt let you update a given iso, I didn't have to implement the update callback.

Here is the [link](https://github.com/Telmate/terraform-provider-proxmox/compare/master...h0lyalg0rithm:terraform-provider-proxmox:add_resource_storage_iso) to the final PR for this feature
