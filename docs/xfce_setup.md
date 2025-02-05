# XFCE Setup.

## Add the user to sudo.

Switch to root.
```
su root
```

Add your user to the sudo group.
```
sudo usermod -aG sudo $USERNAME
```

Now exit, logout and log back in for the group changes to take effect.

## Set default editor to vi.

```
echo 'export EDITOR=vi' >> ~/.bashrc && source ~/.bashrc
```

## Install the essentials.

```
sudo apt update

sudo apt install vim tmux gpg curl pass taskwarrior htop lm-sensors
network-manager lynx
```

### Install FZF, ripgrep, vim and tmux plugin managers.

```
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install

sudo apt install ripgrep

curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

git clone --depth 1 https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim

git clone --depth 1 https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### Fetch the config files.

```
wget https://raw.githubusercontent.com/recursivethinker/config-files/main/vim/.vimrc -O ~/.vimrc

wget https://raw.githubusercontent.com/recursivethinker/config-files/main/tmux/.tmux.conf -O ~/.tmux.conf
```

## Cosmetic upgrades to the XFCE desktop.

### Install Dracula theme.
```
mkdir -p ~/.themes

git clone --depth 1 https://github.com/dracula/gtk ~/.themes/Dracula/
```

Once that is done, simply open the 'Appearanace settings' and the 'Window
Manager' settings and select 'Dracula' in both. You should be good to go.

### Fonts.

Install Fira Code - 
```
sudo apt install fonts-firacode
```

Set your default monospace font to 'Fira Code Regular' or 'Fira Code Retina'.

Play around with the other fonts a little bit too until you are satisfied.

Then, theme XFCE Terminal. First create a colorschemes directory to place themes
in, then get the Dracula theme and copy it there:

```
mkdir ~/.local/share/xfce4/terminal/colorschemes -p

wget https://raw.githubusercontent.com/dracula/xfce4-terminal/refs/heads/master/Dracula.theme -O ~/.local/share/xfce4/terminal/colorschemes/Dracula.theme
```

We should be mostly done at this point. All that is left to do is maybe, swap
out the wallpaper for something more tasteful that you like and you should be
good to go! Also remember to customize the panels to your taste.

Just remember to execute the commands to install the Vim and Tmux plugins after
you start them up the first time.

