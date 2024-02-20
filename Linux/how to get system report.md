
Sometimes, when I have several applications running on my laptop, it noticeably slows down, making it difficult to navigate. 

To help me manage this, here is a simple bash script for an overview of CPU load, Memory usage, and Disk Space usage.

```bash
#!/bin/bash

# Gets CPU usage
cpu_usage=$(top -l 1 | awk '/CPU usage/ {print $7}' | cut -d '%' -f 1)

# Gets Memory usage
memory_usage=$(vm_stat | awk '/active/ {print (($3 + $5) / 1024) * 4 / 1024}')

# Gets Disk usage
disk_usage=$(df -h / | awk 'NR==2 {print $5}' | tr -d '%')

echo "System Monitoring Report:"
echo "${cpu_usage}%"
echo "Memory Usage: ${memory_usage} MB"
echo "Disk Usage: ${disk_usage}%"


```
