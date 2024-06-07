% ECS 98F: Final Assignment
% Noah Rose Ledesma
% UC Davis

## 1 Changelog

* v1: First publication

## 2 General Information

* You are to work alone for this homework

## 3 Materials

The git repository has been given to you as a zip file. Unzipping the archive
will create a new directory `10.git/` that is the git repository. All commands
you write in the following sections should be relative to that directory.

## 3 Introduction

You are writing an autograder for a homework assignment for ECS 98F, a one-unit
seminar course for undergraduate students at UC Davis. Your co-instructors have
created a git repository for the assignment and have each contributed different
components.

They have asked you to complete the grading script but before you can do that,
you need to consolidate all of the work into a single branch.

## 4 Requirements

The goal of this assignment is for you to consolidate all of these changes into
the `main` branch of the repository and update the provided grading script.

This document will walk through the required steps and occasionally prompt you
for a free text response. You should edit this file in response to the prompts.

### 4.1 Consolidating the branches

Before you begin merging changes, you need to discover what changes were made.
Enter the git command used to list all of the branches in the repository

Question One:
```
<Your answer here>
git branch -a
```

Knowing what branches exist in the repository is only somewhat helpful. What is
more important is understanding how these branches relate to each other. To see
a visual representation of the different branches and how they relate to the
`main` branch, run the following command:

```
git log --all --decorate --oneline --graph
```

Where is the `HEAD` of the `main` branch in relation to the other commits in
the output of the previous command? What commits are above and below it?

Question Two:
```
<Your answer here>
The `HEAD` of the `main` branch is at commit `40ccab8`. There are several commits above it from different branches such as `grading_script`, `grade_function`, `compare_outputs`, `reference_impl`, and `test_cases`.
```

Which two branches have the commit with the message `Add reference
implementation`?

Question Three:
```
<Your answer here>
The branches `reference_impl` and `test_cases` have the commit with the message `Add reference implementation`.
```

### 4.2 Merge reference_impl

Merge the `reference_impl` branch into the `main` branch and write the command
you used below.

Question Four:
```
<Your answer here>
git merge reference_impl
```

To better understand what this merge did to the repository, rerun the `git log`
command ran previously. Where is the `HEAD` of the main branch now? Where is
the tip of the `reference_impl` branch in relation to `HEAD`?

Question Five:
```
<Your answer here>
The `HEAD` of the `main` branch is now at the merge commit that includes the `reference_impl` branch. The tip of the `reference_impl` branch is now included in the `HEAD` of the `main` branch.
```

Where do you expect the `HEAD` of the main branch to be after the `test_cases`
branch is merged?

Question Six:
```
<Your answer here>
I expect the `HEAD` of the `main` branch to be at the merge commit that includes the `test_cases` branch.
```

### 4.3 Merge test_cases

Try to merge the `test_cases` branch into the `main` branch and write the
command you used below. What stops you from merging these branches?

Question Seven:
```
<Your answer here>
git merge test_cases
```

Open the file that contains the merge conflict. What is the line of code that
is causing the merge conflict from the `main` branch?

Question Eight:
```
<Your answer here>
printf("%d is not an integer.\n", value);
```

What is the line of code from the `test_cases` branch?

Question Nine:
```
<Your answer here>
```

Before we can resolve this conflict, we need to understand why these two
changes were introduced. Run the following command to see which what commit
each line is from in `sum.c`.
```
git blame reference_implementation/sum.c
```

What are the two commit hashes for the conflicting lines?

Question Ten:
```
<Your answer here>
```

Read the commit message for each of these commits using the following command.

```
git log <commit hash>
```

What should the correct line be? Justify your answer.

Question Eleven:
```
<Your answer here>
```

Resolve the merge conflict by replacing both lines with the correct line. Then,
run `git add` on `sum.c` and `git commit` to conclude the merge. Don't forget
to remove the merge conflict markers from `sum.c` before committing!

### 4.4 Merge remaining branches

Before continuing, take another look at the `git log` graph. Notice where HEAD
is in relation to the other branches. There are a number of branches to merge
still.

Verify that your graph matches
```
*   d2c3305 (HEAD -> main) Merge branch 'test_cases'
|\  
| * b222656 (test_cases) Add missing period in error message
| * 7b827eb Add test cases
| * ab572e3 Add reference implementation
* | 79b7b46 (reference_impl) Put single quotes around invalid input. The ASSIGNMENT.md file specifies that invalid input should be printed out with single quotes around the offending string.
* | 9c59a73 Add reference implementation
|/  
| * e9c6e3f (sample_submissions) Add sample submissions
|/  
| * 710ccf7 (compare_outputs) Compare the output of the submission against the expected string
| * dced2c2 Add function for running a single test case against a submission The output of the submission needs to be compared to the expected output. This is left as a TODO for Noah.
| * be86eed Add compile submission function to grading script
|/  
| * abe2726 (grade_function) Add code to run grading function
| * 206f8a2 Add function to grade a single submission
| * f18a271 Compare the output of the submission against the expected string
| * e361255 Add function for running a single test case against a submission The output of the submission needs to be compared to the expected output. This is left as a TODO for Noah.
| * 7e09c4f Add compile submission function to grading script
|/  
| * e0daf26 (grading_script) Fix typo in grep for exit code
| * 3de20ec Add function for running a single test case against a submission The output of the submission needs to be compared to the expected output. This is left as a TODO for Noah.
| * 04e0bdf Add compile submission function to grading script
|/  
* 40ccab8 Init commit
```

The branch `grading_script` should be merged into `main` before
`grade_function` or `compare_outputs`. Explain why this is using the
information from the `git log` graph to justify your answer.

Question Twelve:
```
<Your answer here>
```

Merge the `grading_script` branch into main. Then, merge the `grade_function`
and `compare_outputs` branches, resolving any conflicts if necessary.

Finally merge the `sample_submissions` branch into main.

### 4.5 Completing the grading script

After merging all the branches into main, the `grade.sh` script will be
configured to grade a single student's submission. Try running it on the
reference implementation like so:

```
$ ./grade.sh reference_implementation/
```

Before making any changes to the script, create a new branch "grade_all" and
switch to it.

Create a new function in this script called `grade_all` that will grade all
student submissions in a directory. It should take a single parameter `$1`,
that should be the directory containing all of the student submissions.

For every student submission in the provided directory run the `grade` function
on that submission. Change the code at the very bottom of the script to call
the new `grade_all` function.


After you have made these changes, the grading script should have the following
behavior.
```
$ ./grade.sh sample_submissions/
== Grade Submission sample_submissions/0/ ==
-- Compile Submission --
Pass: submission compiles
Run Test "test_cases/case_0.txt" ... Pass
Run Test "test_cases/case_1.txt" ... Pass
Run Test "test_cases/case_2.txt" ... Pass
Run Test "test_cases/case_3.txt" ... Fail: sum of "4.0 1" should be "'4.0' is not an integer.". Got "4.0 is not an integer.".
Run Test "test_cases/case_4.txt" ... Fail: sum of "1 1 2 toto tata" should be "'toto' is not an integer.". Got "toto is not an integer.".
== Grade: 3/5 ==

== Grade Submission sample_submissions/1/ ==
-- Compile Submission --
Pass: submission compiles
Run Test "test_cases/case_0.txt" ... Pass
Run Test "test_cases/case_1.txt" ... Pass
Run Test "test_cases/case_2.txt" ... Pass
Run Test "test_cases/case_3.txt" ... Pass
Run Test "test_cases/case_4.txt" ... Pass
== Grade: 5/5 ==

== Grade Submission sample_submissions/2/ ==
-- Compile Submission --
Pass: submission compiles
Run Test "test_cases/case_0.txt" ... Pass
Run Test "test_cases/case_1.txt" ... Pass
Run Test "test_cases/case_2.txt" ... Pass
Run Test "test_cases/case_3.txt" ... Fail: sum of "4.0 1" should be "'4.0' is not an integer.". Got "'4.0' is not an integer".
Run Test "test_cases/case_4.txt" ... Fail: sum of "1 1 2 toto tata" should be "'toto' is not an integer.". Got "'toto' is not an integer".
== Grade: 3/5 ==

== Grade Submission sample_submissions/3/ ==
-- Compile Submission --
Pass: submission compiles
Run Test "test_cases/case_0.txt" ... Fail: sum of "5 5 10" should be "20". Got "21".
Run Test "test_cases/case_1.txt" ... Pass
Run Test "test_cases/case_2.txt" ... Pass
Run Test "test_cases/case_3.txt" ... Pass
Run Test "test_cases/case_4.txt" ... Pass
== Grade: 4/5 ==

== Grade Submission sample_submissions/4/ ==
-- Compile Submission --
Pass: submission compiles
Run Test "test_cases/case_0.txt" ... Fail: sum of "5 5 10" should be "20". Got "15".
Run Test "test_cases/case_1.txt" ... Fail: sum of "-1 4 1 2" should be "6". Got "7".
Run Test "test_cases/case_2.txt" ... Pass
Run Test "test_cases/case_3.txt" ... Fail: sum of "4.0 1" should be "'4.0' is not an integer.". Got "1".
Run Test "test_cases/case_4.txt" ... Pass
== Grade: 2/5 ==
```

Finally, merge your changes into the `main` branch.

## 5 Notes

- ***Do not modify the commit message for merges***
  - The autograder will be looking for these commits by the message name.

- ***Do not enable the "expand zip" option when uploading to Gradescope***

- If you submit the assignment only to discover your git history was incorrect,
don't be afraid to restart from the handout repository. Once you have gone
through the steps once, going through them again should not be difficult.

## 6 Submission

Create a zip file of your git repository with the following commands:
```
$ zip -r submission.zip 10.git/
$ mv submission.zip submission
```
Removing the `.zip` extension  with `mv` stops Gradescope from automatically
expanding it.

Upload `submission` and a separate copy of this document (`ASSIGNMENT.md`) to
the appropriate assignment on Gradescope. You should be uploading two files to
Gradescope.

## 7 Grading

+----------------------------------------------+--------+
| Criteria                                     | Points |
+----------------------------------------------+--------+
| Correct order of merges                      | 2      |
+----------------------------------------------+--------+
| Correct commits                              | 2      |
+----------------------------------------------+--------+
| Correct order of commits                     | 2      |
+----------------------------------------------+--------+
| Complete grading script                      | 2      |
+----------------------------------------------+--------+
| Answer sheet                                 | 2      |
+----------------------------------------------+--------+
| Total                                        | 10     |
+----------------------------------------------+--------+