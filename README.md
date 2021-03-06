# Vimage --> Automated Fully Featured Neovim Image

## What this is

A premade environment/container for developing java, golang (and many more languages!) using neovim based on debian slim image, with everything installed and ready to go including language server, neovim, some configs, plugins and more.. A nice stable starting point for writing code using vim.

This image also serves as *a template for setting up other neovim based development images*, for example, seeing as we have a configured neovim, with CoC completion plugin, we can also install rust for example quite easily and then the cargo pkg mgr etc.

## Only 3 Minutes to set up a fully featured neovim development environment
Minus the Docker build time, it takes roughly 3 minutes to get neovim fully working. This process is **fully automated** besides relaunching `nvim` once or twice.
- *1* at first launch of `nvim` :PlugInstall will run automatically, let the plugins download and install *this takes roughly 1 minute* 
- *2* Once plugins installed, relaunch `nvim` -- CoC LSP will now automatically install all the language plugins *this takes roughly 1 minute*
- *3* The first time you edit a java file, java language server will be downloaded automatically, *this takes roughly 30 seconds*

## Why un/optimised versions?

Simply put, we can make python 20% faster with optimisations, but the build time is extended by almost double with this turned on. So I made 2 versions, one with a faster python (optimised version), one with a faster build time (unomptimised version)

## Get the Dockerfile

- clone this repo to where you want it, or wget/curl just the dockerfile only, as it will be all you need to build the docker image
- `cd` to directory contaning Dockerfile from this repo

## Build/Run the Container

### Build it
`docker build -t "nameToGiveYourContainer:Dockerfile" .`

### Find the ID of your new image
`docker images`

### Run it, launch a shell prompt
`docker run -it --entrypoint /bin/zsh <IDofyournewcontainer>`

## Setting Up Neovim [Vim]

- open vim `nvim`
- note: you may see an error such as "gruvbox not installed", this will trigger :PlugInstall to install plugins.
- it will now clone all of the packages needed for the plugins located in my vimrc ~/.config/nvim/init.vim
- relaunch vim, plugins should now load. Coc {our Language Server for completion etc} will now pop open a window an install all of the language extensions automatically i.e java, python completions etc
- finally, run `TSInstall java` (or any other supported language) in command mode to install language parsers for treesitter. By default vim does syntax using regex but you can have a much better experience with TS **note Treesitter currently requires bleeding edge nightly 0.5 nvim release which is not currently in debian/nightly as of Dec 2020**
- once you are done installing your desired treesitter parsers, your development environment is now completely set up with everything ready to go!
- check out beauwilliams/dotfiles repo to see my nvim configuration for more info

## Testing nvim with java language completion and some extra goodies

- try `nvim test.java`
- you will see on the bottom bar, that the java language server is downloading as jlt.ds is not found (first launch only)
- it will download it for you automatically (its the language server from eclipse so lots of similar errors etc)
- once the language server is downloaded were are now ready to roll.

### Goodies

File Browser, command pallette, startup window, better shell, fully featured neovim editor, treesitter based syntax highlighting

- SPACE bar is the leader key
- In normal mode hit `<leader>n` for a file browser
- In normal mode hit `<leader>p` for a file search built on fuzzy finder powered by the very fast ripgrep, `<leader>f` for word search, b for buffers, C for commands, P for history
- `<leader>t` for terminal in neovim,
- `<leader>h j k or l` to create new window in that direction respectively, `<leader>w` to cycle windows. Windows autoresize depending on one in focus
- VSCode like completion and language features, snippets. Tab and enter to move through suggestions
- Git features, gutter, and more UX enhancements...
- Launch neovim with `nvim` it will load a launch screen with recent files etc
- type `zsh` to launch a better shell with history and tab completions

# See full neovim mappings and configuration here
![init.vim](https://github.com/beauwilliams/Dotfiles/blob/master/Vim/nvim/init.vim)

# Please note that while my neovim configuration supports many languages for editing, the debian install is currently only setup with JDK and Golang. For other languages you must install yourself.

# Preview Images

![gif1](https://i.ibb.co/j8SRZjD/dotfiles.gif)
![Preview](https://i.ibb.co/7xmh5JV/Screen-Shot-2020-06-24-at-11-00-39-pm.png)
![Preview](https://i.ibb.co/9Nxh3hW/Screen-Shot-2020-06-24-at-11-00-48-pm.png)

