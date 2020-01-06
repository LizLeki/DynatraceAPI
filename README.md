# Schedule Automatic Enable-Disable Monitor Groups around Maintenance Windows

The two Python scripts in this directory allow you you to automate the creation of scheduled tasks in Windows Task Manager which bulk enable/disable Dynatrace Synthetic Monitors via REST API at times associated with planned maintenance windows.

<b>getSetWindows.py</b> leverages the maintenence window API to retrieve information about scheduled maintenence windows for a given date and creates or updates tasks in Windows Task Manager to trigger a seperate Python script which handles toggling tag groups on/off around each window.

<b>toggleMonitors.py</b> is a lightly modified version of [bulk-enable-disable-monitors](https://github.com/Dynatrace/snippets/tree/master/api/synthetic/bulk-enable-disable-monitors), which toggles synthetic monitors on and off by tag group. This script is executed with associated arguments as determined in getSetWindows.py

The installation and usage sections are written for Windows and may be slightly different on other operating systems.

Note that this script is community driven and is not officially supported through Dynatrace.


## Getting Started

[insert description]

### Prerequisites

* Dynatrace tenant/environment
* [Python3](https://www.python.org/downloads/) (scripts developed using 3.7.3)
   * [pywin32 Windows API access for Python](https://github.com/mhammond/pywin32)
   * [requests HTTP library for Python](https://2.python-requests.org/en/master/)
    
## Usage
The script requires three parameters for execution:
* Dynatrace domain
* API token
* Date

### Basic Usage

1. Generate a [Dynatrace API Token](https://www.dynatrace.com/support/help/extend-dynatrace/dynatrace-api/) with the following permissions enabled

         * Read configuration
         * Create and read synthetic monitors, locations, and nodes

2. Navigate to the script directory in Command Prompt

3. Run the script with the following syntax

         python getSetWindows.py <Dynatrace domain> <API token> <Date>

    DT SaaS Example: 

         python getSetWindows.py "https://mySampleEnv.live.dynatrace.com/" "abcdefjhij1234567890" "2020-01-01"
         
   DT Managed Example:

         python getSetWindows.py "https://mySampleEnv.dynatrace-managed.com/e/SampleEnvironmentID/" "abcdefjhij1234567890" "2020-01-01" 

## Troubleshooting

Please refer to the log.log file that is created in the script execution directory.

## Known Limitations
