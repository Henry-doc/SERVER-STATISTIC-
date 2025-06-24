#!/bin/bash
echo "=====SERVER STATISTIC PERPROMANCE====="
echo
echo "====TOTAL CPU USAGE===="
free -m | awk 'NR==2{
    used= $3;
    free= $4;
    total=$2;
    printf "Used: %dMB, Free: %dMB, Usage: %.f%%\n", used, free, (used/total)*100 
}'
echo

echo "====DISK USAGE===="
df -h / | awk 'NR==2 {
    printf "Used: %s, Free: %s, Usage: %s\n", $3, $4, $5
}'
echo

echo "====TOP FIVE PROCESSES BY CPU USAGE===="
ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6
echo 

echo "==TOP FIVE PROCESSES BY MEMORY USAGE===="
ps -eo pid,comm,%mem --sort=-%mem | head -n 6
echo

echo "====OS VERSION===="
cat /etc/os-release | grep PRETTY_NAME | cut -d= -f2 | tr -d '"'
echo

echo "====UPTIME===="
uptime -p
echo

echo "====LOAD AVERAGE===="
uptime | awk -F 'load average: ' '{print $2}'
echo

echo "====LOGGED IN USERS===="
who | wc -l
echo

# project URL
https://github.com/Henry-doc/SERVER-STATISTIC-