# md2csv
A lightweight Bash script that converts standard Markdown tables into well-formatted CSV files. It preserves table headers, auto-adapts to different Markdown table alignment styles, and handles edge cases like spaces/special characters in table cells and absolute/relative file paths.

## 📋 Features
- **Seamless Markdown to CSV Conversion**: Transforms Markdown tables into standard comma-separated value (CSV) format
- **Header Preservation**: Automatically detects and preserves the Markdown table header row as the CSV title row
- **Alignment Compatibility**: Works with all Markdown table alignment styles (`|---|`, `|:-:|`, `|--|`, `|-|`)
- **Robust Cell Handling**:
  - Cleans leading/trailing spaces from table cells automatically
  - Preserves special characters and spaces within table cells
  - Skips empty lines in the input Markdown file
- **Flexible Path Support**: Works with both relative and absolute file paths for input files
- **User-Friendly Output**: Provides clear completion messages with file location and row count statistics
- **Temporary File Safety**: Uses secure temporary files to handle conversion without memory issues

## 🛠 Prerequisites
- Unix-like operating system (Linux, macOS, BSD)
- Bash shell (version 3.0+ compatible)
- Standard Unix utilities: `awk`, `mktemp`, `wc`, `dirname`, `basename`, `realpath`, `cp`, `rm` (pre-installed on most systems)

## 🚀 Installation
1. Download the script:
   ```bash
   curl -O https://raw.githubusercontent.com/your-username/your-repo/main/md2csv
   ```
2. Make the script executable:
   ```bash
   chmod +x md2csv
   ```
3. (Optional) Install to system PATH for global access:
   ```bash
   sudo mv md2csv /usr/local/bin/
   ```

## 📖 Usage
### Basic Syntax
```bash
md2csv <target_md_file_path>
```

### Command Arguments
| Argument | Description |
|----------|-------------|
| `<target_md_file_path>` | Path to the Markdown file containing tables (relative or absolute path required) |
| `-h`/`--help` | (Optional) Show detailed help documentation (parses script comments) |

### Examples
```bash
# Convert Markdown file with relative path
./md2csv test.md

# Convert Markdown file with absolute path
./md2csv /tmp/report_data.md

# If installed to PATH
md2csv ~/documents/meeting_notes.md
```

## 📁 Output Details
### File Naming & Location
- The CSV output file is created in the **same directory** as the input Markdown file
- Naming convention: `[original_filename].csv` (e.g., `test.md` → `test.csv`)
- The script automatically removes the `.md` extension to avoid double extensions (no `test.md.csv`)

### Supported Markdown Table Formats
The script handles all common Markdown table styles:
```markdown
# Basic table
| Name | Age | City |
|------|-----|------|
| John | 30  | NYC  |
| Jane | 28  | LA   |

# Table with alignment
| Product | Price | In Stock |
|:-------|------:|:-------:|
| Laptop | 999.99 | Yes     |
| Phone  | 699.99 | No      |
```

### Completion Message
After successful conversion, the script outputs:
```
Completed. Total data rows in CSV file: 2
Result file: /home/user/documents/test.csv
```
- `Total data rows`: Number of actual data rows (excludes header row)
- `Result file`: Absolute path to the generated CSV file

## 🧹 Data Processing Rules
1. **Header Detection**: Identifies the header row as the line immediately preceding the separator line (`|---|`)
2. **Separator Handling**: Ignores alignment characters (`:`) in separator lines
3. **Cell Cleaning**: Leading/trailing whitespace is removed from all table cells
4. **Empty Line Skipping**: Automatically skips empty lines in the input file
5. **Column Count**: Automatically detects and adapts to the column count from the Markdown table
6. **Special Characters**: Preserves special characters (e.g., commas, hyphens, underscores) within cells

## ⚠️ Error Handling
The script includes comprehensive error checking for common issues:
- Missing input file parameter (shows clear usage instructions)
- Non-existent input file or non-regular file (e.g., directory instead of file)
- Failed temporary file creation (critical operation failure)
- No valid Markdown table content found (shows warning and exits gracefully)

## 🐞 Known Limitations
- **Single Table Only**: Best suited for Markdown files with a single table (may process only the first table if multiple exist)
- **Table Format**: Requires standard Markdown table syntax with pipe (`|`) delimiters (does not support HTML tables)
- **Nested Pipes**: Does not handle pipe characters (`|`) within quoted table cells (e.g., `"Doe | John"` will split into multiple columns)
- **Encoding**: Best with UTF-8 encoded Markdown files (may have issues with other encodings like GB2312)
- **Large Files**: May have performance limitations with extremely large Markdown files (100k+ lines)

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 💡 Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/multi-table-support`)
3. Commit your changes (`git commit -m 'Add support for multiple tables in one file'`)
4. Push to the branch (`git push origin feature/multi-table-support`)
5. Open a Pull Request


