## THIS IS JUST A PERSONAL PRE-SETUP FOR A FRESH FEDORA WORKSTATION (GNOME) INSTALL

### 1. update system : 
```sudo dnf upgrade --refresh -y```

NOTE : software in linux/fedora are in apps ie sandboxed (flatpaks, appimages) or packages (rpm, compressed binaries) -> softwares included/fetched from software repositories like fedora linux (s/m packages), fedora flatpaks, flathub (more flatpaks), RPM fusion FREE & NON-FREE and fedora 3rd party repositories (proprietery software) -> fetched software can be installed & updated via package managers like dnf/yum for fedora (s/m packages), flatpak, gnome software store   + there are firmware ie software for managing the core hardware (which are installed along with linux kernal and updated right in gnome store)

``` sudo dnf upgrade -y && flatpak update -y && fwupdmgr get-updates && fwupdmgr update (separtely update system packages, flatpak apps, firmware) or just use gnome software to update all in one place ```


### 2. Enable RPM Fusion (Proprietery extra software repo):
```
https://rpmfusion.org/Howto

sudo dnf install \
    https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
    https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

add flathub (additional to fedora's flatpak repo):
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
sudo dnf upgrade --refresh -y

app image launcher (https://github.com/TheAssassin/AppImageLauncher/releases)(https://github.com/TheAssassin/AppImageLauncher/releases/download/v2.2.0/appimagelauncher-2.2.0-travis995.0f91801.x86_64.rpm) (or use gear lever for better compatability since the above is old, https://flathub.org/en/apps/it.mijorus.gearlever)

install nvidia prop gpu drivers if needed : sudo dnf install akmod-nvidia (intel/amd included)
```

### 3. Windows compatability layer (setup wine) : 
```https://gitlab.winehq.org/wine/wine/-/wikis/Fedora, install winetricks from software for GUI windows prefix manager [wine alternatives - bottles, winboat, lurks for gaming]```


### 4. install major softwares : 
```
brave (customize, sync bookmarks and pass), vlc, vscode (sync account, add code . command alias to bashrc alias code='flatpak run com.visualstudio.code'), terminator, qbitorrent, arduino IDE, gparted, balena etcher, vbox/gnome boxes, timeshift, build-essentials, fastfetch

sudo dnf5 install gcc gcc-c++ make cmake pkgconf-pkg-config glibc-devel libstdc++-devel kernel-headers gdb git (sudo dnf5 install gcc gcc-c++ glibc-devel libstdc++-devel kernel-headers)
sudo dnf5 install python3 python3-pip

or sudo dnf install @development-tools (This is group install ie install a set of packages including git, compilers etc)
```
### 5. setup git : global config & ssh 
```
git config --global user.name "aaromalonline"
git config --global user.email "aaromalonline@gmail.com"
ssh-keygen -t ed25519 -C "aaromalonline@gmail.com" -f ~/.ssh/id_ed25519 -N "" && eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519

copy : cat ~/.ssh/id_ed25519.pub to github ssh keys
ssh -T git@github.com (check connection)
```
### 6. install multimedia codecs:
```
sudo dnf5 group install multimedia --setopt=install_weak_deps=False --exclude=PackageKit-gstreamer-plugin
sudo dnf5 group install sound-and-video
# If you just want all the common codecs in one go (like MP3, H.264, AAC, etc.), you can also do
sudo dnf5 install gstreamer1-plugins-{bad-free,good,ugly,base} \
                 gstreamer1-plugin-openh264 \
                 gstreamer1-libav \
                 lame* --exclude=lame-devel
```

### 7. extensions & tweaks (gnome customisation): 
```
sudo dnf5 upgrade --refresh -y
sudo dnf5 install -y gnome-tweaks (and Extension Manager from flathub softwares)
enable maximize/minimize windows in tweaks 
install extensions - Blur my shell, Apps menu, Place status indicator, Activities Icon & Label, frippery move clock, caffiene, Tiling Assistant
```
### 8. system clock sync (issue) : 
```sudo timedatectl set-local-rtc 1 --adjust-system-clock```
