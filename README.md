# fail2ban

```bash
yum install epel-release
yum install fail2ban fail2ban-systemd
cp -pf /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

Edit /etc/fail2ban/jail.local
```
[DEFAULT]
bantime = 1h

[sshd]
enabled = true

ignoreip = 127.0.0.1/8
bantime = 600
findtime = 600
maxretry = 5
```


fail2ban-client

Status
```bash
fail2ban-client status
fail2ban-client status sshd
```

Get a config field
```
fail2ban-client get sshd bantime
```
