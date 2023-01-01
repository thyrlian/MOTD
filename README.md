# MOTD

Message Of The Day

## HOWTO

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

To disable last login info
```bash
# put the below configuration into /etc/ssh/sshd_config
PrintLastLog no

# restart SSH service
sudo systemctl restart sshd
```
