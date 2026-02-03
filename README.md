# csv-shell-tools
A collection of lightweight, robust, and user-friendly Bash shell scripts for processing CSV files. These tools are designed to handle common CSV operations with minimal dependencies, focusing on simplicity, compatibility, and ease of use for both beginners and experienced users.

## 📚 Available Tools
This repository currently includes 5 specialized CSV processing scripts, each with a specific focus:

| Script | Description | Key Features |
|--------|-------------|--------------|
| [`csv2md`](./csv2md) | Convert CSV files to well-formatted Markdown tables | • Preserves CSV headers<br>• Auto-generates aligned separator lines<br>• Cleans leading/trailing spaces from fields<br>• Supports relative/absolute file paths |
| [`csvfilter`](./csvfilter) | Filter CSV rows based on column, operator, and value | • 8 comparison operators (EQ, NEQ, FD, NFD, GT, GTE, LT, LTE)<br>• Supports string (case-insensitive) and numeric comparisons<br>• Preserves header row<br>• Detailed error validation |
| [`csvr`](./csvr) | Reverse CSV data rows while preserving headers | • Maintains header row unchanged<br>• Reverses all data rows (2nd line to end)<br>• Memory-efficient (uses temp files for large CSVs)<br>• Clear row count statistics |
| [`csvsum`](./csvsum) | Calculate cumulative sums for CSV columns | • Supports single/multiple/all columns<br>• Handles UTF-8 BOM headers and invisible characters<br>• Compatible with floating-point numbers<br>• Optimized output for awk parsing |
| [`md2csv`](./md2csv) | Convert Markdown tables to standard CSV files | • Detects and preserves Markdown table headers<br>• Compatible with all Markdown alignment styles<br>• Skips empty lines<br>• Cleans table cell whitespace |

## 🛠 Prerequisites
All scripts share the same minimal system requirements:
- Unix-like operating system (Linux, macOS, BSD)
- Bash shell (version 3.0+ recommended)
- Standard Unix utilities (`awk`, `sed`, `head`, `tail`, `wc`, etc.) – pre-installed on most systems

## 🚀 Installation
### Clone the Repository
```bash
git clone git@github.com:liuchonghui/csv-shell-tools.git
cd csv-shell-tools
```

### Make Scripts Executable
```bash
# Make all scripts executable
chmod +x */*.sh

# Or make individual scripts executable (example)
chmod +x csv2md/csv2md
chmod +x csvfilter/csvfilter
```

### (Optional) Install to System PATH
For global access to all tools:
```bash
# Create a symlink for each script (example)
sudo ln -s "$(pwd)/csv2md/csv2md" /usr/local/bin/
sudo ln -s "$(pwd)/csvfilter/csvfilter" /usr/local/bin/
sudo ln -s "$(pwd)/csvr/csvr" /usr/local/bin/
sudo ln -s "$(pwd)/csvsum/csvsum" /usr/local/bin/
sudo ln -s "$(pwd)/md2csv/md2csv" /usr/local/bin/
```

## 📖 Usage
Each tool has its own detailed documentation:
- For `csv2md`: See [csv2md/README.md](./csv2md/README.md)
- For `csvfilter`: See [csvfilter/README.md](./csvfilter/README.md)
- For `csvr`: See [csvr/README.md](./csvr/README.md)
- For `csvsum`: See [csvsum/README.md](./csvsum/README.md)
- For `md2csv`: See [md2csv/README.md](./md2csv/README.md)

Basic usage pattern for all scripts:
```bash
# Run from repository directory
./<script-directory>/<script-name> [options] <file-path>

# If installed to PATH
<script-name> [options] <file-path>
```

## 📝 Roadmap
This repository is actively maintained and will be expanded with additional CSV processing tools, including (but not limited to):
- CSV column renaming
- CSV row/column deletion
- CSV file merging
- CSV data sorting
- CSV duplicate removal
- CSV format validation

## 🧰 Common Features Across All Tools
- **Robust Error Handling**: Clear, descriptive error messages for invalid inputs
- **Path Flexibility**: Support for both relative and absolute file paths
- **File Validation**: Checks for file existence, readability, and correct file type
- **User-Friendly Output**: Informative completion messages with file paths and statistics
- **Cross-Platform**: Works on Linux, macOS, and BSD systems with minimal adjustments

## 📄 License
All scripts in this repository are licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

## 💡 Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/new-csv-tool`)
3. Commit your changes (`git commit -m 'Add csvsort script for sorting CSV rows'`)
4. Push to the branch (`git push origin feature/new-csv-tool`)
5. Open a Pull Request


