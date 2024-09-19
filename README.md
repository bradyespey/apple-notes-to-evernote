# Apple Notes to Evernote Migration

## Overview

This project automates the migration of Apple Notes into Evernote. It exports notes from Apple Notes into Markdown format, converts them into Evernote's ENEX format, and imports them into Evernote, ensuring that notes, folders, and attachments are preserved.

**Key Features**
- **Export Notes:** Uses the Exporter tool to export Apple Notes to Markdown format.
- **Convert to ENEX:** A custom Python script (built on [md2enex](https://github.com/karloskalcium/md2enex)) converts Markdown files to ENEX, ensuring that all note data, attachments, and folders are correctly migrated.
- **Compare Notes:** Scripts allow you to compare the migrated notes in Evernote with the original Apple Notes to ensure completeness.

---

## Workflow

1. **Clean Notes:** Remove duplicates and clean up note titles with special characters using a script.
2. **Export Apple Notes:** Use the Exporter tool to export Apple Notes to Markdown.
3. **Convert to ENEX:** Run a custom Python script that leverages `md2enex` to convert Markdown files to ENEX format and log any problematic files.
4. **Import to Evernote:** Import the ENEX files into Evernote.
5. **Verify Migration:** Compare the notes in Evernote with the original Apple Notes to ensure nothing was left behind.

---

## Step-by-Step Setup Guide

### Step 1: Clean Up Notes

- Use the `notes_cleanup.applescript` script to remove duplicates and notes with special characters (colons, periods, quotes, and apostrophes).
- Remove note locks and unshare notes if necessary, as these could cause issues during export.

### Step 2: Export Apple Notes to Markdown

#### 2.1 Install Exporter
- Download the Exporter app for Mac from [this link](https://apps.apple.com/us/app/exporter/id1099120373?mt=12).

#### 2.2 Export Notes
- Configure Exporter with the following settings:
  - Name format: Leave blank.
  - Markdown header: `#Title`
  
- Set the destination folder for the exported notes. Example: `/Users/bradyespey/Projects/Notes`.

- Run Exporter and verify that Markdown files and their corresponding attachments are correctly saved.

### Step 3: Convert Markdown Files to ENEX

#### 3.1 Setup the Conversion Script
- Ensure **Python 3.x** is installed and activate a virtual environment:
  ```
  python3 -m venv venv
  source venv/bin/activate
  ```
  
- Install the required dependencies using pip:
  ```
  pip install pypandoc typer lxml
  ```

- The custom `export_markdown_to_enex.py` script wraps around the `md2enex` script and adds enhanced error handling and file logging. Adjust the paths in the script to point to your directories:
  
  - **Source Directory (Markdown files):** `/Users/bradyespey/Projects/Files/Evernote/iCloud`
  - **Output Directory (ENEX files):** `/Users/bradyespey/Projects/Files/Evernote/Converted`

#### 3.2 Run the Conversion
- Run the `export_markdown_to_enex.py` script. This will:
  - Convert the Markdown files into ENEX format.
  - Export any problematic files to a CSV for review.

Example command:
```bash
python export_markdown_to_enex.py
```

### Step 4: Import ENEX Files into Evernote

#### 4.1 Import ENEX Files
- Open Evernote on your Mac.
- Navigate to `File > Import Notes...` and select the generated ENEX files.

#### 4.2 Verify Import
- Ensure that all titles, attachments, and folder structures match what was originally in Apple Notes.

---

## Scripts

The following scripts handle each part of the process:

- **`notes_cleanup.applescript`:** Cleans up notes in Apple Notes before exporting.
- **`export_markdown_to_enex.py`:** Converts Markdown files into ENEX format, logging any problematic files.
- **`markdown_to_enex_comparison.py`:** Compares the Markdown and ENEX files to ensure completeness.
- **`export_notes_info_to_csv.py`:** Exports detailed notes metadata from Apple Notes to CSV for manual review.

Each script is available in this repository and can be customized to suit your environment.

---

### How to Contribute
Feel free to contribute by submitting issues or making pull requests. 

### License
This project is licensed under the MIT License.