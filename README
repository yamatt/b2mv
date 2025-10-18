# b2mv

A simple command-line utility for moving and renaming files and directories in Backblaze B2 cloud storage.

## Description

`b2mv` provides a convenient way to move or rename files and entire directories within Backblaze B2 buckets using server-side operations. It performs server-side copy followed by deletion of the original files, similar to how the `mv` command works in Unix-like systems.

## Features

- **Single file operations**: Move or rename individual files
- **Directory operations**: Move entire directories with all their contents
- **Server-side operations**: Efficient transfers without downloading/uploading
- **Progress tracking**: Shows progress when moving multiple files
- **Error handling**: Robust error handling with clear messages

## Prerequisites

- [Backblaze B2 CLI](https://www.backblaze.com/b2/docs/tool_installation.html) must be installed and configured
- Valid B2 account credentials configured via `b2 authorize-account`

## Installation

1. Make the script executable:

   ```bash
   chmod +x b2mv
   ```

2. Optionally, move it to a directory in your PATH:
   ```bash
   sudo mv b2mv /usr/local/bin/
   ```

## Usage

```bash
b2mv <bucket> <old-path> <new-path>
```

### Parameters

- `bucket`: The name of the B2 bucket containing the files
- `old-path`: The current path/name of the file or directory in the bucket
- `new-path`: The new path/name for the file or directory in the same bucket

**Important**: Use trailing slashes (`/`) for directory operations.

### Examples

**Rename a single file:**

```bash
b2mv my-bucket old-name.txt new-name.txt
```

**Move a file to a different directory within the same bucket:**

```bash
b2mv my-bucket file.txt archive/file.txt
```

**Move an entire directory:**

```bash
b2mv my-bucket old-directory/ new-directory/
```

**Move a directory to a new location:**

```bash
b2mv my-bucket documents/ archive/2023/documents/
```

**Rename and move simultaneously:**

```bash
b2mv my-bucket documents/report.pdf backups/2023/annual-report.pdf
```

**Reorganize directory structure:**

```bash
b2mv my-bucket temp-uploads/ processed/batch-2023-10/
```

## How It Works

### Single File Operations

For single files, the script performs two operations:

1. **Server-side copy**: Creates a copy of the file at the new location using `b2 file server-side-copy`
2. **Delete original**: Removes the original file using `b2 rm`

### Directory Operations

For directories (indicated by trailing slash), the script:

1. **Lists all files**: Uses `b2 ls --recursive` to find all files in the source directory
2. **Processes each file**: Iterates through each file and performs the move operation
3. **Progress tracking**: Shows current progress (file X of Y)
4. **Preserves structure**: Maintains the relative directory structure in the destination

## Directory Operation Details

- **Detection**: Directory operations are detected by a trailing slash (`/`) in the source path
- **Recursive**: All files and subdirectories are moved recursively
- **Structure preservation**: The relative path structure is maintained in the destination
- **Progress feedback**: Shows which file is being processed and overall progress
- **Error handling**: If any file fails to move, the operation stops with an error

## Error Handling

The script includes comprehensive error handling to:

- Validate that exactly 3 arguments are provided
- Exit immediately if any command fails (due to `set -euo pipefail`)
- Handle copy failures without removing the original file
- Provide clear error messages for debugging
- Track progress and show which operations succeed or fail

## Performance Considerations

- **Server-side operations**: All copy operations happen on Backblaze servers
- **No data transfer**: Files are not downloaded/uploaded, saving bandwidth and time
- **Sequential processing**: Files are moved one at a time to avoid overwhelming the API
- **Data transfer costs**: Server-side copy operations within the same region are typically free

## Notes

- **Atomic operation**: If a copy fails, the original file remains untouched
- **File metadata**: Server-side copy preserves file metadata including timestamps and custom headers
- **Directory syntax**: Always use trailing slashes for directory operations
- **Large directories**: For very large directories, the operation may take some time but will show progress

## License

See the LICENSE file for details.

## Contributing

Feel free to submit issues and pull requests to improve this utility.
