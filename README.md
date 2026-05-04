# COBOL_SEQ3000

## Introduction
This COBOL program performs sequential file maintenance on an Employee Master file. It reads an Old Employee Master file (OLDEMP) and a Personnel Transaction file (EMPTRAN), applies HR actions using the balanced-line algorithm, and produces two output files: a New Employee Master file (NEWEMP) containing the updated roster, and an Error Transaction file (ERRTRAN) containing any HR requests that could not be processed due to logical errors.

The program handles the following HR actions:

1. **Add (A)** - Hire a new employee and write a new master record
2. **Delete (D)** - Terminate an employee and remove their record from the master file
3. **Change (C)** - Update selected fields on an existing employee's master record
4. **Error Handling** - Write invalid transactions to the error file with file status checking

---

## Table of Contents
- [What does it do?](#what-does-it-do)
- [Output Example](#output-example)
- [COBOL Concepts Used](#cobol-concepts-covered-in-this-assignment-were)
- [Authors](#authors)

---

## What does it do?
For each run, the program will:

1. Open the Old Employee Master file (OLDEMP) and Personnel Transaction file (EMPTRAN) as input.
2. Open the New Employee Master file (NEWEMP) and Error Transaction file (ERRTRAN) as output.
3. Perform an initial read of both input files before entering the main processing loop.
4. Compare the Master Employee ID to the Transaction Employee ID using the balanced-line algorithm to determine the correct action.
5. If the Master ID is less than the Transaction ID, copy the master record unchanged to NEWEMP and read the next master record.
6. If the Master ID equals the Transaction ID, evaluate the action code: Delete bypasses the record, Change updates only non-blank and non-zero fields, and a matched Add is written to the error file.
7. If the Master ID is greater than the Transaction ID, evaluate the action code: Add creates a new master record with zeroed vacation and sick hours, while unmatched Delete or Change transactions are written to the error file.
8. Check the file status after every write to NEWEMP and ERRTRAN, displaying an error message and terminating gracefully if a write fails.
9. Continue processing until both input files are exhausted (both IDs equal HIGH-VALUES).

---

## Output Example

**NEWEMP (New Employee Master File):**
10001JOHN SMITH                    SALESS1045000004001550

10003NEW HIRE ONE                  SALESS1040000000000000

10008ROBERT DAVIS                  HR   H3065000008003000

**ERRTRAN (Error Transaction File):**
C10009GHOST EMPLOYEE                IT   T10500000

A10012MARY WILLIAMS                 ACCT A10550000

D10015                                     0000000

---

## COBOL Concepts covered in this assignment were:
- Sequential file handling with fixed-length records using QSAM organization.
- Defining FILE STATUS variables and checking them after every WRITE operation.
- The balanced-line algorithm for matching records across two sorted sequential files.
- Control flow using 88-level condition names and SET statements.
- Reading with AT END handling and using HIGH-VALUE as an end-of-file sentinel.
- Conditional field updates using NOT EQUAL SPACE and NOT EQUAL ZEROES checks.
- MOVE statements for formatting new hire records, including explicit initialization of numeric fields to zero.
- Graceful program termination on file I/O errors using a processing switch.
- Writing records FROM a working-storage area using the READ INTO and WRITE FROM idioms.
- JCL configuration for a multi-step IGYWCLG compile, link, and go procedure on IBM z/OS.

---

## Authors

**Grant Peverett**

- **GitHub Profile**: [Grantyy1](https://github.com/Grantyy1)
- **Email**: [grpeve01@wsc.edu]
