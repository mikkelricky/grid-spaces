# Grid spaces

Grid spaces a la [TotalSpaces2](https://totalspaces.binaryage.com/), but for
[macOS Monterey](https://www.apple.com/macos/monterey/), built on
[yabai](https://github.com/koekeishiya/yabai) and
[skhd](https://github.com/koekeishiya/skhd). You also need
[jq](https://stedolan.github.io/jq/) to make the magic work - and `jq` is a
magic tool in itself!

## Installation

Install `jq`:

```sh
brew install jq
```

Check the [installation
requirements](https://github.com/koekeishiya/yabai/wiki#installation-requirements)
for `yabai` and install it:

```sh
brew install yabai --HEAD
yabai --start-service
```

Create the desired number of spaces [using
yabai](https://github.com/koekeishiya/yabai/wiki/Commands#create-and-destroy-spaces)
or [Mission Control](https://support.apple.com/en-us/HT204100).

Make sure that `yabai` works and can focus spaces by running a command like

```sh
yabai --message space --focus next
```

Create the file `~/.gridspacesrc` and define the number of columns in your grid:

```dotenv
GRID_COLUMNS=3
```

Install [skhd](https://github.com/koekeishiya/skhd#install):

```sh
brew install koekeishiya/formulae/skhd
brew services start skhd
```

Create or edit [the configuration file for
skhd](https://github.com/koekeishiya/skhd#configuration) and define keyboard
shortcuts for moving around in the grid, e.g.

```sh
cmd + ctrl - up            : «path to this directory»/navigate up
cmd + ctrl - down          : «path to this directory»/navigate down
cmd + ctrl - left          : «path to this directory»/navigate left
cmd + ctrl - right         : «path to this directory»/navigate right

cmd + ctrl + shift - up    : «path to this directory»/navigate --move-window up
cmd + ctrl + shift - down  : «path to this directory»/navigate --move-window down
cmd + ctrl + shift - left  : «path to this directory»/navigate --move-window left
cmd + ctrl + shift - right : «path to this directory»/navigate --move-window right
```

That's it! Now you should be able to use your grid.

## System preferences

`yabai` and Grid spaces only work as expected when some Spaces system
preferences are set correctly:

![System Preferences: Set up spaces](images/set-up-spaces.png)

* “Automatically rearrange Spaces based on most recent use” **must not** be checked
* “Displays have separate Spaces” **must** be checked
* “When switching to an application, switch to a Space with open windows for the
  application” **may be** checked and might come in handy if you’ve lost a
  window for an application that you’re onyl use on special occasions.

```shell
# Uncheck “Automatically rearrange Spaces based on most recent use”
defaults write com.apple.dock mru-spaces -boolean false

# You may want to check “When switching to an application, switch to a Space with open windows for the application”.
defaults write 'Apple Global Domain' AppleSpacesSwitchOnActivate -boolean true

# Reload the system preferences
killall 'System preferences'
```

Furthermore, all Mission Control space switching keyboard shortcuts should be
disabled as all Space navigation should be handled by `skhd` calling the
`navigate` script:

![System Preferences: Mission Control space switching keyboard shortcuts](images/keyboard-shortcuts.png)

Finally, you may want to [Reduce
motion](https://support.apple.com/en-hk/guide/mac-help/mchlc03f57a1/mac) to get
rid of some animations:

![System Preferences: Reduce motion](images/reduce-motion.png)

## Updating

```sh
brew reinstall yabai
yabai --restart-service
```

## Coding standards

[Install ShellCheck](https://github.com/koalaman/shellcheck#installing):

```sh
brew install shellcheck
```

Check to code:

```sh
shellcheck navigate
```
