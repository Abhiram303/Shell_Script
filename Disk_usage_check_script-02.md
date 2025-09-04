# Disk Usage Check Script
**Goal:**
> Check the disk usage of / (root) partition.
> If usage is more than 80%, print a warning message; otherwise, print Disk usage is normal.

```bash
#!/bin/bash

# Get disk usage percentage for root partition
usage=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

echo "Current Disk Usage: $usage%"

# Check if usage > 80
if [ "$usage" -gt 80 ]; then
    echo "WARNING: Disk usage is above 80%! Please take action."
else
    echo "Disk usage is normal."
fi
```
