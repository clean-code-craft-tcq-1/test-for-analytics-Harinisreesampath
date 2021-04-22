# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file.
2. Read access to csv files in the server.
3. Utility for handling csv files.
4. Utility for generating PDF reports.
5. Utility for sending notifications. 

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | Off-the-shelf PDF converter will be already tested by their developers. We simply just use their functionalities.
Counting the breaches       | Yes           | To count number of times it crossed the threshold in a month.
Detecting trends            | Yes           | To identify if there are any rise in the readings for continuous 30 minutes.
Notification utility        | Yes           | To check whether the notification functionalities are working as expected. 

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data.
3. Write "No Data" to the PDF when the csv is an empty file.
4. Write "Breach Count" to the PDF from a csv containing readings that cross the threshold limit.
5. Write "0" for breach count to the PDF when there is no readings crosses the threshold limit.
6. Write "Record Trends" to the PDF from a csv containing readings that increase continuously for 30 minutes.
7. Generate a fake "PDF Report" from csv analysis for every weeks.
8. Store the PDF report to server when the PDF is generated. 
9. Trigger a fake notification whenever PDF report is generated.
10. Return "Success" when fake notification is triggered as expected.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | recipients   | success / failed            | Fake the notification
Report inaccessible server | server address, credentials | connected / disconnected               | Fake the server
Find minimum and maximum   | csv data     | minimum & maximum value     | None - it's a pure function
Detect trend               | csv data     | timestamp details           | None - it's a pure function
Write to PDF               | report data  | PDF File                    | Fake the pdf file
