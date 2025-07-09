# Apache Log Parser: CSV Output

This Bash script parses an Apache log and outputs the results in CSV format.

## Script

```bash
#!/bin/bash

LOGFILE="/var/log/apache2/access.log"
REGEX='^([0-9]+\.[0-9]+\.[0-9]+\.[0-9]+) .* \[([^\]]+)\] "([A-Z]+) ([^ ]+) HTTP/[0-9.]+" ([0-9]{3}) ([0-9]+|-)'

echo "ip,date_time,method,url,status,bytes"

while IFS= read -r line; do
    if [[ $line =~ $REGEX ]]; then
        ip="${BASH_REMATCH[1]}"
        datetime="${BASH_REMATCH[2]}"
        method="${BASH_REMATCH[3]}"
        url="${BASH_REMATCH[4]}"
        status="${BASH_REMATCH[5]}"
        bytes="${BASH_REMATCH[6]}"

        echo "$ip,\"$datetime\",$method,$url,$status,$bytes"
    fi
done < "$LOGFILE"
```
