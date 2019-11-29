## Code Review Strategy

Before diving into the code analysis, we started with reviewing our assurance cases, misuse cases, and threat model report. From the review, we observed the most critical weakness areas in the software and decided to approach the checklist review strategy which is would most appropriate method for analyzing the code of large-scale projects like GoCD. To reduce the effort of going through all the code for each line we decided on adopting to review all items from our [checklist](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/CodeReview/Checklist.md).

We analyzed our code in both automated and manual review process. The automated code review is performed using open source static code analysis tool called **PWD and Findbugs**. The list of resultant vulnerabilities from the automated tool scan was narrowed  down to analyze  **CWE(Common Weakness Enumeration)** that are related to our misuse case, assurance cases, and threat model and examined manually.

## Manual Code Review

## Automated Tool Scan
After exploring the DHS SWAMP scanning platform we attempted to use the system to scan the GoCD Java code files.  We did use the SWAMP platform to scan the Java Bytecode with Findbugs 3.0.1.  We also used the PMD 6.9.0 tool to scan the Java code files.

#### Findbugs 3.0.1
This tool was used in the SWAMP platform to scan the GoCD Java Bytecode.  

#### PMD 6.9.0
The most recent version of the PMD tool was just downloaded locally to a Linux host and ran against the GoCD codebase.

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/5
