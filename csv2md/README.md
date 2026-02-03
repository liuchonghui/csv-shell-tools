# csv2md
A lightweight Bash script that converts standard CSV files into well-formatted, aligned Markdown tables. It preserves CSV headers, auto-adapts to column counts, and handles edge cases like spaces/special characters in fields and absolute/relative file paths.

## 📋 Features
- **Seamless CSV to Markdown Conversion**: Transforms CSV files into standard Markdown table format
- **Header Preservation**: Uses the first row of CSV as Markdown table header
- **Auto-Aligned Separator**: Generates proper Markdown table separator lines (`| --- | --- |`) matching CSV column count
- **Robust Field Handling**:
  - Cleans leading/trailing spaces from CSV fields automatically
  - Converts `null` values to empty strings for cleaner output
  - Supports spaces and special characters in CSV fields
- **Flexible Path Support**: Works with both relative and absolute file paths
- **User-Friendly Output**: Provides clear completion messages with file location and row count

## 🛠 Prerequisites
- Unix-like operating system (Linux, macOS, BSD)
- Bash shell (version 3.0+ compatible)
- Standard Unix utilities: `awk`, `mktemp`, `wc`, `dirname`, `basename`, `realpath` (pre-installed on most systems)

## 🚀 Installation
1. Download the script:
   ```bash
   curl -O https://raw.githubusercontent.com/your-username/your-repo/main/csv2md
   ```
2. Make the script executable:
   ```bash
   chmod +x csv2md
   ```
3. (Optional) Install to system PATH for global access:
   ```bash
   sudo mv csv2md /usr/local/bin/
   ```

## 📖 Usage
### Basic Syntax
```bash
csv2md <target_csv_file_path>
```

### Command Arguments
| Argument | Description |
|----------|-------------|
| `<target_csv_file_path>` | Path to the CSV file to convert (relative or absolute path required) |

### Examples
```bash
# Convert CSV file with relative path
./csv2md test.csv

# Convert CSV file with absolute path
./csv2md /tmp/sales_data.csv

# If installed to PATH
csv2md ~/documents/employee_records.csv
```

## 📁 Output Details
### File Naming & Location
- The Markdown output file is created in the **same directory** as the input CSV file
- Naming convention: `[original_filename].md` (e.g., `test.csv` → `test.md`)
- The script automatically removes the `.csv` extension to avoid double extensions (no `test.csv.md`)

### Output Format
The generated Markdown table follows standard GitHub-flavored Markdown format:
```markdown
| Header1 | Header2 | Header3 |
| --- | --- | --- |
| Value1 | Value2 | Value3 |
| Value4 | Value5 | Value6 |
```

### Completion Message
After successful conversion, the script outputs:
```
Completed. Total data rows in Markdown table: 42
Result file: /home/user/documents/test.md
```
- `Total data rows`: Number of actual data rows (excludes header and separator rows)
- `Result file`: Absolute path to the generated Markdown file

## 🧹 Data Processing Rules
1. **Header Row**: First row of CSV is always treated as the table header
2. **Field Cleaning**: Leading/trailing whitespace is removed from all fields
3. **Null Handling**: Explicit `null` values in CSV are converted to empty strings
4. **Empty Fields**: Preserved as empty cells in the Markdown table
5. **Column Count**: Automatically detects and adapts to the column count from the CSV header row

## ⚠️ Error Handling
The script includes error checking for common issues:
- Missing input file parameter (shows usage instructions)
- Non-existent input file or non-regular file (e.g., directory instead of file)
- Failed temporary file creation (critical operation failure)
- Empty CSV file (shows warning and exits gracefully)

## 🐞 Known Limitations
- **Delimiter**: Only supports comma (`,`) as CSV delimiter (does not handle custom delimiters)
- **Quoted Fields**: Does not support CSV fields with quoted commas (e.g., `"Doe, John",45,NY` will split into extra columns)
- **Encoding**: Best with UTF-8 encoded CSV files (may have issues with other encodings like GB2312)
- **Large Files**: May have performance limitations with extremely large CSV files (100k+ rows)

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 💡 Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/improve-conversion`)
3. Commit your changes (`git commit -m 'Add support for quoted CSV fields'`)
4. Push to the branch (`git push origin feature/improve-conversion`)
5. Open a Pull Request

