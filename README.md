# MOTD

Message Of The Day

## HOWTO

### Static MOTD

* Approach 1: Banner

```bash
# prepare a banner file, let's say <sshd_banner>, place it under /etc/ssh/
echo "\nBanner /etc/ssh/sshd_banner" >> /etc/ssh/sshd_config
```

* Approach 2: MOTD

```bash
# place your text/message to
/etc/motd

# restart SSH service
sudo systemctl restart sshd

# if you wanna apply some color, follow below steps
# but first, save your plain text into a file let's call it <motd_text>
echo -en "\033[1;32m" | sudo tee /etc/motd
sudo cat /etc/motd_text | sudo tee -a /etc/motd
echo -en "\033[0m" | sudo tee -a /etc/motd
```

### Dynamic MOTD

To view the built-in dynamic MOTD
```console
ls /etc/update-motd.d/
00-header
10-help-text
50-motd-news
85-fwupd
88-esm-announce
90-updates-available
91-contract-ua-esm-status
91-release-upgrade
92-unattended-upgrades
95-hwe-eol
98-fsck-at-reboot
98-reboot-required
```

To disable certain dynamic MOTD
```bash
sudo chmod -x /etc/update-motd.d/xx-yyyyyy
```

To create a new dynamic MOTD
```bash
sudo touch /etc/update-motd.d/00-xyz
sudo chmod +x /etc/update-motd.d/00-xyz
```

To check MOTD scripts errors
```bash
run-parts /etc/update-motd.d/ > /dev/null
```

To disable last login info
```bash
# put the below configuration into /etc/ssh/sshd_config
PrintLastLog no

# restart SSH service
sudo systemctl restart sshd
```
