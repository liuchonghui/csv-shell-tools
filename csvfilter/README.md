# csvfilter
A powerful Bash script for filtering rows in CSV files based on specified column, operator, and value. It preserves the CSV header row and outputs results to a new file with a consistent naming convention, supporting both string and numeric comparisons with multiple operators.

## 📋 Features
- **Flexible Filtering**: Supports 8 common comparison operators for both strings and numbers
- **Header Preservation**: Always keeps the first row (header) of the original CSV file
- **String Handling**: 
  - Case-insensitive contains/does not contain checks
  - Support for spaces in string values (with proper quoting)
  - Automatic cleaning of quoted CSV fields
- **Numeric Handling**: Precise comparisons for integers and floating-point numbers
- **User-Friendly**: Clear error messages, detailed help documentation, and informative completion output
- **Consistent Output**: Results saved to `[original_filename].csvfilter.csv` in the same directory
- **Robust Validation**: Comprehensive checks for valid parameters, file existence, and data types

## 🛠 Prerequisites
- Unix-like operating system (Linux, macOS, BSD)
- Bash shell (version 3.0+ compatible)
- Standard Unix utilities: `awk`, `dirname`, `basename` (pre-installed on most systems)

## 🚀 Installation
1. Download the script:
   ```bash
   curl -O https://github.com/liuchonghui/csv-shell-tools/raw/refs/heads/main/csvfilter/csvfilter
   ```
2. Make the script executable:
   ```bash
   chmod +x csvfilter
   ```
3. (Optional) Install to system PATH for global access:
   ```bash
   sudo mv csvfilter /usr/local/bin/
   ```

## 📖 Usage
### Basic Syntax
```bash
csvfilter --col=column_number --filter=operator --value=match_value target_csv_file
```

### Required Parameters
| Parameter | Description |
|-----------|-------------|
| `--col=N` | Column number to filter (positive integer, 1-based index) |
| `--filter=OP` | Comparison operator (see supported operators below) |
| `--value=VAL` | Value to match against:<br>- **Numbers**: Direct value (e.g., `--value=1000`)<br>- **Strings**: Quoted value (e.g., `--value="jenkins ci"`) |
| `target_csv_file` | Path to CSV file (relative or absolute) |

### Supported Operators
| Operator | Description | Type | Case Sensitivity |
|----------|-------------|------|------------------|
| `EQ` | Equal | String/Numeric | Case-sensitive (string) |
| `NEQ` | Not Equal | String/Numeric | Case-sensitive (string) |
| `FD` | Contains | String | Case-insensitive |
| `NFD` | Does Not Contain | String | Case-insensitive |
| `GT` | Greater Than | Numeric | N/A |
| `GTE` | Greater Than or Equal | Numeric | N/A |
| `LT` | Less Than | Numeric | N/A |
| `LTE` | Less Than or Equal | Numeric | N/A |

### Examples
```bash
# Filter rows where column 3 contains "jenkins ci" (case-insensitive)
./csvfilter --col=3 --filter=FD --value="jenkins ci" data.csv

# Filter rows where column 5 is greater than 1000 (numeric comparison)
./csvfilter --col=5 --filter=GT --value=1000 sales.csv

# Filter rows where column 4 equals "right now" (exact string match)
./csvfilter --col=4 --filter=EQ --value="right now" log.csv

# Filter rows where column 7 is less than or equal to 500.50
./csvfilter --col=7 --filter=LTE --value=500.50 metrics.csv

# Filter rows where column 2 does NOT contain "error"
./csvfilter --col=2 --filter=NFD --value="error" application.log.csv
```

### Help Documentation
```bash
./csvfilter --help
# or
./csvfilter -h
```

## 📁 Output Details
### File Naming & Location
- Output file is created in the **same directory** as the input CSV
- Naming convention: `[original_filename].csvfilter.csv`
  - Example: `data.csv` → `data.csvfilter.csv`

### Completion Output
After successful execution, the script displays:
```
处理完成！
源文件: ./data.csv
输出文件: ./data.csvfilter.csv
条件匹配数据42行
筛选条件: 第3列 包含（忽略大小写）'jenkins ci'
```
- Clear summary of filtering criteria
- Number of matching data rows (excludes header row)
- Full paths to source and output files

## 🧹 Data Processing Rules
1. **Header Row**: Always preserved and written to output file first
2. **Field Cleaning**: Automatic removal of surrounding quotes from CSV fields
3. **String Comparison**:
   - `EQ`/`NEQ`: Exact, case-sensitive matches
   - `FD`/`NFD`: Case-insensitive substring checks
4. **Numeric Comparison**:
   - Automatically converts values to numeric type
   - Supports positive/negative numbers and decimals
   - Invalid numeric values in CSV fields are treated as `0`
5. **Empty Values**: Handled gracefully (empty string for string ops, 0 for numeric ops)

## ⚠️ Error Handling
The script validates all inputs and provides clear error messages for:
- Missing required parameters (`--col`, `--filter`, `--value`)
- Invalid column numbers (non-integers, zero, negative values)
- Unsupported filter operators
- Non-numeric values with numeric operators
- Non-existent target files
- Non-CSV files (missing .csv extension)
- File processing errors

## 🐞 Known Limitations
- **Delimiter**: Only supports comma (`,`) as CSV delimiter
- **Quoted Fields**: Does not handle quoted fields containing commas (e.g., `"Doe, John",45` splits into extra columns)
- **Encoding**: Best with UTF-8 encoded CSV files
- **Performance**: May be slow with extremely large CSV files (100k+ rows)
- **Whitespace**: Leading/trailing spaces in CSV fields affect exact matches (`EQ`/`NEQ`)

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 💡 Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/add-regex-support`)
3. Commit your changes (`git commit -m 'Add regex support for FD/NFD operators'`)
4. Push to the branch (`git push origin feature/add-regex-support`)
5. Open a Pull Request

