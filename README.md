# CSV Duplicate Finder

Find exact duplicates and fuzzy name matches in the newest CSV inside a data folder.  
The script standardizes Email and Phone Number, checks exact duplicates on key fields, and also finds likely name duplicates using token sort ratio.

## What this tool does

* picks the most recent CSV from a folder you choose
* cleans Email and Phone Number columns
* finds exact duplicates using Email, Phone Number, Age, and Gender
* finds likely name duplicates with fuzzy matching and writes a small report

## Files in this repo


## Requirements

* Python 3.9 or later
* Packages listed in requirements.txt

Example requirements
pandas==2.2.2
fuzzywuzzy==0.18.0
python-Levenshtein==0.25.1


`python-Levenshtein` is optional but makes fuzzy matching faster.  
If you prefer RapidFuzz, you can swap it yourself later.

## Setup

1. create a virtual environment
      python3 -m venv .venv
2. activate it
      source .venv/bin/activate 
3. install dependencies
      python -m pip install -r requirements.txt

markdown
Copy
Edit


## Usage

1. put one or more CSV files in `applications_data`  
the newest file will be used automatically

2. open `dedupe_latest.py` and review these at the top
adjust the paths and the threshold if needed
    DATA_DIR = "/Users/laksh/Desktop/applications_data"
    OUTPUT_DIR = "/Users/laksh/Desktop/applications_data/dupe_reports"
    THRESHOLD = 90
3. run the script
    python dedupe_latest.py
You will see which input file was used, counts for exact duplicates and name matches, and paths to the CSV reports.

## Outputs

* exact duplicates report  
`applications_data/dupe_reports/<input_name>_dupes_report.csv`

* fuzzy name matches  
`applications_data/dupe_reports/<input_name>_name_dupes.csv`  
contains row indexes, both names, and the match score

## Notes

* exact duplicates require all of these columns to exist  
Email, Phone Number, Age, Gender  
if any are missing, the exact duplicate step is skipped with a message

* THRESHOLD controls how strict name matching is  
higher value means fewer but stronger matches  
try 85 to catch more near matches

## Run every morning on macOS

If you want a daily run at 8 am
    crontab -e


Add this line and adjust paths

    0 8 * * * /usr/bin/python3 /Users/laksh/Desktop/dedupe_latest.py >> /Users/laksh/Desktop/dupe_run.log 2>&1


## Troubleshooting

* error No CSV files found  
  make sure `applications_data` has at least one CSV

* ModuleNotFoundError for pandas or fuzzywuzzy  
  install requirements inside the virtual environment  

* permission errors on macOS  
  if your data folder is under Desktop or Documents, grant Terminal and VS Code access in System Settings Privacy and Security

## License

MIT or your choice

