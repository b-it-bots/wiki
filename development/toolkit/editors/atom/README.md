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
After that select `Editor` on the menu to your left.

## Minimal setup
After you have installed atom, there are a few additional packages that you should install. You can do this by using the command `apm install <package name>`, going to *Install* in the settings section or by runnig the script `atom-minimum.sh` found in this wiki.
* minimap
* highlight-selected
* language-ini
* language-cmake
* atom-ros (shameless plug, @argenos developed this package, but feel free to contribute!)

Other recommended packages include (there is an `atom-recommended.sh` script to install them):
* minimap-highlight-selected
* minimap-git-diff
* minimap-find-and-replace
* minimap-selection

### Indentation
To configure your indentation accoridng to [PEP 8](https://www.python.org/dev/peps/pep-0008/#indentation).

###
