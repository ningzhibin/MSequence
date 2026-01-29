# Changelog

All notable changes to this project will be documented in this file.

## [0.04] - 2026-01-26

### Added
- **384-well plate support**: Application now supports both 96-well and 384-well plate formats
  - Auto-detects plate format based on number of columns in header row
  - Supports 96-well plates: 12 columns × 8 rows (A-H)
  - Supports 384-well plates: 24 columns × 16 rows (A-P)
  - Updated help text and documentation to reflect both formats

### Changed
- Parsing logic updated to handle up to 24 columns (previously limited to 12)
- Row detection now supports rows A-P (previously limited to A-H)

## [0.03] - 2026-01-26

### Added
- **Dual input methods**: Users can now choose between uploading a file or pasting layout data directly
  - Toggle between "Upload File" and "Paste Data" modes
  - Paste method includes a textarea with example placeholder text
  - Both methods use the same parsing logic for consistency

## [0.02] - 2026-01-26

### Added
- Enhanced File Name Prefix section with multiple configurable components:
  - **Service field**: Text input with default value "Service" and checkbox to include/exclude
  - **Date field**: Date picker with default value set to current system date (YYYYMMDD format), checkbox to include/exclude
  - **Project field**: Text input with default value "project" and checkbox to include/exclude
  - **Plate ID field**: Text input with default value "Plate1" and checkbox to include/exclude
- File name components are joined with underscores, then joined with sample name from layout
- Real-time file name preview showing how components combine with sample name
- Improved UI with dedicated section for file name components with visual grouping
- Date field automatically formats selected date as YYYYMMDD in the output

### Changed
- File Name Prefix is now built dynamically from multiple components instead of single text input
- Improved form layout with better organization of related fields

## [0.01] - 2026-01-26

### Added
- Initial release of Thermo Xcalibur CSV Generator
- Single HTML file application with embedded CSS and JavaScript
- File upload functionality for TSV/CSV layout files
- Support for 96-well plate layout parsing (12 columns × 8 rows A-H)
- CSV generation with Xcalibur-compatible format:
  - Bracket Type=4 header
  - File Name column (prefix + sample name)
  - Path column (user-defined)
  - Instrument Method column (user-defined)
  - Position column (prefix + well position, e.g., B:A1)
  - Inj Vol column (user-defined, default: 1)
- Preview functionality showing first 10 rows of generated CSV
- Automatic CSV download
- Modern, responsive UI with gradient design
- Form validation and error handling
- README.md documentation
- CHANGELOG.md version tracking

### Technical Details
- Pure JavaScript implementation (no external dependencies)
- Client-side file processing (no server required)
- Supports both tab-separated (TSV) and comma-separated (CSV) input files
- Handles empty cells (skips blank wells)
- Generates well positions in format: RowLetter + ColumnNumber (e.g., A1, B12)
