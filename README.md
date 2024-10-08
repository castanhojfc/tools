# Local Setup

# (Optional) WSL

1. Open terminal with administrator rights
2. Install: `wsl --install`
3. Download and install Linux kernel update package: <https://aka.ms/wsl2kernel>
4. List distributions available to download: `wsl --list --online`
5. Install distribution: `wsl --install -d <Distribution Name>`
6. Configure an account
7. (Optional) make it the default distribution (Check help instructions from the wsl command)

# Font

Nerd Fonts: <https://www.nerdfonts.com>

FiraCode: <https://github.com/tonsky/FiraCode>

1. Download FiraCode Nerd Font: <https://github.com/ryanoasis/nerd-fonts/releases/download/v3.1.1/FiraMono.zip>
2. Install (WSL: Select all files, right click and install all, Ubuntu: copy all files to `~/.local/share/fonts` and run `sudo fc-cache -f -v` or reboot)

# Terminal

Wez's Terminal: <https://wezfurlong.org/wezterm/>

1. Download and install: <https://wezfurlong.org/wezterm/installation>
2. Create configuration file. (WSL: create file `wezterm.lua` inside the installation directory, Ubuntu: create `$HOME/.config/wezterm/wezterm.lua`)

Configuration
```lua
local wezterm = require 'wezterm'
local act = wezterm.action
local config = {}

config = wezterm.config_builder()

-- Optional, only needed for WSL
config.default_prog = { 'wsl' }

config.font = wezterm.font 'FiraCode Nerd Font Mono'

config.color_scheme = 'Solarized (dark) (terminal.sexy)'

config.enable_tab_bar = false

config.window_close_confirmation = 'NeverPrompt'

return config
```

# Shell

Z Shell: <https://www.zsh.org/>

Oh My Zsh: <https://ohmyz.sh/>

Z Plug: <https://github.com/zplug/zplug>

Starship: <https://starship.rs>

zsh-autosuggestions: <https://github.com/zsh-users/zsh-autosuggestions>

zsh-syntax-highlighting: <https://github.com/zsh-users/zsh-syntax-highlighting>

zsh-autocomplete: <https://github.com/marlonrichert/zsh-autocomplete>

1. Install everything:
```bash
sudo apt-get install zsh
chsh -s /bin/zsh
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
curl -sL --proto-redir -all,https https://raw.githubusercontent.com/zplug/installer/master/installer.zsh | zsh
curl -sS https://starship.rs/install.sh | sh
```

2. Add the following to the end of `~/.zshrc` replacing the user configuration section:
```bash
# User configuration

ENABLE_CORRECTION="true"

export VISUAL=nvim
export EDITOR="$VISUAL"
export PATH="/usr/local/opt/gettext/bin:$PATH"

# Keep 1000 lines of history within the shell and save it to ~/.zsh_history:
HISTSIZE=1000
SAVEHIST=1000
HISTFILE=~/.zsh_history

# Aliases
alias ll='ls -lh'
alias la='ls -lAh'
alias l='ls -lah'
alias md='mkdir -p'
alias rd='rmdir'
alias cd..='cd ..'
alias cd...='cd ../..'
alias cd....='cd ../../..'
alias cd.....='cd ../../../..'
alias cd......='cd ../../../../..'
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias .....='cd ../../../..'
alias ......='cd ../../../../..'
alias vi=nvim
alias vim=nvim
alias zj=zellij

# Zplug

# Check if installed
if [[ ! -d ~/.zplug ]]; then
  git clone https://github.com/zplug/zplug ~/.zplug
  source ~/.zplug/init.zsh && zplug update --self
fi

source ~/.zplug/init.zsh
zplug "zplug/zplug"

# Plugins
zplug "zsh-users/zsh-autosuggestions"
zplug "zsh-users/zsh-syntax-highlighting", defer:2
zplug "marlonrichert/zsh-autocomplete"

# Install packages that have not been installed yet
if ! zplug check --verbose; then
    printf "Install? [y/N]: "
    if read -q; then
        echo; zplug install
    else
        echo
    fi
fi

zplug load

# End of Zplug configuration

eval "$(starship init zsh)"
cd $HOME # Only needed for WSL

# zsh-autocomplete configuration
bindkey '\t' menu-select "$terminfo[kcbt]" menu-select
bindkey -M menuselect '\t' menu-complete "$terminfo[kcbt]" reverse-menu-complete
```
3. Restart terminal

4. Activate Oh My Zsh plugins
```bash
plugins=(git docker docker-compose vi-mode asdf)
```

5. Change Starship theme
```bash
mkdir .config
touch ~/.config/starship.toml
starship preset gruvbox-rainbow -o ~/.config/starship.toml
```

Oh My Zsh Plugins: <https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins>

# File versioning

Git: <https://git-scm.com/>

1. Configure
```bash
git config --global user.name <name>
git config --global user.email <email>
git config --global core.editor nvim
ssh-keygen -t ed25519 -C <email>
ssh-agent
ssh-add /home/<username/.ssh/<private_key>
cat ~/.ssh/<public_key>
```

2. Add ssh key on GitHub

# Containerization

Docker: <https://www.docker.com>

Download and install: <https://www.docker.com/products/docker-desktop>

On WSL make sure that the integration is activated in the distro

# Package Manager

Brew: https://brew.sh/

Install: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

Install dependencies: `sudo apt-get install build-essential`

Add brew to PATH: `(echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /home/castanhojfc/.zshrc`

Reload Shell: `eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"`

# Version Manager

asdf: <https://asdf-vm.com/>

Install: `git clone https://github.com/asdf-vm/asdf.git ~/.asdf`

Plugins: <https://github.com/asdf-vm/asdf-plugins>

# Environment Variables Manager

direnv: <https://direnv.net/>

Install: `brew install direnv`

# Editor

Neovim: <https://neovim.io/>

1. Install: `brew install neovim`

2. Install clipboard provider:
```bash
sudo apt update
sudo apt install xclip
```

# Terminal Multiplexer

Zellij: <https://zellij.dev/>

Install: `brew upgrade zellij`

Create configuration and dump it to a file:
```bash
mkdir ~/.config/zellij
zellij setup --dump-config > ~/.config/zellij/config.kdl
```

Configure (Copy paste values)
```bash
theme "solarized-dark"

layout_dir "/home/<username>/Workspace/Layouts"
```

Layouts: <https://zellij.dev/documentation/layouts>
Examples: <https://zellij.dev/documentation/layout-examples>

Layout Example (default.kdl):

```
layout {
	tab name="my amazing tab" cwd="~" hide_floating_panes=true {
		pane cwd="/tmp"
		pane cwd="Workspace"
		pane command="tail" {
			args "-f" "Workspace/Layouts/default.kdl"
		}
		floating_panes {
			pane
			pane command="ls"
			pane {
				x 1
				y "10%"
				width 200
				height "50%"
			}
		}
		pane size=1 borderless=true {
			plugin location="zellij:compact-bar"
		}
	}
	tab {
		pane split_direction="vertical" {
			pane edit="~/.zshrc" size="70%" focus=true
			pane split_direction="horizontal" name="My Awesome Pane"{
				htop { args "" ""; }
				htop { args "" ""; }
				htop { args "" ""; }
			}
		}
		pane size=1 borderless=true {
			plugin location="zellij:compact-bar"
		}
	}
	pane_template name="htop" {
		command "htop"
		start_suspended true
	}
}
keybinds {
	shared {
		bind "Alt 1" { Run "git" "status"; }
		bind "a" {
			Run "tail" "-f" "foo" {
				cwd "/tmp"
				direction "Down"
			}
		}
	}
}
```

Zellij will open the default layout always
Create more project layouts and use then with: `zellij -l <layout>`

Links:

<https://github.com/alebcay/awesome-shell>
