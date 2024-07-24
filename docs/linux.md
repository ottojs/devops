# Linux

## Recommended Packages

### Debian / Ubuntu

- Debian 12 - Bookworm
- Ubuntu 24.04 - Noble Numbat

```bash
# Upgrade Packages
sudo apt-get update;
sudo apt-get dist-upgrade -y;
sudo apt-get autoremove;
# Rebooting is recommended
# reboot

# Recommended Packages
sudo apt-get install -y vim htop tree jq wget curl build-essential;
```

### Arch (2024-07)

**NOTE:** Node.js "Iron" is v20.x

```bash
# Upgrade Packages
# Recommendation is to perform upgrades at least once per week
sudo pacman -Syu;
# Rebooting is recommended
# reboot

# Recommended Packages
sudo pacman -S --needed base-devel linux-headers linux-lts-headers go nodejs-lts-iron vim wget curl tree jq htop ansible kubectx kube-linter helm yamllint;
```
