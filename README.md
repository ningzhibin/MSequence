# Thermo Xcalibur CSV Generator

A web-based application to generate CSV template files for importing into Thermo Xcalibur for MS analysis. This tool converts 96-well or 384-well plate layouts into the required CSV format for Xcalibur sequence import.

## Features

- **Single HTML file**: No installation required, works directly in any modern web browser
- **Dual input methods**: Choose between uploading a file or pasting layout data directly
- **Flexible File Name Components**: Build file names from multiple components:
  - Service name (default: "Service")
  - Date (default: current date in YYYYMMDD format, selectable via date picker)
  - Project name (default: "project")
  - Plate ID (default: "Plate1")
  - Each component can be included/excluded via checkbox
- **Customizable parameters**: Configure path, instrument method, position prefix, and injection volume
- **Preview**: Preview the generated CSV before downloading
- **Automatic download**: Generated CSV file downloads automatically

## Usage

1. Open `index.html` in a web browser
2. Choose your input method:
   - **Upload File**: Click "Upload File" and select a TSV or CSV file
   - **Paste Data**: Click "Paste Data" and paste your layout directly into the textarea
3. Configure the file name components (all checked by default):
   - **Service**: Service name (default: "Service")
   - **Date**: Select date from date picker (default: today's date, formatted as YYYYMMDD)
   - **Project**: Project name (default: "project")
   - **Plate ID**: Plate identifier (default: "Plate1")
   - Uncheck any component to exclude it from file names
4. Fill in the other required fields:
   - **Position Prefix**: Prefix for well positions (e.g., `B:` for positions like `B:A1`, `B:B1`)
   - **Path**: File path for the output directory (e.g., `D:\XU_20251101_P04\`)
   - **Instrument Method**: Path to the instrument method file
   - **Injection Volume**: Default injection volume (default: 1)
4. Click "Generate CSV"
5. The CSV file will be automatically downloaded

## Input File Format

The layout file should be a TSV or CSV file with:
- First row: Column numbers (1, 2, 3, ...)
  - 96-well plate: 12 columns (1-12)
  - 384-well plate: 24 columns (1-24)
- First column: Row letters
  - 96-well plate: 8 rows (A-H)
  - 384-well plate: 16 rows (A-P)
- Remaining cells: Sample names (blank cells indicate empty wells)

The application automatically detects the plate format based on the number of columns in the header row.

Example (96-well):
```
	1	2	3	4	...
A	WT1_I_A	WT1_I_B	WT1_I_C	WT2_I_A	...
B	WT1_II_A	WT1_II_B	WT1_II_C	WT2_II_A	...
...
```

Example (384-well):
```
	1	2	3	4	...	24
A	WT1_I_A	WT1_I_B	WT1_I_C	WT2_I_A	...	WT12_I_A
B	WT1_II_A	WT1_II_B	WT1_II_C	WT2_II_A	...	WT12_II_A
...
P	WT1_XVI_A	WT1_XVI_B	WT1_XVI_C	WT2_XVI_A	...	WT12_XVI_A
```

## Output Format

The generated CSV file follows the Xcalibur format:
- First line: `Bracket Type=4`
- Header row: `File Name,Path,Instrument Method,Position,Inj Vol`
- Data rows: One row per non-empty well in the layout

Example output (with default file name components):
```csv
Bracket Type=4,,,,
File Name,Path,Instrument Method,Position,Inj Vol
Service_20260126_project_Plate1_WT1_I_A,D:\XU_20251101_P04\,C:\Xcalibur\methods\...,B:A1,1
Service_20260126_project_Plate1_WT1_I_B,D:\XU_20251101_P04\,C:\Xcalibur\methods\...,B:B1,1
...
```

The file name format is: `[Service]_[Date]_[Project]_[PlateID]_[SampleName]` where each component can be customized or excluded.

## File Structure

- `index.html` - Main application file (single HTML file with embedded CSS and JavaScript)
- `example_layout.txt` - Example input layout file
- `Example_sequence.csv` - Example output CSV file

## Browser Compatibility

Works in all modern browsers that support:
- FileReader API
- Blob API
- ES6 JavaScript features

Tested on:
- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)

## Deployment

To host on GitHub Pages:
1. Upload `index.html` to your GitHub repository
2. Enable GitHub Pages in repository settings
3. Access via: `https://yourusername.github.io/repository-name/index.html`

Alternatively, you can host it on any web server or use it locally by opening the HTML file directly in your browser.

## Version History

See [CHANGELOG.md](CHANGELOG.md) for detailed version history.

## License

This tool is provided as-is for laboratory use.
