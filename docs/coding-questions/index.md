---
title: Coding Questions
layout: default
nav_order: 3
has_toc: false
---

# Coding Questions

Before you begin writing coding questions, you must have PrairieLearn installed locally ([instructions here]({{ site.baseurl }}{% link docs/installing-prairielearn-locally/index.md %})). The guide for this section will run through the development process of a coding question already implemented, `arrayContainsDuplicate`, which you can find by that QID on PrairieLearn, or by that folder name inside `pl-virginia-cs2100/questions`. All steps and code used to write this question will be shown on this guide, along with blank templates you can use to create new questions (the overall process is the same for all coding questions). Follow the below steps in order:

1. In IntelliJ, create a blank project you will use to develop a solution to the question and JUnit test cases. You can reuse the same IntelliJ project to write multiple questions (delete the contents of each file and start over).

2. Follow the instructions [here](https://www.jetbrains.com/help/idea/junit.html#intellij) (only the "Add dependencies" section) to set up JUnit for this project.

3. If the question will ask the student to simply write a method, create a file in `src` called `Solution.java`. If the question will ask the student to write or fill in missing code of a class, then create a file with the name of the class the student will need to edit to answer the question. Inside this class, write the starter code and your solution to the problem. For the question `arrayContainsDuplicate`, the student's method takes in an `int` array and must return `true` if the array contains any duplicate values, or `false` otherwise. Here is an example `Solution.java` for this question (I know this isn't the most efficient solution, but most students would come up with this solution):

    ```java
    public class Solution {
        public boolean containsDuplicate(int[] nums) {
            for (int i = 0; i < nums.length - 1; i++) {
                for (int j = i + 1; j < nums.length; j++) {
                    if (nums[i] == nums[j]) {
                        return true;
                    }
                }
            }
            return false;
        }
    }
    ```

    If your question requires additional classes (e.g. a linked list question would require a `Node` class), then also add that class to the `src` folder. The student will only be able to edit one specified class, but there will be an additional step later on in order to ensure the additional classes can be used in the autograder.

4. Add a new class called `Tests.java` to the `src` folder. Paste the following template into this file:

    ```java
    import org.junit.jupiter.api.Test;
    import org.junit.jupiter.api.DisplayName;
    import org.junit.jupiter.api.Tag;
    import static org.junit.jupiter.api.Assertions.*;
    
    public class Tests {
        
    }
    ```

5. Now, write all the test cases for this question. There should be about 1-3 example test cases that should be shown to the student to ensure they understand the problem. Each test should be written using this template:
    
    ```java
    @Test
    @DisplayName("Test name")
    @Tag("points=_")
    void testName() {
    
    }
    ```
    The `@DisplayName` tag should contain the test case name, formatted like normal English. If this is an example test case, the display name should start with "Example" (If there is only 1 given example, use "Example", otherwise, use "Example 1", "Example 2", etc.)

    The tag containing a point value should contain "points=1" if the test case is an example, and "points=0" if a hidden test case. This is done so that only example test case results are shown while students are taking the quiz.

    Ensure you create as many tests as necessary to judge the student's submitted code, including edge cases (may be only a few test cases). Edge cases should not be included in the example test cases, but make sure the edge cases are realistic (e.g. add an assumption that the input will never be `null`). Do not use dynamic randomly generated test cases, as it could cause different results for students with similar submissions.

    All assertions for only **non-example** test cases should include the assertion fail message "FAIL". This is used to update the grading for hidden test case results later.

    Here is the `Tests.java` file for `arrayContainsDuplicate`:

    ```java
    import org.junit.jupiter.api.Test;
    import org.junit.jupiter.api.DisplayName;
    import org.junit.jupiter.api.Tag;
    import static org.junit.jupiter.api.Assertions.*;

    public class Tests {
        @Test
        @DisplayName("Example 1")
        @Tag("points=1")
        void example1() {
            Solution sol = new Solution();
            assertTrue(sol.containsDuplicate(new int[] {1, 2, 1, 3}));
        }

        @Test
        @DisplayName("Example 2")
        @Tag("points=1")
        void example2() {
            Solution sol = new Solution();
            assertFalse(sol.containsDuplicate(new int[] {1, 2, 3}));
        }

        @Test
        @DisplayName("Empty array")
        @Tag("points=0")
        void emptyArray() {
            Solution sol = new Solution();
            assertFalse(sol.containsDuplicate(new int[] {}), "FAIL");
        }

        @Test
        @DisplayName("1 element")
        @Tag("points=0")
        void oneElement() {
            Solution sol = new Solution();
            assertFalse(sol.containsDuplicate(new int[] {1}), "FAIL");
        }

        @Test
        @DisplayName("All same number")
        @Tag("points=0")
        void allSameNumber() {
            Solution sol = new Solution();
            assertTrue(sol.containsDuplicate(new int[] {5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5}), "FAIL");
        }

        @Test
        @DisplayName("Large array, no duplicates")
        @Tag("points=0")
        void largeArrayNoDuplicates() {
            Solution sol = new Solution();
            assertFalse(sol.containsDuplicate(new int[] {-59, 7, -38, 52, -17, 69, -86, -25, -63, 50, -23, -29, -22, -65, 54, -2, -45, -41, 17, 43}), "FAIL");
        }

        @Test
        @DisplayName("Large array, 1 duplicate")
        @Tag("points=0")
        void LargeArrayOneDuplicate() {
            Solution sol = new Solution();
            assertTrue(sol.containsDuplicate(new int[] {-59, 7, -38, 52, -17, 69, -86, -25, -2, -63, 50, -23, -29, -22, -65, 54, -2, -45, -41, 17, 43}), "FAIL");
        }

        @Test
        @DisplayName("Large array, many duplicates")
        @Tag("points=0")
        void largeArrayManyDuplicates() {
            Solution sol = new Solution();
            assertTrue(sol.containsDuplicate(new int[] {-4, -3, 4, -4, -5, 2, 4, -3, 2, 5, 2, -1, -2, -1, -5, -3, -2, 4, 0, -3}), "FAIL");
        }
    }
    ```

6. Start up PrairieLearn locally and go to the CS 2100 "Questions" tab. Click "Add question" on the right. The title for the question should be a short description of the question, formatted in normal English (e.g. Array contains duplicate). Students will see the title of the question while taking the quiz, so it should not give away the solution. The QID for the question should be the same, or similar to the title, but in camelCase (e.g. arrayContainsDuplicate). Students will not be able to see the QID. Leave the "Start from Empty Question" option as it is. Click "Create".

7. Open the `pl-virginia-cs2100` folder in VS Code. 

    If you are on Windows, open the terminal in VS Code and run the following commands: `cd ~` followed by `sudo chown -R [yourusername] .` This will make you the owner of the files, since that is not the default.

    Navigate to the `questions` folder and then the subfolder with the QID of the question you just created.

8. Inside this folder, create a folder called `tests`. Inside the `tests` folder, create a folder called `junit`. Inside the `junit` folder, create a file called `Tests.java`. Paste your entire `Tests.java` file from IntelliJ into the newly created `Tests.java` in VS Code. Your folder structure should look like this:

    ![Image]({{ site.baseurl }}/assets/images/coding-question-folder-structure.png)

9. Open the file `info.json`. Paste the following JSON data right after "v3":

    ```
    ,
    "gradingMethod": "External",
    "externalGradingOptions": { "enabled": true, "image": "prairielearn/grader-java", "timeout": 20 },
    "tags": ["coding"],
    "singleVariant": true
    ```

    You can edit the "timeout" parameter (max seconds the autograder will run for before stopping) if you think your question's autograder may take more than 20 seconds per submission (20 seconds should be fine for most, if not all, questions)

    Your `info.json` file should look something like this now (uuid, title, and topic will be different):

    ```json
    {
        "uuid": "36290743-9bfa-4e1c-bb42-4f8bad8537ff",
        "title": "Array contains duplicate",
        "topic": "Arrays",
        "type": "v3",
        "gradingMethod": "External",
        "externalGradingOptions": { "enabled": true, "image": "prairielearn/grader-java", "timeout": 20 },
        "tags": ["coding"],
        "singleVariant": true
    }
    ```

10. Open the file `server.py` and paste the following code:

    ```py
    def generate(data):
        data["params"]["_grader"] = {
            "type": "java",
            "workingDirectory": "tests",
            "compile": {
                "command": "javac",
                "args": ["-cp", ".:junit/*", "../student_code/Solution.java", "junit/Tests.java"]
            },
            "execute": {
                "command": "java",
                "args": ["-cp", ".:junit/*", "org.junit.runner.JUnitCore", "Tests",]
            }
        }
    ```

    If the file that the student will edit is not called `Solution.java`, change the name of the file in line 7 to the name of the file the student will edit.

11. Open the file `question.html` and paste the following template.

    ```html
    <pl-question-panel>
    <markdown>Question instructions</markdown>

    <p style="font-weight: bold;">Example 1:</p>
    <div style="margin-left: 20px;"> 
        <markdown>Input: `param = value`</markdown>
        <markdown>Output: `output`</markdown>
        <markdown>Explanation: Why the input produced that output</markdown>
    </div>

    <p style="font-weight: bold;">You may assume:</p>
    <div style="margin-left: 20px;">
        <markdown>Assumptions the student can make that won't be tested in hidden test cases</markdown>
    </div>

    <pl-file-editor file-name="Solution.java" ace-mode="ace/mode/java">public class Solution {
        public returnType methodName(params) {
            // Type code here. Do not change the class or method headers.
        }
    }</pl-file-editor>
    </pl-question-panel>

    <pl-submission-panel>
        <example-test-results></example-test-results>
        <pl-file-preview></pl-file-preview>
    </pl-submission-panel>
    ```

    This html file is what is shown to the students when they are taking the quiz. See the [question.html Formatting]({{ site.baseurl }}{% link docs/question-html-formatting/index.md %}) page for how to use Markdown and properly use this template to format the question.

    Include all example test cases in `question.html` and copy that portion of the template multiple times if there are multiple examples. The text inside the `pl-file-editor` tag is the starter code for the question. Replace it with your solution for testing, and then delete your solution from `question.html` before committing and pushing. If the submitted file is not called `Solution.java`, be sure to edit the `file-name` parameter in the `pl-file-editor` tag to match the name of the submitted file.

    Here is what `question.html` looks like for `arrayContainsDuplicate`:

    ```html
    <pl-question-panel>
    <markdown>Develop a method that determines whether an integer array `nums` contains any duplicate values. The method should return `true` if any element is appears more than once, and `false` if every element in the array is distinct.</markdown>

    <p style="font-weight: bold;">Example 1:</p>
    <div style="margin-left: 20px;"> 
        <markdown>Input: `nums = {1, 2, 1, 3}`</markdown>
        <markdown>Output: `true`</markdown>
        <markdown>Explanation: The element 1 occurs more than once.</markdown>
    </div>

    <p style="font-weight: bold;">Example 2:</p>
    <div style="margin-left: 20px;"> 
        <markdown>Input: `nums = {1, 2, 3}`</markdown>
        <markdown>Output: `false`</markdown>
        <markdown>Explanation: All elements are unique.</markdown>
    </div>

    <p style="font-weight: bold;">You may assume:</p>
    <div style="margin-left: 20px;">
        <markdown>`nums` will never be `null`.</markdown>
    </div>

    <pl-file-editor file-name="Solution.java" ace-mode="ace/mode/java">public class Solution {
        public boolean containsDuplicate(int[] nums) {
            // Type code here. Do not change the class or method headers.
        }
    }</pl-file-editor>
    </pl-question-panel>

    <pl-submission-panel>
        <example-test-results></example-test-results>
        <pl-file-preview></pl-file-preview>
    </pl-submission-panel>
    ```

12. If you do not have any additional Java classes required for this question (e.g. a `Node` class for a linked list question), then you can skip this step. To add additional Java classes, create a folder called `libs` inside the `tests` folder of this question (such that it is on the same level as the `junit` folder. Go back into IntelliJ and go into the `out/production/ProjectName` folder and find the corresponding .class file of the class that needs to be included but not edited. Open that .class file in your file explorer and copy it into the newly created `libs` folder. Repeat this with all .class files needed. Do not copy over `Tests.class`, `Solution.class`, or the name of the file the student will edit. Note that the students won't be able to see the implementation of these files, so you should display the contents of the file or a UML class diagram inside `question.html` (see [question.html Formatting]({{ site.baseurl }}{% link docs/question-html-formatting/index.md %})).

13. To preview your file, go into the "Questions" tab in your locally hosted PrairieLearn site, and find the question you just wrote. Ensure it is formatted correctly, and try the "Save & Grade" button to ensure the autograder works properly. It should only show the results of the example test cases.

14. Once you are satisfied with the question, be sure to delete the solution from `question.html`. In the locally hosted PrairieLearn site, go to the question settings and update the topic and tags to match the question and click "Save". Then, commit and push your changes. Now, your questions should be synced to the remote repository and available on the online PrairieLearn course site!