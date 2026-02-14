# Installing SF Mono on Fedora

## Prerequisites

Install `p7zip` to extract the `.dmg` archive:

```bash
sudo dnf install p7zip p7zip-plugins

Download and Extract

    Create a working directory and download the font:

bash
mkdir sfmono && cd sfmono
wget https://devimages-cdn.apple.com/design/resources/download/SF-Mono.dmg

    Extract the .dmg:

bash
7z x SF-Mono.dmg

    Extract the font files from the nested package:

bash
cd SFMonoFonts.pkg
gunzip < Payload | cpio -id

This creates a Library/Fonts/ directory containing the .otf files.
Install the Fonts

User-only installation:

bash
mkdir -p ~/.local/share/fonts/SFMono
cp Library/Fonts/*.otf ~/.local/share/fonts/SFMono/
fc-cache -fv

System-wide installation:

bash
sudo mkdir -p /usr/local/share/fonts/SFMono
sudo cp Library/Fonts/*.otf /usr/local/share/fonts/SFMono/
sudo chown -R root: /usr/local/share/fonts/SFMono
sudo chmod 644 /usr/local/share/fonts/SFMono/*
sudo restorecon -vFr /usr/local/share/fonts/SFMono
sudo fc-cache -fv

    Note: The restorecon command sets correct SELinux labels on Fedora.

Verify Installation

bash
fc-list | grep "SF Mono"

You should see entries like SF Mono Regular, SF Mono Bold, etc.
Cleanup

bash
cd ../..
rm -rf sfmono
