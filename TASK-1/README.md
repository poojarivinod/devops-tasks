**Date:** `29-01-2026`
# TASK-1: Linux Commands

This guide covers basic to intermediate Linux commands commonly used in DevOps.

---

## Level 1: Basic Linux Commands

### 1. Create a directory
```bash
mkdir ~/linux_practice
cd ~/linux_practice
```

### 2. Create 5 empty files
```bash
touch file1.txt file2.txt file3.txt file4.txt file5.txt
```

### 3. Write your name and today’s date into file1.txt
```bash
echo "Name: Vinod" > file1.txt
date >> file1.txt
```

### 4. Display content using cat and less
```bash
cat file1.txt
less file1.txt
```

### 5. Copy file1.txt
```bash
cp file1.txt backup_file1.txt
```

### 6. Rename file2.txt to data.txt
```bash
mv file2.txt data.txt
```

### 7. Delete file5.txt
```bash
rm file5.txt
```

---

## Level 2: File Permissions & Ownership

### 8. Check permissions
```bash
ls -l
```

### 9. Change permission of data.txt to rw-r-----
```bash
chmod 640 data.txt
```

### 10. Make file3.txt executable
```bash
chmod +x file3.txt
```

### 11. Change ownership of file4.txt
```bash
sudo chown username:username file4.txt
```

### 12. Permission explanation
- **r (read)** – view file contents
- **w (write)** – modify file
- **x (execute)** – run file as a program

---

## Level 3: Searching & Viewing Files

### 13. Search word Linux
```bash
grep "Linux" *.txt
```

### 14. Count lines, words, characters
```bash
wc file1.txt
```

### 15. Display last 10 lines of logs
```bash
tail -n 10 /var/log/syslog
# OR
tail -n 10 /var/log/messages
```

### 16. Find all .txt files
```bash
find ~/linux_practice -name "*.txt"
```

---

## Level 4: Process & System Monitoring

### 17. List running processes
```bash
ps aux
```

### 18. Find PID of sshd or systemd
```bash
ps aux | grep sshd
ps aux | grep systemd
```

### 19. Kill a process
```bash
kill <PID>
```

### 20. Check CPU and memory usage
```bash
top
# OR
htop
```

### 21. Disk usage
```bash
df -h
du -sh ~/linux_practice
```

---

## Level 5: Package Management

### 22. Install tree
```bash
sudo yum install tree -y
# OR
sudo dnf install tree -y
# OR
sudo apt install tree -y
```

### 23. Remove tree
```bash
sudo yum remove tree -y
sudo dnf remove tree -y
sudo apt remove tree -y
```

### 24. Check git version
```bash
git --version
```

### 25. List installed packages
```bash
yum list installed
dnf list installed
apt list --installed
```

---

## Level 6: Networking Basics

### 26. Check IP address
```bash
ip addr show
# OR
ifconfig
```

### 27. Test connectivity
```bash
ping google.com
```

### 28. Display open ports
```bash
ss -tulnp
# OR
netstat -tulnp
```

### 29. Check DNS configuration
```bash
cat /etc/resolv.conf
```

### 30. Download a file
```bash
wget https://example.com/file.txt
# OR
curl -O https://example.com/file.txt
```

---

## Author
**Vinod**  
Linux & DevOps Practice

