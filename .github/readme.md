# Ubuntu unattended-upgrades

Semi-customized sane defaults

## Config steps

### 1. Get it

```bash
git clone https://github.com/dev01d/unattended-upgrades.git \
&& cd unattended-upgrades
```

### 2. Edit the config files for your maintenance window

- `50unattended-upgrades` provides the `Automatic-Reboot-Time` option
- `download-override.conf` provides the time potential updates are pulled down
- `upgrade-override.conf` provides the time upgrades are performed

### 3. Install it

'One-liner' install:

<!-- spellchecker: disable -->

```bash
sudo cp -v *-upgrades /etc/apt/apt.conf.d/ \
&& sudo mkdir -p /etc/systemd/system/apt-daily.timer.d/ \
&& sudo mkdir -p /etc/systemd/system/apt-daily-upgrade.timer.d/ \
&& sudo cp -v download-override.conf /etc/systemd/system/apt-daily.timer.d/override.conf \
&& sudo cp -v upgrade-override.conf /etc/systemd/system/apt-daily-upgrade.timer.d/override.conf \
&& sudo systemctl restart apt-daily.timer \
&& sudo systemctl status apt-daily.timer \
&& sudo systemctl restart apt-daily-upgrade.timer \
&& sudo systemctl status apt-daily-upgrade.timer \
&& cd .. \
&& rm -rf unattended-upgrades
```

<!-- spellchecker: enable -->

## Usage

Test with:

```bash
unattended-upgrade -v --dry-run
```

Manually upgrade with:

```bash
unattended-upgrade -v
```
