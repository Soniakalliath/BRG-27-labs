# Apache Log Parser: Failed Requests Only

This Bash script extracts and displays only HTTP requests with a status code of 400 or higher from an Apache log file.

## Script

```bash
#!/bin/bash

LOGFILE="/var/log/apache2/access.log"
REGEX='^([0-9]+\.[0-9]+\.[0-9]+\.[0-9]+) .* \[([^\]]+)\] "([A-Z]+) ([^ ]+) HTTP/[0-9.]+" ([0-9]{3}) ([0-9]+|-)'

echo "FAILED REQUESTS:"
echo "IP Address     | Date/Time              | Method | URL           | Status | Bytes"
echo "--------------------------------------------------------------------------------"

while IFS= read -r line; do
    if [[ $line =~ $REGEX ]]; then
        status="${BASH_REMATCH[5]}"
        if (( status >= 400 )); then
            ip="${BASH_REMATCH[1]}"
            datetime="${BASH_REMATCH[2]}"
            method="${BASH_REMATCH[3]}"
            url="${BASH_REMATCH[4]}"
            bytes="${BASH_REMATCH[6]}"

            printf "%-14s | %-21s | %-6s | %-13s | %-6s | %-6s\n" \
                "$ip" "$datetime" "$method" "$url" "$status" "$bytes"
        fi
    fi
done < "$LOGFILE"
```
