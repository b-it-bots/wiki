# Atom
## Installation
### Option 1: Following their [official instructions](https://flight-manual.atom.io/getting-started/sections/installing-atom/).

1. Download their latest **stable** release [here](https://github.com/atom/atom/releases/latest).
2. Run the following:  

```shell
# Install atom
sudo dpkg -i atom-amd64.deb

# Install Atom's dependencies if they are missing
sudo apt-get -f install
```
### Option 2: Adding the unofficial ppa
Run the following commands:
```shell
sudo add-apt-repository ppa:webupd8team/atom
sudo apt-get update
sudo apt-get install atom
```

## Configuration
You can easily open your settings by pressing `ctrl`+`,`. (Also found in Edit>Preferences).

### Minimal setup
After you have installed atom, there are a few additional packages that you should install. You can do this by runnig the script `atom-minimum.sh` found in the [dotfiles](https://mas.b-it-center.de/gitgate/b-it-bots/dotfiles) repository in your terminal. This will install the following packages:
* language-ini
* language-cmake
* atom-ros
* linter-pycodestyle
* linter
* linter-ui-default
* linter-clang
* intentions
* busy-signal

Other recommended packages include (there is an `atom-recommended.sh` script to install them):
* minimap
* highlight-selected
* minimap-highlight-selected
* minimap-git-diff
* minimap-find-and-replace
* minimap-selection

### Updating your config file
Copy the contents of the `config.cson` file in this repository to your atom config.
Assuming you cloned the [dotfiles](https://mas.b-it-center.de/gitgate/b-it-bots/dotfiles) repository on your home folder:

```shell
cp -f ~/dotfiles/atom/config.cson ~/.atom/config.cson
```
# Contributors
* Argentina Ortega - **Original author**
