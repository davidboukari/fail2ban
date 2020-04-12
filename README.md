# fail2ban

## Caution to this big issue: think the problem is the time unit detection 

* https://github.com/fail2ban/fail2ban/issues/2134 

```
 unixpro commented on 19 May 2018

I have found this exact same problem. I have spent ages trying to track down the problem with heavydebug, simplifying filters etc. In fact I came here to find how to help by contributing what I have found out.
CentOS 7.4, fail2ban-server-0.9.7-1.el7, iptables no firewalld.
I have found that on daemon start, the filter works fine but regex detection stops after fail2ban has run through the log file on initial startup. Tried pyinotify, gamin and polling backends.

I've tracked the problem to be something to do with findtime detection - I think the problem is the time unit detection when using normal rsyslog custom logfiles instead of systemd journal. I think

To confirm I set findtime = 32000000 and now I am seeing the expected Found and Ban entries in my /var/log/fail2ban.log.

Therefore I think the problem is with the detection of timestamps in the logfile - possibly/probably with time log units.
```

## Installation

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


## fail2ban-client

### Status
```bash
fail2ban-client status
fail2ban-client status sshd
```

### Get a config field
```
fail2ban-client get sshd bantime
```

### unban client
```bash
fail2ban-client set  owncloud unbanip 123.1.43.5
```
