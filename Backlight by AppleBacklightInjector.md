# Steps to support backlight adjustment

## install iasl

$cd ~/Downloads
$curl --remote-name --progress-bar --location https://bitbucket.org/RehabMan/acpica/downloads/iasl.zip
$unzip iasl.zip
$sudo cp iasl /usr/bin
$sudo chmod 755 /usr/bin/iasl

## Pull code

$mkdir ~/Projects
$cd ~/Projects
$git clone https://github.com/RehabMan/HP-ProBook-4x30s-DSDT-Patch probook.git
$cd ~/Projects
$git clone https://github.com/RehabMan/OS-X-Clover-Laptop-Config.git guide.git

## Compile code

$cd ~/Projects/guide.git
$make

## Apply

1.~/Projects/guide.git/build/SSDT-PNLF.aml
   Copy it EFI/CLOVER/ACPI/patched
2. ~/Projects/probook.git/kexts/AppleBacklightInjector.kext
   Copy it to /Library/Extensions/
3. Edit EFI/CLOVER/config.list, section /KernelAndKextPatches/KextsToPatch

```xml
   <dict>
         <key>Comment</key>
         <string>change F%uT%04x to F%uTxxxx in AppleBacklightInjector.kext (credit RehabMan)</string>
         <key>Name</key>
         <string>com.apple.driver.AppleBacklight</string>
         <key>Find</key>
         <data>RiV1VCUwNHgA</data>
         <key>Replace</key>
         <data>RiV1VHh4eHgA</data>
   </dict>
```

## Fix permission

$sudo kextcache -i /

## Reboot
