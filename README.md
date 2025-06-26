# FTP Speed Monitor

A Bash script that continuously monitors FTP server upload and download speeds, logging results for performance analysis.

## Overview

This script performs automated FTP speed tests by uploading and downloading a test file at regular intervals. It's designed to help monitor FTP server performance over time and identify potential connectivity issues.

## Features

- **Continuous Monitoring**: Runs upload/download tests every 5 minutes (configurable)
- **Speed Measurement**: Measures both upload and download speeds
- **Automatic Logging**: Results are logged with timestamps to a file
- **Stuck File Cleanup**: Automatically detects and removes stuck temporary files that could interfere with tests
- **Real-time Output**: Displays results in terminal while logging to file

## Prerequisites

This script requires the following tools to be installed:

- `wget` - for download speed testing
- `wput` - for upload speed testing
- `curl` - for file existence checking and cleanup

### Installation on macOS

Install the required tools using [Homebrew](https://brew.sh/):

```bash
brew install wget wput curl
```

### Installation on Linux

Most Linux distributions include `wget` and `curl` by default. Install `wput`:

```bash
# Ubuntu/Debian
sudo apt-get install wput

# CentOS/RHEL
sudo yum install wput
```

## Configuration

Before running the script, you need to configure the following variables in `ftp_check.sh`:

```bash
ftpu="ftp.domain.com"               # Your FTP server URL
ftpp="/automated_test/"             # FTP directory path
ftpusr="username"                   # FTP username
ftppw="password"                    # FTP password
tfn="testfile.zip"                  # Test file name
tfloc="$HOME/Desktop/"              # Local test file location
lfn="wpuget.log.txt"                # Log file name
lfloc="$HOME/Desktop/"              # Log file location
stime=300                           # Sleep time between tests (seconds)
```

## Usage

1. **Prepare Test File**: Place your test file (e.g., `testfile.zip`) in the specified local directory
2. **Configure Script**: Edit the variables in `ftp_check.sh` with your FTP server details
3. **Make Executable**: 
   ```bash
   chmod +x ftp_check.sh
   ```
4. **Run Script**:
   ```bash
   ./ftp_check.sh
   ```

## Output

The script outputs results in the following format:

```
Start Test @ Mon Apr  1 10:00:00 PDT 2019
Mon Apr  1 10:00:05 PDT 2019 UL 1.2 MB/s
Mon Apr  1 10:00:10 PDT 2019 DL 2.3 MB/s

Mon Apr  1 10:05:05 PDT 2019 UL 1.1 MB/s
Mon Apr  1 10:05:10 PDT 2019 DL 2.1 MB/s
```

Results are simultaneously displayed in the terminal and logged to the specified log file.

## Log File

The script creates/maintains a log file (`wpuget.log.txt` by default) containing:
- Timestamp for each test
- Upload speeds (UL)
- Download speeds (DL)

## Stopping the Script

Press `Ctrl+C` to stop the monitoring script.

## Version History

- **v1.0**: Initial version with basic upload/download speed testing
- **v1.2**: Added function to check and remove stuck temporary files

## License

This project is open source. Feel free to modify and distribute as needed.

## Troubleshooting

### Common Issues

1. **Permission Denied**: Ensure the script has execute permissions (`chmod +x ftp_check.sh`)
2. **Command Not Found**: Install required tools (`wget`, `wput`, `curl`)
3. **FTP Connection Failed**: Verify FTP credentials and server accessibility
4. **Test File Missing**: Ensure the test file exists in the specified local directory

### Notes

- The script overwrites the test file on the server during upload tests
- Downloaded files are redirected to `/dev/null` to avoid cluttering local storage
- The script includes cleanup functionality specific to certain FTP server configurations 