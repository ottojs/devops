# Windows

## Requirements

- Windows 10
- Windows 11

## Install PowerShell (MSI)

1. [Download PowerShell](https://github.com/PowerShell/PowerShell/releases) (as of writing is v7.4.4 [direct link](https://github.com/PowerShell/PowerShell/releases/download/v7.4.4/PowerShell-7.4.4-win-x64.msi))
1. Run the downloaded `PowerShell-7.4.4-win-x64.msi` file to install

## Check Current ExecutionPolicy

1. Right click start menu buton => Windows PowerShell (Admin)
1. Run `Get-ExecutionPolicy`
1. If "Restricted" Run `Set-ExecutionPolicy AllSigned`

## Verify Virtualization is Enabled

**NOTE:** This may require Windows Professional edition.  
`Get-ComputerInfo -property "HyperVisorPresent"`  
This should return `"True"`  
If not, follow [these instructions to enable Virtualization](https://support.microsoft.com/en-us/windows/enable-virtualization-on-windows-11-pcs-c5578302-6e43-4b4b-a449-8ced115f58e1)

## Install Chocolatey

[Chocolatey Install Docs](https://chocolatey.org/install#individual)  
This is provided for convenience and you should verify it matches above (for security reasons and updates)

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

1. Close all PowerShell windows
1. Right click start menu buton => Windows PowerShell (Admin)
1. Run `choco list`
1. Run `choco install gsudo -y` to install "sudo" capabilty (Windows 11 will eventually have native sudo)
1. Close all PowerShell windows

## Install Windows Terminal

- [GitHub](https://github.com/microsoft/terminal/releases)
- [Microsoft Store](https://apps.microsoft.com/detail/9n0dx20hk701)
- `winget install 9N0DX20HK701 --accept-source-agreements --accept-package-agreements`

## Configure Windows Terminal

### Launch Terminal

```plain
Start
  => Search (just start typing)
    => Terminal
```

### Pin Terminal to Taskbar

```plain
Right Click Terminal icon in bottom Taskbar
  => Pin to taskbar
```

### Edit Settings

```plain
Press "Ctrl+," or ...

In Terminal, near top, next to tabs
  => Click the "down arrow"
    => Settings

Startup (in sidebar)
  => Default profile
    => "PowerShell" (the darker one)

Startup (in sidebar)
  => Default terminal application
    => Terminal

Color schemes (in sidebar)
  => Campbell Powershell
    => Set as default

You can edit this keyboard shortcut or skip
Actions (in sidebar)
  => Add new
    => Clear buffer
      => ctrl+shift+k
        => Save

All Done
  => Press "Save" on bottom right
    => Close Settings Tab
```

## Recommended Packages

```powershell
# Settings
choco feature enable --name="exitOnRebootDetected"

# BAse
sudo choco install git -y
sudo choco install nodejs-lts -y
sudo choco install go -y

# If using containers (Kubernetes, etc.)
sudo choco install podman-desktop -y
sudo choco install podman-cli -y
```

## Install WSL2 (Windows Subsystem for Linux)

- [Microsoft Store WSL Announcement](https://devblogs.microsoft.com/commandline/the-windows-subsystem-for-linux-in-the-microsoft-store-is-now-generally-available-on-windows-10-and-11/)
- [GitHub](https://github.com/microsoft/WSL/releases)
- [Debian Microsoft Store](https://apps.microsoft.com/detail/9msvkqc78pk6)

### Already have WSL?

1. Check WSL Version (We require v2.2.4 or later)
1. `wsl --version`
1. Run `wsl --shutdown` to stop all running WSL VMs
1. Run `wsl --update` to upgrade to the latest version

### Install WSL2 with Debian

Here we install WSL2 and use Debian as the distribution (the default distribution is Ubuntu)

**NOTE:** You'll be prompted to pick a username and password. Because your PC is already protected by a login, it is recommended to pick an easy username and password so you don't forget (example: we choose "user" for both username and password)

1. `wsl --install Debian`
1. Restart Your PC

### Error?

If you get an error like below, you probably have not enabled virtualization in your BIOS/UEFI or your CPU does not support it. See the above section "Verify Virtualization is Enabled"

```powershell
WslRegisterDistribution failed with error: 0x80370102
Please enable the Virtual Machine Platform Windows feature and ensure virtualization is enabled in the BIOS.
For information please visit https://aka.ms/enablevirtualization
Press any key to continue...
```

### Entering WSL

1. `wsl` should get you in but...
1. `wsl --shell-type login` is preferred as it is a full login shell

### Setup Debian on WSL

```bash
wsl --shell-type login;

sudo apt-get update;
sudo apt-get dist-upgrade -y;
sudo apt-get autoremove;
exit

wsl --terminate Debian;
wsl --shell-type login;

# Recommended Packages
sudo apt-get install -y vim htop tree jq wget curl build-essential;
```

### Recreate WSL Debian ("Reinstall")

```powershell
# Show installed WSL distributions
wsl --list;

# Recreate Debian as an example
wsl --terminate Debian;
wsl --unregister Debian;
wsl --install Debian;
```

## Android Development

If you are developing an app, you'll need these too.

- [Android Releases](https://developer.android.com/studio/releases)
- [Android JDKS](https://developer.android.com/build/jdks)

```powershell
sudo choco install Temurin21 -y
sudo choco install android-sdk -y
sudo choco install AndroidStudio -y
```

**Optional - Intel HAXM**
Deprecated in January 2023 but may be useful in speeding up emulators.
If you are unsure, you can skip installing this.

- [Intel HAXM Downloads](https://github.com/intel/haxm/releases)
- [Intel HAXM Instructions](https://github.com/intel/haxm/wiki/Installation-Instructions-on-Windows)
