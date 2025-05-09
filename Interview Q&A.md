# Top 20 Linux Scenario-Based Interview Questions and Answers (with Examples)

## 1. Scenario: A server you manage becomes unresponsive. What are your first steps?
**Answer:** Ping the server to check connectivity. If unreachable, check the hypervisor or console access. If reachable, use SSH and check system load with `top`, disk space with `df -h`, and logs with `dmesg` or `/var/log/messages`.

**Example:**
```bash
ping 192.168.1.10
ssh user@192.168.1.10
top
df -h
```

## 2. Scenario: You get a report that a Linux server is slow. How do you investigate?
**Answer:** Use `top`, `htop`, or `vmstat` to check CPU and memory usage. Use `iotop` for disk I/O. Analyze running processes and system logs.

**Example:**
```bash
uptime
htop
iotop
```

## 3. Scenario: How do you troubleshoot high CPU usage on a Linux system?
**Answer:** Run `top` or `ps aux --sort=-%cpu`. Identify the top-consuming process. Check if it's expected, misbehaving, or stuck in a loop.

**Example:**
```bash
ps aux --sort=-%cpu | head -5
```

## 4. Scenario: A user cannot SSH into a server. What do you check?
**Answer:** Check network access and `sshd` status (`systemctl status sshd`). Validate firewall rules (`iptables`/`firewalld`). Confirm user account and permissions.

**Example:**
```bash
systemctl status sshd
sudo iptables -L
tail -n 50 /var/log/secure
```

## 5. Scenario: How do you find which process is using a specific port?
**Answer:** Use `lsof -i :<port>` or `netstat -tulnp | grep <port>`. Alternatively, use `ss -tulnp`.

**Example:**
```bash
sudo lsof -i :8080
```

## 6. Scenario: Disk space is full on a production server. What do you do?
**Answer:** Run `df -h` to confirm. Use `du -sh * | sort -h` in `/var` or `/home` to find large files. Clean logs, temp files, or move data.

**Example:**
```bash
df -h
du -sh /var/* | sort -h
```

## 7. Scenario: How do you check if a cron job ran successfully?
**Answer:** Inspect the user's `cron` log in `/var/log/cron` or job-specific output logs. Use `crontab -l` to list scheduled jobs.

**Example:**
```bash
grep CRON /var/log/syslog
```

## 8. Scenario: How do you find and kill a zombie process?
**Answer:** Zombie processes are listed as 'Z' in `ps aux`. Find the parent PID and restart the parent process if it's not reaping zombies.

**Example:**
```bash
ps aux | grep 'Z'
```

## 9. Scenario: A system rebooted unexpectedly. How do you find the cause?
**Answer:** Check `last -x` for reboot history. Use `journalctl -b -1` or `/var/log/messages` to investigate logs before the reboot.

**Example:**
```bash
last -x | grep reboot
journalctl -b -1
```

## 10. Scenario: How do you create and manage users in Linux?
**Answer:** Use `useradd`, `passwd`, and `usermod` commands. Set appropriate groups and permissions. Use `/etc/passwd` and `/etc/shadow` for verification.

**Example:**
```bash
sudo useradd devuser
sudo passwd devuser
```

## 11. Scenario: You need to find all files modified in the last 2 days. How?
**Answer:** Use `find /path -type f -mtime -2` to locate recently modified files.

**Example:**
```bash
find /home -type f -mtime -2
```

## 12. Scenario: A partition is filling up due to log files. What’s your solution?
**Answer:** Implement log rotation with `logrotate`. Move old logs to backup or compress them. Automate cleanup with cron.

**Example:**
```bash
logrotate -d /etc/logrotate.conf
```

## 13. Scenario: How do you check memory usage and identify memory leaks?
**Answer:** Use `free -m`, `top`, or `vmstat`. Tools like `smem`, `pmap`, or `valgrind` can help debug memory leaks.

**Example:**
```bash
free -m
```

## 14. Scenario: How do you change the default runlevel or target in systemd systems?
**Answer:** Use `systemctl set-default multi-user.target` or `graphical.target`. Legacy systems used `/etc/inittab`.

**Example:**
```bash
systemctl set-default multi-user.target
```

## 15. Scenario: How do you secure SSH access on a Linux server?
**Answer:** Disable root login, change default port, use key-based authentication, and configure fail2ban or similar tools.

**Example:**
```bash
sudo nano /etc/ssh/sshd_config  # Set PermitRootLogin no
```

## 16. Scenario: You need to search for a string in all `.log` files under `/var/log`. How?
**Answer:** Use `grep -R 'search-string' /var/log/*.log` or `find /var/log -name '*.log' -exec grep 'search-string' {} +`.

**Example:**
```bash
grep -Ri "error" /var/log/*.log
```

## 17. Scenario: How do you monitor disk I/O in real-time?
**Answer:** Use `iotop`, `iostat`, or `dstat` to monitor I/O usage and bottlenecks.

**Example:**
```bash
sudo iotop
```

## 18. Scenario: How do you schedule a recurring job every 5 minutes?
**Answer:** Add `*/5 * * * * /path/to/script.sh` in `crontab -e`. Make sure the script has execution permissions.

**Example:**
```bash
crontab -e
# Add:
*/5 * * * * /usr/local/bin/backup.sh
```

## 19. Scenario: A service failed to start. How do you troubleshoot it?
**Answer:** Check the service status with `systemctl status servicename`. Use `journalctl -u servicename` for detailed logs.

**Example:**
```bash
systemctl status nginx
journalctl -u nginx
```

## 20. Scenario: How do you copy a directory from one Linux server to another securely?
**Answer:** Use `scp` or `rsync`.

**Example:**
```bash
scp -r /var/www user@192.168.1.2:/var/backup
```
