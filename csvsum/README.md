# csvsum
A lightweight and robust Shell script tool designed to calculate cumulative sums for specified columns (or all columns) in CSV files. It features enhanced compatibility with messy CSV formats (e.g., BOM headers, trailing spaces, invisible characters) and optimized output formatting for easy parsing with awk.

## 📋 Features
- **Flexible Column Selection**: Calculate sums for single columns, multiple columns (comma-separated), or all columns in a CSV file
- **Robust CSV Compatibility**:
  - Handles UTF-8 BOM headers automatically
  - Cleans invisible characters, leading/trailing spaces in column names and values
  - Supports floating-point numbers, positive/negative values (e.g., `-123.45`, `+67.89`)
  - Validates CSV file existence, readability, and non-empty content
- **Informative Output**: Prints column number, column name, number of data rows, and cumulative sum in a structured format
- **User-Friendly**: Clear error messages and usage instructions for easy troubleshooting

## 🛠 Prerequisites
- Unix-like operating system (Linux, macOS, BSD)
- Bash shell (version 4.0+ recommended)
- Standard Unix utilities: `awk`, `sed`, `head`, `tail`, `wc`, `seq`, `tr` (pre-installed on most systems)

## 🚀 Installation
1. Download the script:
   ```bash
   curl -O https://raw.githubusercontent.com/your-username/your-repo/main/csvsum
   ```
2. Make the script executable:
   ```bash
   chmod +x csvsum
   ```
3. (Optional) Move to system PATH for global access:
   ```bash
   sudo mv csvsum /usr/local/bin/
   ```

## 📖 Usage
### Basic Syntax
```bash
csvsum [--col=column_number[,column_number...]|--col=all] csv_file_path
```

### Command Options
| Option | Description |
|--------|-------------|
| `--col=all` | Calculate sum for all columns (default behavior if no `--col` specified) |
| `--col=N` | Calculate sum for the Nth column (column number starts from 1) |
| `--col=N1,N2,N3` | Calculate sums for multiple columns (comma-separated, no spaces) |

### Examples
```bash
# Calculate sum for column 9
csvsum --col=9 data.csv

# Calculate sums for columns 9, 10, 11
csvsum --col=9,10,11 data.csv

# Calculate sum for all columns (shortcut - omit --col parameter)
csvsum --col=all data.csv
csvsum data.csv  # Equivalent to above
```

## 📝 Output Format
The script outputs results in a consistent, human-readable format (easily parsable with awk):
```
第 9 列 Sales 1500 个数据的累加总和为 256890.75
```


### Output Explanation
| Component | Description |
|-----------|-------------|
| `Column 9` | The column number being calculated (1-based index) |
| `Sales` | Column name from CSV header (or "Unnamed Column" if empty) |
| `1500 data rows` | Number of actual data rows (total rows - header row) |
| `total sum: 256890.75` | Cumulative sum of all valid numeric values in the column |

## ⚠️ Error Handling
The script includes comprehensive error checking for common issues:
- Missing file path parameter
- Non-existent/inaccessible CSV files
- Invalid file type (non-CSV extension)
- Empty CSV files
- Invalid column numbers (non-integers, zero, negative values)
- Malformed `--col` parameter format
- CSV files with no valid columns

## 🧹 Data Handling Rules
- Empty values or non-numeric values (letters, symbols) are treated as `0`
- Floating-point precision is preserved (uses `0.0` as initial sum value)
- Trailing commas in CSV rows are ignored (no empty columns counted)
- Leading/trailing spaces in column values are automatically stripped

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🐞 Known Issues & Limitations
- Does not support CSV files with quoted fields containing commas (e.g., `"Doe, John",45,NY`)
- Assumes comma (`,`) as the only delimiter (does not support custom delimiters)
- Large CSV files (100k+ rows) may have performance limitations (native shell tools are slower than specialized CSV parsers)

## 💡 Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request


