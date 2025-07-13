---
title: "Remote Logging with Rsyslog"
date: 2015-10-04
draft: false
tags: ["rsyslog", "logging", "system-administration", "remote-logging", "linux"]
categories: ["System Administration"]

---


**RSYSLOG** is the rocket-fast system for log processing. After syslog, now rsyslog comes pre-built with the Linux systems, meant for local and remote logging. In any system, you will want to:

- **(a)** Log the system and application logs on the local machine, and/or
- **(b)** Log the system and application logs to a remote machine

Below given are 2 cases, useful for forwarding OS logs and application logs:

## Forwarding only OS logs

Add the below given line at the bottom of the `/etc/rsyslog.conf` file, and later restart the rsyslog service:

```bash
*.info;authpriv.*;cron.*;mail.* @remote_ip:514
```

By default, rsyslog uses port number **514** for its activities. If the logs need to be forwarded through UDP, mention a single `@` before the remote_ip, and for TCP, mention `@@` before the remote_ip.

**Log types explained:**
- `*.info` – all logs with info severity
- `authpriv.*` – all logs related to authorization and privileges
- `cron.*` – all logs related to cron – scheduled jobs
- `mail.*` – all logs related to mail and mail servers

## Forwarding OS and Application logs

### 1. Load the required module

Add the following module - it is the module for forwarding logs from a file. Add this along with the other `$ModLoad` tags at the top of the file:

```bash
# Add the following module - it is the module for forwarding logs from a file.
# Add this along with the other $ModLoad tags at the top of the file
$ModLoad imfile
```

### 2. Modify the messages configuration

Add `local7.none` to the below line as shown below. This will stop the logging of local7 messages in `/var/log/messages`, as we need to forward our application logs through local7 service:

```bash
# Add 'local7.none' to the below line as shown below.
# This will stop the logging of local7 messages in /var/log/messages, as we need to forward our application logs through local7 service
*.info;mail.none;local7.none;authpriv.none;cron.none /var/log/messages
```

### 3. Comment out local7 boot logs

Comment the local7 for boot logs, to stop logging the application logs to `/var/log/boot.log` which we are forwarding through local7 service:

```bash
# Comment the local7 for boot logs, to stop logging the application logs to /var/log/boot.log which we are forwarding through local7 service
#local7.* /var/log/boot.log
```

### 4. Configure file monitoring

Add the below lines to forward the logs from their respective files. First 3 lines are variable, the other 2 are static:

```bash
# Add the below lines to forward the logs from their respective files. First 3 lines are variable, the other 2 are static.
# $InputFileName takes the path to log file (absolute path of the file)
# $InputFileTag will attach the mentioned tag (here: tag_jio.com) to the original log
# $InputFileStateFile is the State file where the logs are stored before forwarding (for eg. useful in case of network failure)
$InputFileName /path/to/log/file
$InputFileTag tag_website.com:
$InputFileStateFile buffer_file_name
$InputFileFacility local7
$InputRunFileMonitor
```

**Configuration parameters explained:**
- `$InputFileName` takes the path to log file (absolute path of the file)
- `$InputFileTag` will attach the mentioned tag (here: `tag_website.com`) to the original log
- `$InputFileStateFile` is the State file where the logs are stored before forwarding (e.g. useful in case of network failure)

### 5. Configure log forwarding

Add this line at the bottom of the file, for forwarding:

```bash
# Add this line at the bottom of the file, for forwarding
# local7.* (all logs of local7 - application),
# *.info (all logs with info level),
# authpriv.* (all logs of authorization-privilege) and
# cron.* (all logs of cron)
# - to the receiver IP and Syslog port 514.
# Add '@' for sending logs through UDP, '@@' for TCP.
local7.*;*.info;authpriv.*;cron.* @receiver_IP:514
```

**What gets forwarded:**
- `local7.*` (all logs of local7 - application)
- `*.info` (all logs with info level)
- `authpriv.*` (all logs of authorization-privilege)
- `cron.*` (all logs of cron)

**Protocol selection:**
- Add `@` for sending logs through UDP
- Add `@@` for sending logs through TCP

> **Note:** Above given configuration is for Red Hat based systems only. It may differ in Debian based systems.

## Common Troubleshooting Steps

- **Check network connectivity** between the sender and receiver – Firewall port opening (Port: 514 – TCP/UDP), Ping, Traceroute
- **Check if logs are present** at the mentioned log file path
- **Check the 'space' and 'semicolon'** in the rsyslog configuration file
- **Change the `$InputFileStateFile`'s value** to something else (e.g. change `buffer_file_name` to `buffer_file_name_1`)
- **Restart the rsyslog service**

```bash
sudo systemctl restart rsyslog
```