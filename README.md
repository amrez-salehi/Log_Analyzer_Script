# Log_Analyzer_Script


## Project Goal

The goal of this project is to help practice basic shell scripting skills. You will use a shell script to analyze **nginx access logs** and get useful statistics from them. This project helps you learn how to use commands like `awk`, `sort`, `uniq`, `head`, `grep`, and `sed` to process text files from the command line.

---

## Features

The script reads an nginx access log file and outputs:

1. **Top 5 IP addresses with the most requests**
2. **Top 5 most requested paths**
3. **Top 5 response status codes**
4. **Top 5 user agents**

Example output:

```
Top 5 IP addresses with the most requests:
45.76.135.253 - 1000 requests
142.93.143.8 - 600 requests
178.128.94.113 - 50 requests
43.224.43.187 - 30 requests
178.128.94.113 - 20 requests

Top 5 most requested paths:
/api/v1/users - 1000 requests
/api/v1/products - 600 requests
/api/v1/orders - 50 requests
/api/v1/payments - 30 requests
/api/v1/reviews - 20 requests

Top 5 response status codes:
200 - 1000 requests
404 - 600 requests
500 - 50 requests
401 - 30 requests
304 - 20 requests

Top 5 user agents:
Mozilla/5.0 ... - 100 requests
DigitalOcean Uptime Probe 0.22.0 ... - 80 requests
```

---

## Requirements

* Linux or macOS terminal
* Basic shell commands (`awk`, `sort`, `uniq`, `head`)

---

## Setup Instructions

1. **Download the log file**
   Save the nginx access log file in a folder, e.g., `/home/amir/logs/access.log`.

2. **Create the script**
   Save the following script as `analyze_logs.sh`:

```bash
#!/bin/bash

LOG_FILE="/path/to/your/access.log"

echo "Top 5 IP addresses with the most requests:"
awk '{print $1}' $LOG_FILE | sort | uniq -c | sort -nr | head -5

echo ""
echo "Top 5 most requested paths:"
awk '{print $7}' $LOG_FILE | sort | uniq -c | sort -nr | head -5

echo ""
echo "Top 5 response status codes:"
awk '{print $9}' $LOG_FILE | sort | uniq -c | sort -nr | head -5

echo ""
echo "Top 5 user agents:"
awk -F'"' '{print $6}' $LOG_FILE | sort | uniq -c | sort -nr | head -5
```

> Replace `/path/to/your/access.log` with the full path to your log file.

3. **Make the script executable**

```bash
chmod +x analyze_logs.sh
```

4. **Run the script**

```bash
./analyze_logs.sh
```

---

## How It Works

* **IP addresses:** Extract the first field from each line (`awk '{print $1}'`) and count occurrences.
* **Paths:** Extract the 7th field (`awk '{print $7}'`) and count occurrences.
* **Status codes:** Extract the 9th field (`awk '{print $9}'`) and count occurrences.
* **User agents:** Split each line by `"` (`awk -F'"' '{print $6}'`) and count occurrences.

All counts are sorted in descending order, then the top 5 results are displayed.

---

## Stretch Goals

* Try to implement the same analysis using `grep` and `sed` instead of `awk`.
* Add an option to analyze a custom log file path without editing the script.

---

## License

This project is for learning purposes and open to anyone to use and modify.

---

If you want, I can also **add a small diagram to explain the data flow in the script**, which makes the README look more professional.
