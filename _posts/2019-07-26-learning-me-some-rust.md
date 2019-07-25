---
layout: post
title: Learning me some Rust
date: 2019-07-26 01:46 +0200
---

Installing Rust on the mac is pretty straightforward

```
curl https://sh.rustup.rs -sSf | zsh
```

You would have to install the commandline tools that come with the mac

```
xcode-select --install
```

To learn some Rust I thought going through some exercism exercises would be good.

```
brew update && brew install exercism
```

Some vim setup to help with running the tests

```
Plugin 'rust-lang/rust.vim'

map <C-r> :RustTest!<CR>
let g:rustfmt_autosave = 1
```

With Rust format I didnt have to worry about the code style and format.

Now all I had to do is press `Ctrl + r` in the test file.
