# Nmap Port Scanning Automation with Python Scripts

This guide will walk you through using a simple Python script to scan for open ports on a target IP address using the `nmap` library. The script will then generate a text file report with the scan results.

## Prerequisites

Before you begin, you need to have the following installed on your system:

1.  **Python:** This script is written in Python. If you don't have it installed, you can download it from [python.org](https://www.python.org/downloads/).

2.  **Nmap:** The script uses the Nmap tool. You must install it on your system. You can find the installation instructions for your operating system on the [Nmap website](https://nmap.org/download.html).

3.  **python-nmap library:** You need to install the Python library that allows the script to interact with Nmap. You can install it using `pip`:
    ```bash
    pip install python-nmap
    ```

## Setup

1.  **Create the Python Script:**
    Open a text editor and save the following Python code in a file named `scanner.py`.

    ```python
    import nmap
    import sys
    import time

    print("\nRunning...\n")

    nm_scan = nmap.PortScanner()

    # The script expects the target IP as a command-line argument.
    # It scans port 80 using a SYN scan ('-sS').
    nm_scanner = nm_scan.scan(sys.argv[1], '80', arguments='-sS')

    # Extracting scan results
    host_is_up = "The host is: " + nm_scanner['scan'][sys.argv[1]]['status']['state'] + ".\n"
    port_open = "The port 80 is: " + nm_scanner['scan'][sys.argv[1]]['tcp'][80]['state'] + ".\n"
    method_scan = "The method of scan is: " + nm_scanner['scan'][sys.argv[1]]['tcp'][80]['reason'] + ".\n"

    # Writing the report to a file
    with open("%s.txt" % sys.argv[1], 'w') as f:
        f.write(host_is_up + port_open + method_scan)
        f.write("\nReport generated " + time.strftime("%Y-%m-%d_%H:%M:%S GMT", time.gmtime()))

    print("\nFinished...")
    ```

## Execution

1.  **Open your command prompt or terminal.**

2.  **Navigate to the directory where you saved `scanner.py`.**
    For example, if you saved it in a `Downloads` folder, you would use:
    ```bash
    cd Downloads
    ```

3.  **Run the script** by typing `python scanner.py` followed by the IP address you want to scan. For example, to scan the IP `142.250.69.238`, you would run:
    ```bash
    python scanner.py 142.250.69.238
    ```
    The terminal will show "Running..." and then "Finished..." once the scan is complete.
    
    *You can add your screenshot of this step here. Upload the image to your GitHub repo and use the following format: `![Running the scanner](link/to/your/image.png)`*

## Output

After the script finishes, it will create a `.txt` file named after the IP address you scanned (e.g., `142.250.69.238.txt`) in the same directory.

You can view the contents of this file using the `more` command in the command prompt or by opening it with a text editor.

```bash
more 142.250.69.238.txt
```

The output inside the file will look like this:

```
The host is: up.
The port 80 is: open.
The method of scan is: syn-ack.

Report generated 2025-06-11_03:20:00 GMT
```

This indicates that the host at the specified IP address is online, and port 80 is open. The report also includes the time the scan was generated.

![Viewing the report](https://github.com/SunilKumarPeela/Images/blob/main/nmappython1.png)

---

![Viewing the report](https://github.com/SunilKumarPeela/Images/blob/main/nmapython2.png)

---

![Viewing the report](https://github.com/SunilKumarPeela/Images/blob/main/nmappython3.png)


