# Pop!_OS Setup 

<!-- For a more detailed explanation of the steps below, please see my [blog post](https://www.joshuamlee.com/posts/pop-os-setup/). --> 

__Notes__  
Current Version for this setup: `Pop!_OS 24.04 LTS` 

For reference, I use this current setup on Lenovo ThinkPad - T14 (AMD). 

Certain commands are catered to the hardware of my laptop. Please modify the commands to your needs.  
e.g. Installing Brave: `arch=amd64` 

Many things here are personal preference  

_If you are new to Linux, I recommend reading through the commands and understanding what each command does before using them_ 

--- 
__Updates__ 
_Latest Update: 2025-12-10_ 
- Using default Cosmic Terminal (version 24.04) -> Previously using Alacritty 
- Updated Git configuration  
- Added Firefox Developer Edition 
- Updated Brave Browser install 
- Updated Node Version Manager (NVM) install 
- Updated Nerd Fonts + NeoVim + LazyVim install and configuration 
- Updated GoLang, Python, and other language installs 

--- 

__General Settings__ 

- Tile windows 
- Enable night light 
- Change device name 
- Turn off file history 
- Enable automatic trash & temporary file cleanup 
- Disable sleep & display timeout 
- Show seconds in system clock 
- Show week numbers in calendar 
- Laptop 
  - Touchpad 
    - Enable natural scrolling 
    - Disable tap to click 
    - Disable while typing 
  - Show battery percentage 
  - Disable suspend when lid is closed 
    - `cd /etc/systemd/` 
    - `sudo vi logind.conf` 
    - Uncomment and set `HandleLidSwitch=ignore` 

--- 

__Install & Configure Software__ 

- Update system 
  - `sudo apt update && sudo apt upgrade -y` 
  - `sudo apt autoremove -y` 
  - `sudo apt autoclean` 
  - `sudo reboot now` 

- [ZSH](https://zsh.org) & [Oh-My-Zsh](https://github.com/ohmyzsh/ohmyzsh) 
  - `sudo apt install zsh` 
  - `chsh -s $(which zsh)` 
  - `sudo apt reboot now` 
  - Open new terminal 
    - `0` 
  - `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` 
  - Restart terminal 
  - `git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions` 
  - `sudo nano ~/.zshrc` 
    - `plugins=(git zsh-autosuggestions)` 
    - Save 
  - `source ~/.zshrc` 

- [Git](https://git-scm.com/) 
  - `git config --global user.name "Your Name"` 
  - `git config --global user.email "your@email.com"` 
  - `git config --global init.defaultBranch master` 
  - `ssh-keygen -t ed25519 -C "your@email.com"` 
  - `eval "$(ssh-agent -s)"` 
  - `ssh-add ~/.ssh/id_ed25519` 
  - `cat ~/.ssh/id_ed25519.pub` 
    - Copy key and paste into GitHub SSH Key settings 
  - `ssh -T git@github.com` 
    - `yes` 

- [Firefox - Developer Edition](https://www.firefox.com/en-US/channel/desktop/developer/) 
  - `sudo install -d -m 0755 /etc/apt/keyrings` 
  - `wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | sudo tee /etc/apt/keyrings/packages.mozilla.org.asc > /dev/null` 
  - `echo "deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main" | sudo tee -a /etc/apt/sources.list.d/mozilla.list > /dev/null` 
  - `echo '` 
  - `Package: *` 
  - `Pin: origin packages.mozilla.org` 
  - `Pin-Priority: 1000` 
  - `' | sudo tee /etc/apt/preferences.d/mozilla` 
  - `sudo apt update && sudo apt install firefox-devedition` 

- [Brave Browser](https://brave.com/) 
  - `sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg` 
  - `sudo curl -fsSLo /etc/apt/sources.list.d/brave-browser-release.sources https://brave-browser-apt-release.s3.brave.com/brave-browser.sources` 
  - `sudo apt update && sudo apt install brave-browser` 
  - `sudo apt install brave-browser` 

- [NVM](https://github.com/nvm-sh/nvm) & [NodeJS](https://nodejs.org/en) & [NPM](https://www.npmjs.com/) 
  - `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash` 
  - Restart terminal 
  - `nvm install v24.12.0` 
  - `nvm use 24.12.0` 
  - Check install 
    - `node --version` 
    - `npm --version` 

- [Nerd Fonts](https://www.nerdfonts.com/) _(I use JetBrainsMono Nerd Font)_
  - Download `.zip` from website
  - `cd ~/Downloads`
  - `unzip JetBrainsMono.zip -d 3270`
  - `cd 3270`
  - `sudo mv -vf *.ttf /usr/local/share/fonts/`
  - `cd ..`
  - `rm -rf *`
  - `nano ~/.config/alacritty/alacritty.yml`
    - `font:`
      - `normal:`
        - `family: JetBrainsMono Nerd Font`
        - `style: Regular`
      - `bold:`
        - `family: JetBrainsMono Nerd Font`
        - `style: Bold`

- [Python](https://www.python.org/) 
  - `sudo apt install python3-pip` 
  - `sudo apt install python3-venv` 

- [Neovim](https://github.com/neovim/neovim)
  - `sudo apt install ninja-build gettext cmake unzip`
  - `git clone https://github.com/neovim/neovim`
  - `cd neovim`
  - `git checkout v0.9.5`
  - `make CMAKE_BUILD_TYPE=RelWithDebInfo`
  - `cd build`
  - `cpack -G DEB`
  - `sudo dpkg -i nvim-0.9.5-Linux.deb`

- [Lazyvim](https://www.lazyvim.org/)
  - `git clone https://github.com/LazyVim/starter ~/.config/nvim`
  - `rm -rf ~/.config/nvim/.git`
  - `nvim`


- [Neofetch](https://github.com/dylanaraps/neofetch)
  - `sudo apt install neofetch`


- [GIMP](https://www.gimp.org/)
  - `sudo apt install gimp`


- [OBS Studio](https://obsproject.com/)
  - `sudo apt install ffmpeg obs-studio`


- [Obsidian.md](https://obsidian.md/)
  - [Download .deb file](https://obsidian.md/download)
  - Install with Eddy


---

__Finishing Touches__

- `sudo apt update && sudo apt upgrade -y`
- `sudo apt autoremove -y`
- `sudo apt autoclean`
- `sudo reboot now`

