---
title: Grading Hidden Test Cases
layout: default
parent: Coding Questions
---

# Grading Hidden Test Cases

Example test case results for coding questions are automatically tracked in PrairieLearn, but hidden test case results need to manually be uploaded using PrairieLearn's manual grading feature. Follow the instructions here to upload the hidden test case results:

1. In PrairieLearn, go to the assessment instance of which you would like to grade hidden test cases for.

2. Go to the Downloads tab within the assessment instance.

3. Download the file ending in `submissions_for_manual_grading.csv`.

4. Open this file in Excel. If Excel asks whether you would like to convert the data, select Don't Convert.

5. Highlight the column headers (all cells in row 1 with text) and go to Data > Filter. This should add a "drop down" icon on the edge of each header row cell.

6. Click the icon in cell E1 (`qid`) and Sort A to Z. This will sort each row by question ID, so that each question is grouped.

7. Edit cell P1 to contain the value `points` (formerly `score_perc`).

8. For each cell in column P in a row that corresponds to a coding question that needs manual grading, paste this formula:

    ```
    =INDIRECT("H" & ROW()) + [MANUALPOINTS] * IF(OR(ISNUMBER(SEARCH("""gradable"":false",INDIRECT("G" & ROW()))), ISNUMBER(SEARCH("""timedOut"":true",INDIRECT("G" & ROW())))),0,((LEN(INDIRECT("G" & ROW()))-LEN(SUBSTITUTE(INDIRECT("G" & ROW()),"""max_points"":0","""max_points"":"))) - (LEN(INDIRECT("G" & ROW()))-LEN(SUBSTITUTE(INDIRECT("G" & ROW()),"FAIL","FAI")))) / (LEN(INDIRECT("G" & ROW()))-LEN(SUBSTITUTE(INDIRECT("G" & ROW()),"""max_points"":0","""max_points"":"))))
    ```
    
    Replace the value `[MANUALPOINTS]` at the start of the formula to the number of manual grading points assigned to the question in PrairieLearn. You can use the square in the bottom right corner of the first cell to drag it down to copy across the rest of the cells corresponding to coding questions. The number in this column will represent the total number of points (auto + manual) the student earned for this question.

9. After all coding questions have a value in column P, save the file in the csv format.

10. Go to the Uploads tab for the assessment instance in PrairieLearn.

11. Select Upload new question scores and upload the csv file you just saved. Wait for the output on the screen to confirm the manual grading upload completed.