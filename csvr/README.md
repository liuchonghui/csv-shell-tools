# csvr
A lightweight and efficient Bash script to reverse the data rows of CSV files while preserving the header row. Ideal for quickly reordering CSV data with the header row intact, producing a new file with a consistent naming convention.

## 📋 Features
- **Header Preservation**: Maintains the first row (header) of the original CSV file unchanged
- **Data Row Reversal**: Reverses all data rows (rows 2 through end) in the CSV file
- **Path Flexibility**: Works with both relative and absolute file paths
- **Robust Validation**:
  - Checks for file existence and valid file type (regular file)
  - Verifies CSV file extension (.csv)
  - Validates temporary file creation permissions
- **Memory Efficient**: Uses temporary files to handle large CSV files without memory overflow
- **Consistent Output**: Generates output file with `.r.csv` suffix in the same directory
- **Informative Feedback**: Provides clear row count statistics for input and output files

## 🛠 Prerequisites
- Unix-like operating system (Linux, macOS, BSD)
- Bash shell (version 3.0+ compatible)
- Standard Unix utilities: `head`, `tail`, `tac`, `wc`, `dirname`, `basename`, `mktemp`, `cat`, `rm` (pre-installed on most systems)
  - Note: `tac` is part of GNU coreutils (pre-installed on most Linux distributions; for macOS, install via `brew install coreutils` and use `gtac` instead)

## 🚀 Installation
1. Download the script:
   ```bash
   curl -O https://raw.githubusercontent.com/your-username/your-repo/main/csvr
   ```
2. Make the script executable:
   ```bash
   chmod +x csvr
   ```
3. (Optional) Install to system PATH for global access:
   ```bash
   sudo mv csvr /usr/local/bin/
   ```

### macOS Note
If `tac` is not available on your macOS system:
```bash
# Install GNU coreutils
brew install coreutils
# Modify the script to use gtac (line 63)
sed -i '' 's/tac/gtac/' csvr
```

## 📖 Usage
### Basic Syntax
```bash
csvr <target_csv_file>
```

### Command Arguments
| Argument | Description |
|----------|-------------|
| `<target_csv_file>` | Path to the CSV file to process (relative or absolute path) |
| `-h`, `--help` | Show detailed help documentation |

### Examples
```bash
# Process CSV file with relative path
./csvr temp.csv

# Process CSV file with absolute path
./csvr /data/analytics/sales_data.csv

# View help documentation
./csvr --help
```

## 📁 Output Details
### File Naming & Location
- The output file is created in the **same directory** as the input CSV file
- Naming convention: `[original_filename].r.csv`
  - Example: `temp.csv` → `temp.r.csv`
  - Example: `sales_data.csv` → `sales_data.r.csv`

### Output Statistics
After successful execution, the script displays concise row count statistics:
```
Total rows in input:    1001 (header: 1, data: 1000)
Total rows in output:   1001 (header: 1, reversed data: 1000)
```
- `Total rows in input`: Total number of rows in the original file (header + data)
- `Total rows in output`: Total number of rows in the reversed file (unchanged count)
- `data`: Number of actual data rows (total rows - 1 header row)

## 🧹 Data Processing Rules
1. **Header Row**: Always preserved as the first row of the output file (unchanged)
2. **Data Rows**: Rows 2 through end of the original file are reversed in order:
   - Original row 2 → Output row last
   - Original row last → Output row 2
3. **File Content**: All original content (special characters, spaces, commas) is preserved exactly
4. **Large Files**: Uses temporary files instead of in-memory processing to handle large CSV files efficiently

## ⚠️ Error Handling
The script includes comprehensive error checking for common issues:
- Missing input file parameter (shows usage instructions)
- Non-existent input file or non-regular file (e.g., directory instead of file)
- Non-CSV file (missing .csv extension)
- Failed temporary file creation (permission denied)

## 🐞 Known Limitations
- **Delimiter**: Only supports standard comma (`,`) delimited CSV files
- **macOS Compatibility**: Requires GNU coreutils (`tac`/`gtac`) for row reversal
- **Encoding**: Best with UTF-8 encoded CSV files (may have issues with other encodings)
- **Empty Files**: Will fail if input CSV file contains only a header row (no data rows)

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 💡 Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/add-encoding-support`)
3. Commit your changes (`git commit -m 'Add support for different CSV encodings'`)
4. Push to the branch (`git push origin feature/add-encoding-support`)
5. Open a Pull Request


