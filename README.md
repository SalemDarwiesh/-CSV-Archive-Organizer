# CSV Archive Organizer

This Python script processes ZIP archives containing CSV files. It extracts the CSVs, renames them based on their creation date within the ZIP, and moves them to designated output folders based on filename prefixes. This automates the organization of data files extracted from archives.

## Features

*   **ZIP File Extraction:** Extracts CSV files from ZIP archives.
*   **Date-Based Renaming:** Renames CSV files based on their creation date (obtained from the ZIP file metadata).
*   **Prefix-Based Sorting:** Moves renamed files into designated output folders based on filename prefixes.
*   **Collision Handling:**  Handles potential filename collisions by adding a counter to duplicate filenames.
*   **Automatic Cleanup:**  Deletes the original ZIP file and temporary extraction directory after processing.
*   **Configurable:**  All input and output paths, file-to-folder mappings, and the logging level are configurable via command-line arguments.
*   **Error Handling:**  Includes error handling and logging for robust operation.

## Requirements

*   Python 3.x
*   No external libraries are required (uses only standard library modules: `os`, `zipfile`, `datetime`, `shutil`, `logging`, `argparse`).

## Usage

```bash
python csv_archiver_workflow.py <downloads_path> <extract_base_path> <destination_base_path> -f "prefix1:folder1 prefix2:folder2 ..." [-l LOG_LEVEL]
Use code with caution.
Markdown
Arguments:

downloads_path (required): The path to the directory containing the ZIP files.

extract_base_path (required): The base path for the temporary extraction directory. A subdirectory will be created under this path for each ZIP file.

destination_base_path (required): The base path for the output folders. Subfolders will be created under this path as specified by the -f argument.

-f / --file_to_folder (required): Specifies the mapping between filename prefixes and output folder names. This argument takes one or more prefix:folder pairs, separated by spaces.

Example: -f "ReportTypeA:OutputFolderA ReportTypeB:OutputFolderB"

Files starting with ReportTypeA will be moved to a folder named OutputFolderA within the destination_base_path.

Files starting with ReportTypeB will be moved to a folder named OutputFolderB within the destination_base_path.

-l / --log_level (optional): Sets the logging level. Defaults to INFO. Allowed values: DEBUG, INFO, WARNING, ERROR, CRITICAL.

Complete Example:

python csv_archiver_workflow.py "/home/user/Downloads" "/tmp/extract" "/home/user/Data/Processed" -f "DataFileA:FolderA DataFileB:FolderB" -l DEBUG
Use code with caution.
Bash
This command:

Processes ZIP files in /home/user/Downloads that start with "DataFiles-".

Extracts the ZIP files to temporary subdirectories under /tmp/extract.

Renames the CSV files based on their creation date.

Moves files starting with DataFileA to /home/user/Data/Processed/FolderA.

Moves files starting with DataFileB to /home/user/Data/Processed/FolderB.

Deletes the original ZIP files and temporary extraction directories.

Logs all actions with the DEBUG level (very verbose).

Important Notes

The script assumes that all CSV files within a ZIP have their dates in the same format as the ZIP file itself.

The script expects the ZIP file names to start with "DataFiles-" (this can be easily modified in the main function if needed).

The -f argument must be provided, and it must be in the correct format (prefix1:folder1 prefix2:folder2 ...).

The script will create any necessary output folders if they don't exist.

Script Explanation
The script works in the following steps:

Argument Parsing: Uses argparse to get command-line arguments for paths, file-to-folder mappings, and the logging level.

Directory Iteration: Iterates through files in the specified downloads_path.

ZIP File Identification: Identifies ZIP files based on the filename prefix ("DataFiles-") and extension (".zip").

Extraction: Extracts the contents of each ZIP file to a temporary subdirectory within extract_base_path.

Creation Date Retrieval: Gets the creation dates of the CSV files from the ZIP file metadata using zipfile.ZipFile.

Renaming: Renames the CSV files using the format [original_prefix]_[creation_date].csv. Handles potential file name collisions.

Moving: Moves the renamed CSV files to their designated output folders based on the prefixes defined in the -f argument.

Cleanup: Deletes the original ZIP file and the temporary extraction directory.

Logging: Logs all actions and errors to the console based on the specified logging level.

Error Handling
The script includes several error handling mechanisms:

ZIP File Errors: Catches exceptions during ZIP file reading and extraction.

Missing Creation Dates: Logs a warning if a CSV file's creation date cannot be determined.

Missing Destination Folders: Creates the destination folder if it does not exist.

Invalid -f Argument Format: Checks for errors in the format of the -f argument.

Cleanup Errors: Catches exceptions during the cleanup process.

This README provides a complete guide to using and understanding the csv_archiver_workflow.py script. It covers requirements, usage examples, a detailed explanation of how the script works, and information about error handling. It's well-formatted for GitHub and ready to be used in your repository.
