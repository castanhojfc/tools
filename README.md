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
```
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

(Re-check everything below)
## Tools

## Terminal

Z Shell: <https://www.zsh.org/>

Oh My Zsh: <https://ohmyz.sh/>

Z Plug: <https://github.com/zplug/zplug>

```bash
sudo apt-get install zsh
chsh -s /bin/zsh
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
curl -sL --proto-redir -all,https https://raw.githubusercontent.com/zplug/installer/master/installer.zsh | zsh
```

`.zshrc` configurations:

```bash
ENABLE_CORRECTION="true"

export VISUAL=vim
export EDITOR="$VISUAL"
export PATH="/usr/local/opt/gettext/bin:$PATH"

# Keep 1000 lines of history within the shell and save it to ~/.zsh_history:
HISTSIZE=1000
SAVEHIST=1000
HISTFILE=~/.zsh_history

# Aliases
# Some more basic aliases
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

##############################
# Zplug
##############################

# Check if zplug is installed
if [[ ! -d ~/.zplug ]]; then
  git clone https://github.com/zplug/zplug ~/.zplug
  source ~/.zplug/init.zsh && zplug update --self
fi

# Essential
source ~/.zplug/init.zsh

# Zplug plugins
zplug "zplug/zplug"

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

eval "$(starship init zsh)"
```

Plugins:
zsh-autosuggestions: <https://github.com/zsh-users/zsh-autosuggestions>

zsh-syntax-highlighting: <https://github.com/zsh-users/zsh-syntax-highlighting>

Oh my zsh also comes with extra plugins, these are recommendations:

```bash
plugins=(git asdf docker docker-compose vi-mode zsh-autosuggestions zsh-syntax-highlighting)
```

## Shell prompt

Starship: <https://starship.rs/>

## Fonts

Nerd Fonts: <https://www.nerdfonts.com/>
