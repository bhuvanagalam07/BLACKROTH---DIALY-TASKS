<<<<<<< HEAD
# Employee Data Processor

A beginner-friendly Python CLI mini-project that reads employee data from CSV, validates records, logs processing activity, and creates CSV/JSON reports.

## Features

- Reusable Python package and command-line interface (`argparse`)
- CSV input using the standard library
- Validation for names, departments, non-negative numeric salaries, and ISO dates (`YYYY-MM-DD`)
- Invalid records are written to `rejected.csv` instead of stopping all processing
- Logging to a file
- JSON employee report and department-wise CSV summary
- Automated tests with `pytest`

## Requirements

- Python 3.10 or newer
- `pip`

## Setup

### Windows PowerShell

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

If PowerShell blocks activation, use `python -m pip install -r requirements.txt` without activating the environment, or use Command Prompt activation: `.venv\\Scripts\\activate.bat`.

## Run

From the project root:

```powershell
python main.py
```

Choose your own paths:

```powershell
python main.py --input data/employees.csv --output-dir reports --log logs/app.log
```

Exit code is `0` for success and `1` for a handled processing error.

## Test

```powershell
python -m pytest -v
```

## Output files

- `reports/employee_report.json`: valid employee records
- `reports/department_summary.csv`: headcount and average salary by department
- `reports/rejected.csv`: invalid rows and rejection reasons
- `logs/app.log`: processing activity and errors

The sample CSV intentionally includes invalid salary values to demonstrate validation and rejected-row reporting.

## Demo script (about 1 minute)

1. Show `data/employees.csv` and point out the valid and invalid rows.
2. Run `python main.py`.
3. Show the valid/rejected counts in the terminal.
4. Open the generated JSON, department summary, rejected CSV, and log file.
5. Run `python -m pytest -v` and show that the tests pass.

## Learning outcomes

This project practices modules/packages, data structures, functions, classes and dataclasses, exception handling, file operations, CSV/JSON, logging, command-line arguments, and automated tests.
=======
EPIC 0: Python Real-Time Foundations

STORY 0.1: Python Core and a Real-Time Log Analyzer
Day: 1 – Monday, 05-10-2026
Project: python-epic-0
Technology: Python 3.12
Tools: VS Code, Git, GitHub
1. Objective
The objective of this task was to understand the basic concepts of Python and apply them by building a simple server log analyzer. The program reads a server log file, analyzes the log entries, counts different log levels, identifies frequently occurring errors, and creates a separate error log.
Along with development, I also tested the program with empty, valid, and malformed input files to make sure that it does not crash.
________________________________________
2. Environment Setup
The project was created using Python 3.12, Visual Studio Code, and Git. A virtual environment was created to keep the project dependencies separate from other Python projects.
The Git repository was named:
python-epic-0
Project Structure
python-epic-0/
│
├── log_analyzer.py
├── sample_server.log
├── errors_only.log
├── README.md
└── venv/
log_analyzer.py contains the main program, sample_server.log contains more than 500 sample log entries, errors_only.log stores ERROR entries, and README.md contains project information and instructions.
________________________________________
3. Python Theory Covered
During this task, I practiced the basic Python concepts required for the project.
•	Variables: Used to store values such as file names and counters.
•	Data types: Practiced strings, integers, lists, dictionaries, sets, tuples, and Boolean values.
•	If/Else: Used to check whether a log entry is INFO, WARNING, or ERROR.
•	Loops: Used to process every line in the log file.
•	Functions: Used to divide the program into smaller reusable tasks.
•	Lists: Used to store collections of data.
•	Dictionaries: Used mainly for counting log levels and error messages.
•	Sets: Used for storing unique values.
•	Tuples: Used for fixed groups of related values.
•	String handling: Used strip() and split() to process log lines.
•	F-strings: Used to display variables clearly in the output.
•	File handling: Practiced reading from and writing to text files.
For example, a dictionary can store the number of different log levels:
level_counts = {
    "INFO": 0,
    "WARNING": 0,
    "ERROR": 0
}
________________________________________
4. Log Analyzer Implementation
A server log records events that happen in an application or server. The three levels used in this task were:
INFO – Normal application activity.
2026-10-05 09:15:21 INFO Server started successfully
WARNING – A condition that may require attention.
2026-10-05 09:17:12 WARNING High memory usage detected
ERROR – Something went wrong in the application.
2026-10-05 09:18:45 ERROR Database connection failed
The sample_server.log file was generated with more than 500 entries. Each entry contains a timestamp, level, and message.
The program reads the file line by line, checks the format, identifies the log level, and updates the required counters.
Main Tasks Performed
1. Count log levels
The program counts the number of INFO, WARNING, and ERROR entries.
Example:
INFO       : 320
WARNING    : 115
ERROR      : 85
2. Find Top 5 Error Messages
The program counts repeated ERROR messages and displays the five most frequent ones.
Top 5 Error Messages:

1. Database connection failed
2. File not found
3. Connection timeout
4. Authentication failed
5. Server unavailable
3. Create errors_only.log
All ERROR entries are written into a separate file. This makes it easier to check only the problems without reading the complete server log.
4. Display Summary Report
After processing the file, the program displays the total number of lines, log-level counts, and top error messages in the console.
________________________________________
5. Error Handling and Testing
The program was designed to handle incorrect input without crashing. This is important because real-world log files may contain incomplete or malformed records.
The following tests were performed:
Test	Expected Result	Status
500+ line log file	Analyze all valid records	Passed
Empty file	Show zero counts without crashing	Passed
INFO-only file	Count INFO and show zero errors	Passed
Malformed line	Ignore/handle invalid line and continue	Passed
For example, an invalid line such as:
This is an invalid log line
should not stop the entire program.
________________________________________
6. Deliverables
The final project contains:
log_analyzer.py
sample_server.log
errors_only.log
README.md
Completion Status
•	Python 3.12 setup – Completed
•	Virtual environment – Completed
•	VS Code and Git setup – Completed
•	Python fundamentals – Completed
•	500+ log entries generated – Completed
•	Log levels counted – Completed
•	Top 5 errors identified – Completed
•	Error log created – Completed
•	Summary report generated – Completed
•	Error handling and testing – Completed
7. Conclusion
This task helped me understand Python fundamentals by applying them to a practical problem. I learned how to work with variables, conditions, loops, functions, data structures, strings, and files.
The final log analyzer successfully reads the server log, analyzes the data, finds common errors, creates an error-only file, and displays a summary. Testing with empty, INFO-only, and malformed files confirmed that the program can handle bad input without crashing.
Overall Status: Completed Successfully


STORY 0.2: Functions, Modules, Error Handling and a CLI Tool
Day: 2 – Tuesday, 06-10-2026
Project: python-epic-0
Technology: Python 3.12
Tools: VS Code, Git, pytest
1. Objective
The objective of this task was to improve the Day 1 log analyzer by converting it into a reusable command-line application. The focus was on writing better functions, organizing code into modules and packages, handling errors properly, and adding logging.
Instead of keeping everything in one Python file, the Day 1 program was refactored into separate modules:
python-epic-0/
│
├── parser.py
├── report.py
├── main.py
├── app.log
└── tests/
    └── test_parser.py
________________________________________
2. Concepts Covered
Functions
I learned how to use functions with different types of arguments.
•	Arguments: Pass values to a function.
•	Return values: Send a result back from a function.
•	*args: Allows multiple positional arguments.
•	**kwargs: Allows multiple keyword arguments.
•	Docstrings: Explain what a function does.
Example:
def add(a, b):
    """Return the sum of two numbers."""
    return a + b
Using functions made the application easier to understand and reuse.
Modules and Packages
A module is a Python file containing reusable code. The log analyzer was divided into modules so that each file has a specific responsibility.
parser.py handles reading and validating log data.
report.py handles counting levels, finding errors, and generating reports.
main.py controls the application and command-line arguments.
This separation makes the project easier to maintain and modify.
________________________________________
3. Error Handling
Error handling was added using try, except, and finally.
•	try contains code that may cause an error.
•	except handles the error.
•	finally runs whether an error occurs or not.
Instead of showing a long Python traceback to the user, the application displays a simple and friendly error message.
For example:
Error: File 'app.log' was not found.
This makes the CLI tool easier for users to understand.
________________________________________
4. Custom Exception
A custom exception called InvalidLogFormatError was added.
It is used when a log line does not follow the expected format.
Example:
class InvalidLogFormatError(Exception):
    """Raised when a log entry has an invalid format."""
This makes log-format problems easier to identify and handle separately from other errors.
________________________________________
5. Logging
The logging module was introduced to replace unnecessary print() debugging statements.
Logging provides different levels such as:
•	DEBUG – detailed development information
•	INFO – normal application activity
•	WARNING – possible problems
•	ERROR – serious problems
The application's activities and errors are recorded in:
app.log
This is more useful than using print() because logs can be saved and reviewed later.
________________________________________
6. Command-Line Interface
The application was converted into a CLI tool using Python's argparse module.
The command used is:
python main.py --file app.log --level ERROR --top 5
Here:
•	--file specifies the log file.
•	--level specifies the log level to filter.
•	--top specifies how many frequent errors should be displayed.
The argparse module also automatically provides a help option.
Command:
python main.py --help
Example output:
usage: main.py [-h] --file FILE [--level LEVEL] [--top TOP]

Analyze server log files.

options:
  -h, --help       show this help message and exit
  --file FILE      path to the log file
  --level LEVEL    filter by log level
  --top TOP        show top N errors
The help output makes the command-line tool easier to use.
________________________________________
7. Refactoring Day 1
The Day 1 log analyzer was refactored instead of creating a completely new application.
The responsibilities were separated as follows:
                 main.py
                    |
          ---------------------
          |                   |
      parser.py           report.py
          |                   |
    Read/validate       Analyze/report
       log data            results
This structure follows the idea of separation of responsibilities. Each module focuses on one part of the application.
________________________________________
8. Testing with Pytest
Five pytest tests were created for the parser.
The tests check important situations such as:
1.	Reading a valid log line
2.	Processing multiple valid lines
3.	Detecting an invalid log format
4.	Handling an empty file
5.	Handling unexpected or invalid input
The tests were executed using:
pytest
Expected result:
5 passed
Passing tests confirmed that the parser was working as expected.
________________________________________
9. Error Testing
The CLI application was tested with different error conditions.
Missing File
When a file that does not exist is provided:
python main.py --file missing.log
The application gives a friendly message instead of a traceback.
Example:
Error: File 'missing.log' was not found.
Wrong Arguments
Invalid or incomplete arguments were tested.
The CLI displays the appropriate usage information instead of crashing.
Bad Permissions
The application was also tested with a file that could not be accessed due to permissions.
The error is handled and a readable message is displayed to the user.
________________________________________
10. Git Commit
After completing the refactoring, logging, CLI, and testing work, the changes were committed to Git.
Commit message:
refactor(day2): modular CLI log tool with logging and pytest
This commit clearly describes the work completed for Day 2.
________________________________________
11. Deliverables
The completed Day 2 work contains:
python-epic-0/
│
├── parser.py
├── report.py
├── main.py
├── app.log
├── tests/
│   └── test_parser.py
└── README.md
The main deliverables are:
•	Refactored Python package
•	Command-line interface
•	--help documentation
•	Application log file
•	Custom InvalidLogFormatError
•	Five pytest tests
•	Git commit
________________________________________
12. Completion Status
Requirement	Status
Functions and arguments	Completed
*args and **kwargs	Completed
Return values and docstrings	Completed
Exception handling	Completed
Custom exception	Completed
Logging module	Completed
Modules and packages	Completed
argparse CLI	Completed
Day 1 refactoring	Completed
--help option	Completed
Missing file testing	Completed
Wrong argument testing	Completed
Permission testing	Completed
Five pytest tests	Completed
Git commit	Completed
Conclusion
This task improved the Day 1 log analyzer by making it more organized, reusable, and user-friendly. I learned how to divide a Python application into modules, create reusable functions, handle errors with custom exceptions, use logging instead of debugging prints, and build a command-line interface using argparse.
The final application can be run from the command line, provides clear help information, handles common errors without displaying confusing tracebacks, and has automated tests to verify the parser.
Overall Status: Completed Successfully
STORY 0.3: Working with Files, CSV, JSON and Data Reports
Day: 3 – Wednesday, 07-10-2026
Project: python-epic-0
Technology: Python 3.12
Tools: VS Code, Git, pytest
1. Objective
The objective of this task was to learn how to work with common business data formats such as CSV and JSON and generate useful employee reports.
I created an employee_report.py program that reads employee information from employees.csv, validates the data, performs calculations, and exports the results to JSON and CSV files.
The program was also designed to reject incorrect data instead of crashing.
________________________________________
2. Concepts Covered
CSV
CSV (Comma-Separated Values) is commonly used to store tabular business data. The employee file contains:
name, department, salary, join_date
The csv module was used to read and write employee records.
JSON
JSON is a structured format commonly used for storing and exchanging data. The report results were exported to a JSON file using Python's json module.
pathlib and os
The pathlib module was used to work with file and folder paths in a simple way. It was also used to find and process multiple CSV files in batch mode.
The os module was practiced for working with directories and the operating system.
datetime
The datetime module was used to convert join dates and identify employees who joined within the last 90 days.
List and Dictionary Comprehensions
Comprehensions were used to create and filter collections in a shorter and cleaner way.
Sorting and Grouping
Employee records were grouped department-wise and sorted when generating reports.
________________________________________
3. Employee Report
The employees.csv file was created with 50+ employee records.
Example:
name,department,salary,join_date
Rahul,IT,45000,2026-07-15
Priya,HR,40000,2026-06-20
Arun,Finance,50000,2026-05-10
The program reads each record and validates:
•	Employee name
•	Department
•	Salary
•	Joining date
________________________________________
4. Department-Wise Report
The program calculates the headcount and average salary for each department.
Example:
Department   Headcount   Average Salary
IT           18          52000
HR           10          43000
Finance      12          48000
Sales        15          45000
This provides a simple overview of employee distribution and salary levels across departments.
________________________________________
5. Employees Joined in Last 90 Days
Using datetime, the program compares each employee's joining date with the current date.
Employees whose joining date falls within the last 90 days are included in the report.
Example:
Employees Joined in Last 90 Days

1. Rahul - IT - 2026-08-15
2. Priya - HR - 2026-09-02
3. Arun - Finance - 2026-09-18
This is useful for tracking recently joined employees.
________________________________________
6. Data Validation and Rejected Records
The program checks the input before processing it.
Invalid records include:
•	Blank rows
•	Missing employee names
•	Missing departments
•	Missing salary
•	Missing joining dates
•	Incorrect date formats
•	Non-numeric salaries
•	Duplicate employee records
Rejected records are written into:
rejected.csv
This ensures that bad data is separated from valid data rather than causing the program to stop.
________________________________________
7. Batch Processing
Batch mode was implemented using pathlib.
Instead of processing only one CSV file, the program can find and process every CSV file in a selected folder.
The general process is:
Input Folder
     ↓
Find all CSV files
     ↓
Read each file
     ↓
Validate records
     ↓
Process valid records
     ↓
Reject invalid records
     ↓
Generate reports
This makes the program more useful when there are multiple employee files to process.
________________________________________
8. Output Files
The program exports the processed information into JSON and CSV formats.
The project contains files such as:
employee_report.py
employees.csv
employee_report.json
employee_report.csv
rejected.csv
README.md
The JSON file contains structured report information, while the new CSV contains the processed employee data.
________________________________________
9. Testing
The program was tested with different types of incorrect input.
Test Case	Expected Result	Status
Blank rows	Reject row without crashing	Passed
Wrong date format	Record moved to rejected.csv	Passed
Non-numeric salary	Record rejected	Passed
Duplicate record	Record detected and rejected	Passed
Missing value	Record rejected	Passed
Five additional pytest cases were also added to check data validation and report generation.
The tests were executed using:
pytest
All required tests were expected to pass successfully.
10. Manual Verification
To confirm that the report calculations were correct, the output totals were manually checked using a sample of 10 employee records.
The department counts and salary calculations from the program were compared with the manually calculated values.
The results matched, confirming that the report calculations were working correctly.
________________________________________
11. Git Commit
After completing the implementation and testing, the changes were committed to Git using:
feat(day3): CSV/JSON employee report with validation
________________________________________
12. What I Learned
Through this task, I learned how to work with real business data using Python.
The main learning points were:
•	Reading and writing CSV files
•	Creating and reading JSON data
•	Working with files and folders using pathlib
•	Using os for file-system operations
•	Working with dates using datetime
•	Using list and dictionary comprehensions
•	Sorting and grouping data
•	Validating business data
•	Detecting duplicates and missing values
•	Handling bad data without crashing
•	Creating automated tests with pytest
•	Processing multiple CSV files in batch mode
Conclusion
The employee reporting task was completed successfully. The program can read 50+ employee records, validate the data, generate department-wise reports, identify recently joined employees, detect invalid and duplicate records, and export the results to CSV and JSON.
The main goal was achieved: bad data is rejected and recorded in rejected.csv instead of crashing the program, and the report totals were verified manually.
Overall Status: Completed Successfully
STORY 0.4: REST APIs, HTTP and Automation
Day: 4 – Thursday, 08-10-2026
Project: python-epic-0
Technology: Python 3.12
Libraries: requests, python-dotenv
Testing: unittest.mock
1. Objective
The objective of this task was to understand how Python applications communicate with web services through REST APIs and to automate a repetitive task.
For this task, I created an API monitoring tool called api_monitor.py. The program checks multiple URLs, records their HTTP status and response time, handles failures using retries and timeouts, and writes downtime information to a log file.
The main focus was on understanding HTTP, REST APIs, JSON responses, authentication, error handling, and automation.
________________________________________
2. HTTP and REST API Theory
HTTP (Hypertext Transfer Protocol) is the communication method used between clients and web servers.
When a Python program sends a request to a website or API, the server sends back a response.
Common HTTP methods include:
•	GET – Used to retrieve data.
•	POST – Used to send or create data.
•	PUT – Used to update data.
•	DELETE – Used to remove data.
For this task, GET requests were mainly used to monitor URLs.
HTTP Status Codes
The response from a server contains a status code.
Code	Meaning
200	Request successful
201	Resource created
400	Bad request
401	Unauthorized
403	Forbidden
404	Resource not found
500	Internal server error
A successful response normally has a 2xx status code, while 4xx and 5xx indicate errors.
________________________________________
3. Headers and JSON
HTTP headers provide additional information about a request or response.
For example, a request can contain:
Content-Type: application/json
This tells the server that JSON data is being sent.
JSON (JavaScript Object Notation) is a common format used by REST APIs to exchange structured data.
Example:
{
    "id": 1,
    "name": "John",
    "email": "john@example.com"
}
Python can convert JSON responses into Python dictionaries and lists for further processing.
________________________________________
4. Using the Requests Library
The Python requests library was used to communicate with APIs.
A simple GET request looks like:
response = requests.get(url, timeout=10)
The program also uses:
•	GET requests
•	POST requests
•	Query parameters
•	Request timeouts
•	Retries
•	HTTP status checking
A timeout prevents the program from waiting forever when a server does not respond.
Retries allow the application to try again when a temporary connection problem occurs.
________________________________________
5. API Monitor
The main application created for this task was:
api_monitor.py
The monitor checks a list of five URLs.
The general process is:
Start Monitor
     ↓
Read URLs
     ↓
Send GET request
     ↓
Wait for response
     ↓
Check status code
     ↓
Measure response time
     ↓
Retry if required
     ↓
Log failures
     ↓
Wait 60 seconds
     ↓
Check again
The response time is measured to understand how quickly each URL responds.
Example output:
https://example.com
Status: 200
Response Time: 0.42 seconds
If a URL fails:
https://example.com/test
Status: 404
Response Time: 0.31 seconds
the failure is recorded in downtime.log.
________________________________________
6. Environment Variables and Security
Authentication information and API keys should never be directly written inside Python source code.
The python-dotenv library was used to read environment variables from a .env file.
Example:
API_KEY=your_api_key_here
The Python program can access it through an environment variable.
The actual .env file is excluded from Git using .gitignore.
An .env.example file is provided instead:
API_KEY=your_api_key_here
This shows developers which variables are required without exposing real secrets.
________________________________________
7. Public API Exercise
A free public API such as JSONPlaceholder was used for testing API requests.
The program sends a GET request, receives the JSON response, and saves the data into a JSON file.
The basic process is:
Send API request
       ↓
Receive JSON response
       ↓
Convert/process response
       ↓
Save as JSON file
This helped me understand how real APIs can be accessed and how API data can be stored for later use.
________________________________________
8. Automation
The monitor was configured to check five URLs every 60 seconds.
Python's time.sleep() can be used to wait between monitoring cycles.
Example:
time.sleep(60)
The monitor was designed to continue running for approximately 10 minutes without manual intervention.
This demonstrates how a simple Python script can automate a repetitive monitoring task.
________________________________________
9. Downtime Logging
When an API or website fails, the failure is written to:
downtime.log
A timestamp is included so that the failure can be tracked.
Example:
2026-10-08 10:15:20 - https://example.com - Status 500
2026-10-08 10:16:21 - https://invalid-url.test - Connection Error
This provides a record of service interruptions and makes troubleshooting easier.
________________________________________
10. Testing
Different failure scenarios were tested to make sure the monitor handles errors gracefully.
Invalid URL
An invalid URL was provided.
Expected: The program catches the connection error and continues monitoring other URLs.
Timeout
A request that takes too long to respond was tested.
Expected: The request times out instead of waiting indefinitely.
404 Response
A URL returning 404 Not Found was tested.
Expected: The failure is detected and written to downtime.log.
500 Response
A server-error response was tested.
Expected: The failure is recorded and the monitor continues running.
Mock API Testing
unittest.mock was used to simulate API responses and failures without depending completely on a real server.
This makes the tests faster and more reliable.
________________________________________
11. Project Deliverables
The completed project contains:
python-epic-0/
│
├── api_monitor.py
├── .env.example
├── .gitignore
├── downtime.log
└── README.md
Important Security Rule
The actual .env file containing secrets is not committed to Git.
Only .env.example is included in the repository.
________________________________________
12. Git Commit
After completing the implementation and testing, the changes were committed with:
feat(day4): API monitor with retries and downtime logging
________________________________________
13. Completion Status
Requirement	Status
HTTP basics	Completed
Status codes	Completed
Headers	Completed
JSON responses	Completed
GET and POST requests	Completed
Parameters	Completed
Timeouts	Completed
Retries	Completed
Environment variables	Completed
API monitor	Completed
Five URLs monitored	Completed
60-second monitoring interval	Completed
Downtime logging	Completed
Invalid URL testing	Completed
Timeout testing	Completed
404 testing	Completed
500 testing	Completed
Mock API testing	Completed
Secrets excluded from Git	Completed
10-minute unattended monitoring	Completed
Conclusion
This task helped me understand how Python applications communicate with real web services using REST APIs. I learned how HTTP requests and responses work, how to handle JSON data, use status codes, set timeouts and retries, and protect API keys using environment variables.
The final API monitor can continuously check multiple URLs, measure response times, handle failures without crashing, and record downtime with timestamps.
Overall Status: Completed Successfully









STORY 0.5: OOP, Mini Project and Epic Review
Day 5 – Friday, 09-10-2026
PAGE 1: OBJECT-ORIENTED PROGRAMMING AND PROJECT STRUCTURE
1. Objective
The objective of Day 5 is to combine the Python concepts learned during the previous four days into one complete mini project called Ops Toolkit. This project provides three command-line operations: log analysis, employee report generation, and API monitoring.
2. Concepts Covered
Object-Oriented Programming (OOP)
•	Class: A blueprint used to create objects.
•	Object: An instance of a class.
•	__init__(): A special method that initializes an object's attributes.
•	Inheritance: Allows one class to reuse the properties and methods of another class.
•	@dataclass: Reduces boilerplate code when creating classes that mainly store data.
•	Exception handling: Handles errors gracefully without unexpectedly stopping the application.
3. Project Structure
The project is organized into separate modules to make the code reusable and easy to maintain.
ops-toolkit/
│
├── toolkit.py
├── log_analyzer.py
├── report_generator.py
├── api_monitor.py
├── parser.py
├── report.py
├── sample_server.log
├── app.log
├── employees.csv
├── employees_report.json
├── employees_report.csv
├── rejected.csv
├── urls.txt
├── downtime.log
├── requirements.txt
├── README.md
├── .gitignore
└── tests/
    ├── test_log_analyzer.py
    ├── test_report_generator.py
    └── test_api_monitor.py
Note: The module names can be adjusted to match the existing code. The important point is to keep the application modular and ensure the imports work correctly.
4. Creating Classes
The project uses three main classes:
•	LogAnalyzer – reads log files, counts log levels, and identifies frequent error messages.
•	ReportGenerator – processes employee CSV data, calculates department statistics, and generates reports.
•	ApiMonitor – checks URLs, records response times, and logs failures.
Example of a simple class:
class LogAnalyzer:
    def __init__(self, file_path):
        self.file_path = file_path

    def analyze(self):
        print(f"Analyzing log file: {self.file_path}")
In this example, LogAnalyzer is the class, __init__() initializes the file path, and analyze() is a method that performs an operation.
A dataclass can be used to store log information:
from dataclasses import dataclass


@dataclass
class LogEntry:
    timestamp: str
    level: str
    message: str
This makes log entries easier to represent and manage.
5. Combining the Previous Stories
The Ops Toolkit combines all four earlier stories:
•	Story 0.1: Python fundamentals and log analysis.
•	Story 0.2: Functions, modules, error handling, logging, and CLI arguments.
•	Story 0.3: CSV and JSON processing, employee reports, and data validation.
•	Story 0.4: REST APIs, HTTP requests, retries, response times, and downtime logging.
This structure creates one application from the separate tools developed during the week.
________________________________________
PAGE 2: OPS TOOLKIT IMPLEMENTATION AND COMMANDS
6. Creating the Main CLI Application
The toolkit.py file serves as the main entry point. The argparse module accepts commands and their arguments from the terminal.
Example implementation:
import argparse

from log_analyzer import LogAnalyzer
from report_generator import ReportGenerator
from api_monitor import ApiMonitor


def main():
    parser = argparse.ArgumentParser(
        description="Ops Toolkit - Python automation tools"
    )

    subparsers = parser.add_subparsers(
        dest="command",
        required=True
    )

    logs_parser = subparsers.add_parser(
        "logs",
        help="Analyze server log files"
    )
    logs_parser.add_argument(
        "--file",
        required=True,
        help="Path to the log file"
    )
    logs_parser.add_argument(
        "--level",
        default="ERROR",
        help="Log level to filter"
    )
    logs_parser.add_argument(
        "--top",
        type=int,
        default=5,
        help="Number of frequent errors to display"
    )

    report_parser = subparsers.add_parser(
        "report",
        help="Generate employee reports"
    )
    report_parser.add_argument(
        "--input",
        required=True,
        help="Path to the employee CSV file"
    )

    monitor_parser = subparsers.add_parser(
        "monitor",
        help="Monitor URLs for availability"
    )
    monitor_parser.add_argument(
        "--urls",
        required=True,
        help="Path to the URL list"
    )

    args = parser.parse_args()

    if args.command == "logs":
        LogAnalyzer(args.file).analyze(
            level=args.level,
            top=args.top
        )

    elif args.command == "report":
        ReportGenerator(args.input).generate()

    elif args.command == "monitor":
        ApiMonitor(args.urls).run()


if __name__ == "__main__":
    main()
Important: This example assumes the three classes expose the methods and parameters shown above. Adjust the calls to match the actual method signatures in the project.
7. Running the Three Commands
Command 1: Log Analysis
python toolkit.py logs --file app.log
This command analyzes the specified log file, counts log levels, identifies frequent error messages, and displays a summary.
To filter errors and display the top five:
python toolkit.py logs --file app.log --level ERROR --top 5
Command 2: Employee Report
python toolkit.py report --input employees.csv
This command reads employee data and generates department-wise headcount and average salary information. It also identifies invalid rows and writes them to rejected.csv.
Command 3: API Monitoring
python toolkit.py monitor --urls urls.txt
This command reads URLs from urls.txt, checks their availability, measures response times, and records failures in downtime.log.
The monitoring implementation should support retries, timeouts, and the configured monitoring interval. It should also support a 10-minute monitoring session without requiring manual intervention.
8. Requirements and Environment
Install the project dependencies in a virtual environment.
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install requests python-dotenv pytest pytest-cov ruff
Create requirements.txt with the dependencies actually used by the application, including compatible version constraints where appropriate.
Example:
requests
python-dotenv
pytest
pytest-cov
ruff
Run the CLI help command:
python toolkit.py --help
The help output should clearly explain the available commands and their arguments.
________________________________________
PAGE 3: TESTING, CODE QUALITY, README AND EPIC REVIEW
9. Testing the Application
Testing verifies that all three modules work correctly and handle invalid input safely.
Run the complete test suite:
python -m pytest -v
Run the tests with coverage:
python -m pytest --cov=. --cov-report=term-missing
The target is 70% or higher test coverage.
The test suite should cover the following scenarios:
1.	Log Analyzer: Correctly counts INFO, WARNING, ERROR, and CRITICAL entries.
2.	Log Analyzer: Handles empty files, malformed lines, and missing files.
3.	Report Generator: Calculates department headcount and average salaries correctly.
4.	Report Generator: Rejects invalid dates, missing values, blank rows, and non-numeric salaries.
5.	API Monitor: Handles invalid URLs, request timeouts, HTTP 404 responses, and HTTP 500 responses.
6.	API Monitor: Uses mocked HTTP requests to test success, failure, and retry behavior without depending on live services.
7.	CLI: Displays help correctly and reports invalid arguments clearly.
All tests should pass before the project is considered complete.
10. Code Quality with Ruff
Ruff is used to identify Python style problems and common code issues.
Check the project:
python -m ruff check .
Automatically fix supported issues:
python -m ruff check . --fix
Format the Python files:
python -m ruff format .
Run the checks again after fixing the issues. Review any remaining warnings rather than ignoring them without a reason.
11. README Documentation
The README.md file should contain:
•	Project title and objective.
•	Features of the three commands.
•	Python version and prerequisites.
•	Virtual environment setup.
•	Dependency installation instructions.
•	Project structure.
•	Usage examples for logs, report, and monitor.
•	Test and coverage commands.
•	Configuration instructions for environment variables.
•	Sample output and troubleshooting guidance.
The .gitignore file should exclude generated and sensitive files where appropriate:
.venv/
__pycache__/
.pytest_cache/
.ruff_cache/
.coverage
.env
*.pyc
Keep .env.example in the repository with placeholder values only. Never commit API keys, passwords, or other secrets.
12. Git Commit and Version Tag
After implementing the features, running the tests, and updating the README, execute:
git status
git add .
git commit -m "release(epic0): ops toolkit v1.0"
git tag v1.0-epic0
The requested story commit message is:
release(epic0): ops toolkit v1.0 and tag v1.0-epic0
Git commit messages and tags are separate concepts, so the commit message and tag are created using separate commands. If following the exact naming convention, the tag should be v1.0-epic0.
13. Final Demonstration and Completion Criteria
For the 10-minute demo:
1.	Explain the project structure and OOP concepts.
2.	Run the log analysis command and show the summary.
3.	Generate an employee report and show the output files.
4.	Run the API monitor and explain response times and downtime logs.
5.	Run the complete pytest suite and display the coverage report.
6.	Demonstrate friendly error handling and explain the README setup instructions.
The final review should confirm that the project works in a fresh virtual environment and can be set up from a clean Git clone by following the README.
Conclusion
Day 5 brings together the Python concepts learned throughout the week into one reusable command-line application. The Ops Toolkit demonstrates object-oriented programming, modular design, file processing, CSV and JSON reporting, REST API monitoring, automated testing, code quality checks, and Git version control.
Completion status: Mark Story 0.5 and all five stories as Done in Jira only after the implementation, testing, documentation, Git tag, and demonstration have been completed and verified.



>>>>>>> 8b3b5c4f946522dac1d567fc3634a517c081a298
