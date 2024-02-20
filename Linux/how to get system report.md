Some times when i run apps, my laptop used to get very slow in its processes and it would just make it uncomfortbale to run Activity Report on my mac. 

So here is a simple bash script that will output your CPU load, Memory and disc space usage. 

```bash
#!/bin/bash

# Gets CPU usage
cpu_usage=$(top -l 1 | awk '/CPU usage/ {print $7}' | cut -d '%' -f 1)

# Gets Memory usage
memory_usage=$(vm_stat | awk '/active/ {print (($3 + $5) / 1024) * 4 / 1024}')

# Gets Disk usage
disk_usage=$(df -h / | awk 'NR==2 {print $5}' | tr -d '%')

echo "System Monitoring Report:"
echo "CPU Usage: ${cpu_usage}%"
echo "Memory Usage: ${memory_usage} MB"
echo "Disk Usage: ${disk_usage}%"


```
