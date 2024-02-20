Some times when i run apps, my laptop used to get very slow in its processes and it would just make it uncomfortbale to run Activity Report on my mac. 

So here is a simple bash script that will output your CPU load, Memory and disc space usage. 

```bash
#!/bin/bash

# Gets CPU usage
cpu_usage=$(top -l 1 | grep "CPU usage" | sed -E 's/.*user, ([0-9]+\.[0-9]+)% idle.*/\1/')

# Gets Memory Usage
memory_usage=$(vm_stat | awk 'NR==2 {print (($3 + $5) / 1024) * 4 / (1024 * 1024) * 100 }')

# Gets disk space usage
disk_usage=$(df -h | awk '$NF=="/" {print $5}' | sed 's/%//')

echo "System Monitoring Report:"
echo "CPU Usage: ${cpu_usage}%"
echo "Memory Usage: ${memory_usage}%"
echo "Disk Usage: ${disk_usage}%"

```
