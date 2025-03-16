# Git Autograder Project

---

## Project Overview

This project involves developing and refining an autograding system designed to automate the grading process for programming assignments. It leverages Git functionalities to consolidate multiple branches, resolve merge conflicts, and implement comprehensive testing through automated scripts.

---

## Key Objectives

- **Branch Consolidation**: Efficiently merge multiple feature branches into a single cohesive `main` branch.
- **Conflict Resolution**: Identify, analyze, and resolve merge conflicts by determining the correct code based on commit history.
- **Automated Grading Script**: Implement and enhance a grading script capable of compiling, running, and evaluating student submissions against predefined test cases.

---

## Core Functionalities

### Branch Management
- List and visually analyze branch structures using Git commands (`git branch -a`, `git log --graph`).
- Methodically merge branches to maintain clear commit histories and project integrity.

### Merge Conflict Resolution
- Diagnose and resolve merge conflicts by examining commit histories and commit messages (`git blame`, `git log`).
- Ensure code consistency and correctness after conflict resolution.

### Grading Script Enhancement
- Develop a robust script (`grade.sh`) capable of:
  - Compiling student submissions.
  - Running multiple test cases.
  - Generating detailed feedback reports.
- Expand grading functionality to handle batch grading for multiple submissions automatically.

---

## Technical Highlights

- Proficiency in advanced Git operations: merging, branching, conflict resolution.
- Bash scripting for automation of repetitive grading tasks.
- Application of testing frameworks and methodologies for software correctness verification.

---

## 📝 Project Structure
```
.
├── grade.sh           # Main grading script
├── test_cases/        # Directory containing test cases
└── reference_implementation/ # Reference solutions for testing
```

---

## Future Enhancements

- Integrate more advanced reporting and logging features.
- Improve scalability for larger classes or datasets.
- Develop a web-based interface for interactive grading results.
