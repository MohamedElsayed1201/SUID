# SUID File Permission Search Script

This script searches for files with the **SUID** (Set User ID) permission on a Linux system, logs the results to a file, and ensures that the necessary directories and permissions are in place. SUID is a special permission that allows users to execute files with the permissions of the file owner. These files can present a security risk if misconfigured, so it's important to monitor and audit them.

The script uses `find` to search the filesystem for files with the `SUID` permission (`/4000`), logs the details of those files (using `file` to determine file types), and saves the output to a log file.

## Prerequisites

- The script requires `sudo` permissions to search the filesystem for files with the SUID permission and to execute the `find` command on system directories.
- The script assumes that you're working in a Unix-like environment (Linux-based systems).

## Usage

1. **Make the script executable:**

   Ensure the script is executable by running the following command:

   ```bash
   chmod +x find_suid_files.sh

    Run the script:

    Execute the script by running:

./find_suid_files.sh

Script Behavior:

    The script checks if the output directory ($HOME/local/log) exists. If it doesn't, the script creates the directory.
    It ensures that the user has write permissions to the output directory.
    The script searches the entire filesystem for files with the SUID permission (/4000).
    For each file found, it logs the file details using the file command to determine the file type.
    The output is saved in a log file located at ~/local/log/findhack.log.
    It removes the log file upon script completion, but you can disable this cleanup if needed.

Log Output:

After running the script, the results of the search will be logged to the file:

    ~/local/log/findhack.log

    You can check this file for details of the files with the SUID permission found on the system.

Example Output

After the script completes, the log file will contain output similar to the following:

[12-01-2025 14:23:45] Starting SUID files permission search...
Searching for files with SUID permissions...
/usr/bin/passwd:  setuid ELF 64-bit LSB executable, x86-64, version 1 (SYSV)
/bin/su:  setuid ELF 64-bit LSB executable, x86-64, version 1 (SYSV)
/usr/sbin/sudo:  setuid ELF 64-bit LSB executable, x86-64, version 1 (SYSV)
...
File permission inspection completed. Check the log file at: ~/local/log/findhack.log

The script outputs the search results to the log file, including the path to the file and its type, which is determined using the file command.
Script Details

    Dependencies:
        sudo for elevated permissions to search system directories.
        find command to locate files with SUID permissions.
        file command to identify file types (included by default in most Linux distributions).

    Log Directory: The script logs the output to the directory specified in the OUTPUT_DIR variable (default: ~/local/log).

    Search Criteria: The script searches for files with the SUID permission (/4000), which is typically set on files that need to run with elevated privileges.

    Log File: The log file will include a timestamp and details of the files with SUID permissions found during the search.

    Cleanup: The script includes a cleanup function that removes the log file upon exit. If you want to keep the log file, you can comment out or remove the cleanup function in the script.

Optional Configuration

    You can modify the directory where the log file is saved by changing the OUTPUT_DIR variable.
    You can disable the cleanup function by commenting out the trap cleanup EXIT line if you want to retain the log file after the script finishes.

Troubleshooting

    Permissions Issues: The script requires sudo permissions to search system directories and determine file types. If you encounter any permission-related errors, ensure you have the necessary privileges.

    No Files Found: If no files are found with SUID permissions, the log file will be empty (or contain just the timestamp and completion message). This could mean that no such files exist on your system, or they may be located in directories that the script is not searching.

License

This script is provided "as-is." You are free to modify and distribute it under your own terms.


### Key Features of the `README.md`:

- **Installation and Setup**: Provides clear instructions on making the script executable and running it.
- **Log Directory and File**: Explains where the log file is saved and how to review the results.
- **SUID Permission Search**: Details how the script searches for files with the `SUID` permission and logs the output.
- **Cleanup Option**: Offers a cleanup function to remove the log file after execution, with instructions on how to disable it if desired.
- **Customization**: Mentions that you can modify the directory for the log file and adjust the search behavior.
- **Troubleshooting**: Provides guidance on handling common issues such as permissions or no files being found.

This `README.md` should give users clear and comprehensive instructions on how to use the script effectively. Feel free to adjust it based on your needs!
