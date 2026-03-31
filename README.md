# Filter Credit Card Records — README

A small command-line tool to filter CSV records where the "Information Type Name" column contains "Credit Card" and write results to an Excel (.xlsx) file. The output file is named _output.xlsx and is written to the same folder as the input CSV.

## Contents
- filter_credit_card_to_xlsx.py — main script (Python)
- .github/workflows/build-windows.yml — optional GitHub Actions workflow to build a Windows .exe using PyInstaller (if included)

## Features
- Memory-efficient chunked CSV processing (pandas)
- Preserves CSV parsing for quoted fields and embedded newlines
- Writes matches incrementally to an .xlsx (openpyxl)
- Clears console before run and prints summary: output path, rows processed, matches, discarded, execution time
- Usable interactively or via command-line arguments
- Can be packaged as a Windows executable using PyInstaller (recommended to build on Windows or via CI)


## Requirements

- Python 3.8+ (tested)
- pip packages:
  - pandas
  - openpyxl
- Optional for building an .exe:
  - pyinstaller

## Install dependencies

Locally (run with Python):
pip install pandas openpyxl

To build an exe on Windows:
pip install pandas openpyxl pyinstaller

## Usage (script)

Interactive (prompts for filename):
python filter_credit_card_to_xlsx.py

Direct (supply CSV path):
python filter_credit_card_to_xlsx.py path\to\input.csv

Adjust chunk size for memory/performance:
python filter_credit_card_to_xlsx.py path\to\input.csv --chunksize 100000


#  Troubleshooting

- "Column 'Information Type Name' not found": ensure the CSV header includes that exact column (leading/trailing spaces are tolerated). If your CSV uses different naming, update the script or rename the header.
- Memory issues: reduce --chunksize value.
- Quoted/embedded newlines: script uses pandas which correctly handles quoted fields; ensure CSV is valid.
- Building exe on macOS: PyInstaller on macOS cannot reliably produce Windows executables. Use GitHub Actions or build on Windows
