# Bash Backup Script

A simple Bash script that automates the backup of recently modified files from a source directory to a destination directory using compressed `.tar.gz` archives.

## Features

- Accepts source and destination directories as command-line arguments.
- Checks whether the provided directories exist.
- Identifies regular files modified within the last 24 hours.
- Creates a compressed `.tar.gz` archive.
- Generates a unique backup filename using the current Unix timestamp.
- Handles filenames containing spaces.
- Prevents the destination directory from being inside the source directory.
- Handles empty directories and backup errors.

## Requirements

- Linux operating system.
- Bash shell.
- GNU `tar`.
- GNU `stat`.
- `realpath`.

## Project Structure

```text
bash-backup-script/
├── backup.sh
└── README.md
```

## Usage

### 1. Clone the repository

```bash
git clone <repository-url>
cd bash-backup-script
```

### 2. Give the script execution permissions

```bash
chmod +x backup.sh
```

### 3. Run the script

```bash
./backup.sh /path/to/source /path/to/destination
```

**Example:**

```bash
./backup.sh /home/user/documents /home/user/backups
```

The script will identify files modified within the last 24 hours and create a compressed archive in the destination directory.

## Backup Output

The generated archive follows this naming format:

```text
backup-<timestamp>.tar.gz
```

Example:

```text
backup-1793520000.tar.gz
```

## Testing

You can test the script using temporary directories:

```bash
mkdir -p ~/backup_test/source
mkdir -p ~/backup_test/destination

echo "Hello World" > ~/backup_test/source/file1.txt
echo "Testing spaces" > ~/backup_test/source/"my file.txt"

touch -d "2 days ago" ~/backup_test/source/old_file.txt

./backup.sh ~/backup_test/source ~/backup_test/destination
```

Verify the generated archive:

```bash
ls -lh ~/backup_test/destination
```

Inspect its contents:

```bash
tar -tzvf ~/backup_test/destination/backup-*.tar.gz
```

Files modified within the last 24 hours should be included, while older files should be excluded.

## Limitations

- Only regular files directly inside the source directory are processed; subdirectories are not searched recursively.
- File selection is based on modification time, not creation time.
- The script runs manually and does not include automatic scheduling.
- GNU/Linux utilities are required.

## Possible Improvements

- Add recursive directory backup support.
- Schedule automatic backups using Cron.
- Add backup logging.
- Implement backup retention to remove old archives.
- Add support for excluding specific files or directories.

## Author

Abdulrahman Ahmed

