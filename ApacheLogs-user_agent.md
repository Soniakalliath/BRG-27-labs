# Apache Log Parser: With User-Agent

This Bash script extracts detailed request information including user-agent string.

## Script

```bash
#!/bin/bash

LOGFILE="/var/log/apache2/access.log"
REGEX='^([0-9]+\.[0-9]+\.[0-9]+\.[0-9]+) .* \[([^\]]+)\] "([A-Z]+) ([^ ]+) HTTP/[0-9.]+" ([0-9]{3}) ([0-9]+|-) "([^"]*)" "([^"]*)"'

echo "IP Address     | Method | URL           | Status | User-Agent"
echo "---------------------------------------------------------------------"

while IFS= read -r line; do
    if [[ $line =~ $REGEX ]]; then
        ip="${BASH_REMATCH[1]}"
        method="${BASH_REMATCH[3]}"
        url="${BASH_REMATCH[4]}"
        status="${BASH_REMATCH[5]}"
        useragent="${BASH_REMATCH[8]}"

        printf "%-14s | %-6s | %-13s | %-6s | %s\n" \
            "$ip" "$method" "$url" "$status" "$useragent"
    fi
done < "$LOGFILE"
```

> Ensure Apache uses the combined log format that includes the user-agent field.
