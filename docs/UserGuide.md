# 🦈 The Sharkives User Guide

The Sharkives is a **desktop application for managing loan records**, optimized for use via a **Command Line Interface (CLI)** while still offering a **Graphical User Interface (GUI)**. If you can type fast, The Sharkster helps you manage loans, repayments, and outstanding debts **more efficiently** than traditional GUI apps.

## Table of Contents

- [Quick start](#quick-start)
- [Features](#features)
  - [Adding a person: `add`](#adding-a-person-add)
  - [Adding a Loan : `loan`](#adding-a-loan-loan)
  - [Sorting the borrowers: `sort`](#sorting-the-borrowers-sort)
  - [Recording a Payment: `pay`](#recording-a-payment-pay)
  - [Filtering loans: `filter`](#filtering-loans-filter)
  - [Deleting a Loanee: `delete`](#deleting-a-loanee-delete)
  - [Deleting a Loanee's Loan: `delete loan`](#deleting-a-loanees-loan-delete-loan)
  - [Listing all Loanees: `list`](#listing-all-loanees-list)
  - [Editing Loanee Details: `edit`](#editing-loanee-details-edit)
  - [Exiting the program : `exit`](#exiting-the-program-exit)
  - [Saving the data](#saving-the-data)
  - [Editing the data file](#editing-the-data-file)
  - [Archiving data files `[coming in v2.0]`](#archiving-data-files-coming-in-v20)
- [FAQ](#faq)
- [Known issues](#known-issues)
- [Command summary](#command-summary)
- [Appendix](#appendix)
- [Glossary](#glossary)

<page-nav-print />

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `17` or above installed in your Computer.<br>
   **Mac users:** Ensure you have the precise JDK version prescribed [here](https://se-education.org/guides/tutorials/javaInstallationMac.html).

2. Download the latest `.jar` file from [here](https://github.com/se-edu/addressbook-level3/releases).

3. Copy the file to the folder you want to use as the _home folder_ for The Sharkives.

4. Open a [command terminal](#glossary), `cd` into the folder you put the jar file in, and use the `java -jar sharkives.jar` command to run the application. `cd` [quick guide](https://www.ibm.com/docs/en/aix/7.3?topic=directories-changing-another-directory-cd-command).<br>
   A [GUI](#glossary) similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

5. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

    * `loan 1 s 1000 10 2027-10-10` : Creates a new simple interest loan with 10% interest for a selected borrower.

    * `sort` : Sort borrowers by name and order asc (default).

    * `list` : Lists all recorded borrowers and their loans.

    * `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01` : Adds a borrower named John Doe to Sharkives.

    * `clear` : Deletes all borrower records.

    * `exit` : Exits the app.

6. Refer to the [Features](#features) below for details of each command.

7. Alternatively, skip straight to our [Command Summary](#command-summary) to get started immediately!

--------------------------------------------------------------------------------------------------------------------

## Features

<box type="info" seamless>

**Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/friend`, `t/friend t/family` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

* If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines as space characters surrounding line-breaks may be omitted when copied over to the application.
</box>

---

### Adding a person: `add`

Adds a person to the address book.

Format: `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]…​`

<div markdown="span" class="alert alert-primary">💡 Tip:
A person can have any number of tags (including 0)
</div>

Examples:
* `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01`
* `add n/Betsy Crowe t/friend e/betsycrowe@example.com a/Newgate Prison p/1234567 t/criminal`

<div style="page-break-after: always;"></div>

---

### Adding a Loan: `loan`

Adds a loan to a contact in the address book. Loans can be either **Simple Interest Loans** or **Compound Interest Loans**.

Format: `loan INDEX TYPE AMOUNT INTEREST_RATE DUE_DATE​`
- `INDEX` refers to the index number of the contact as displayed in the contact list.
- `TYPE` is either `s` (Simple Interest Loan) or `c` (Compound Interest Loan).
- `AMOUNT` is the principal loan amount (accepts up to 2 d.p.).
- `INTEREST_RATE` is the percentage interest rate (accepts up to 2 d.p.).
- `DUE_DATE` is the loan's due date in `YYYY-MM-DD` format.


Examples:
* `loan 1 s 100.00 5.5 2025-12-31`
* `loan 2 c 500 7 2026-06-15`

---

### Sorting the borrowers: `sort`

Sorts the borrowers by parameter and order.

**Format:** `sort s/PARAMETER o/ORDER`
- `PARAMETER` refers to which parameter to sort by `AMOUNT` (Total amount of loans owed for each borrower), `OVERDUE` (Borrower with the most overdue loan), `NAME` (Name of borrower).
- `AMOUNT` refer to order which to sort by. (`ASC` or `DESC`).

**Example:** `sort s/AMOUNT o/ASC`

---


### Recording a Payment: `pay`

Records a payment made by the loanee.

**Format:** `pay PERSON_INDEX LOAN_INDEX AMOUNT`
- `PERSON_INDEX` refers to the index number of the loanee in the contact list.
- `LOAN_INDEX` refers to the index number of the loan of the loanee to pay.
- `AMOUNT` is the amount paid (accepts up to 2 d.p.).

**Example:** `pay 1 2 50.00`

**Alternative Format 1:** `pay PERSON_INDEX LOAN_INDEX MONTHS'M'`
- `MONTHS` is the number of months' worth of instalments to pay.

**Example:** `pay 1 2 5M`

**Alternative Format 2:** `pay PERSON_INDEX LOAN_INDEX all`
- Pays all the remaining owed by the loanee for a particular loan.

**Example:** `pay 1 2 all`

---

<div style="page-break-after: always;"></div>

### Filtering loans: `filter`

Filters and displays the loans by the given conditions and parameters.
You can chain multiple predicates of different parameters.

**Format:** `filter INDEX(optional) [pred/ PARAMETER [TOKENS]...]...`
- `INDEX` refers to the index number of the loanee in the contact list.
- `PARAMETER` refers to which parameter to sort by `AMOUNT` (Total amount of loans owed for each borrower), `OVERDUE` (Borrower with the most overdue loan), `NAME` (Name of borrower).
- `TOKENS` refer to the further arguments to specify a predicate, respective tokens for each parameter are listed below.

**Format:** `filter clear`
- clears all [predicates](#glossary) and shows all loans

| Parameter    | Required Tokens                                                                                                                  |
|--------------|----------------------------------------------------------------------------------------------------------------------------------|
| **amount**   | `operator(< or >), amount(float)` <br> e.g., `pred/ amount > 500` <br> shows client's loans greater than $500.00 remaining owed  |
| **dueDate**  | `operator(< or >), dueDate(yyyy-mm-dd)` <br> e.g., `pred/ dueDate < 2025-05-10` <br> shows client's loans due before 10 May 2025 |
| **loanType** | `loanType(s or c)` <br> e.g., `pred/ loanType s` <br> shows client's simple interest loans                                       |
| **isPaid**   | `paidStatus(y or n)` <br> e.g., `pred/ isPaid n` <br> shows client's loans that are unpaid                                       |

**Example:** `filter 3 pred/ amount > 500 pred/ loanType c pred/ isPaid n` (with person index)

**Example:** `filter pred/ amount < 200 pred/ isPaid y` (without person index)

**Example:** `filter clear` (to clear all predicates)

---

### Deleting a Loanee: `delete`

Deletes all details associated with a loanee.

**Format:** `delete INDEX`
- `INDEX` refers to the index number of the loanee in the contact list.

**Example:** `delete 2`

---

### Deleting a Loanee's Loan: `delete loan`

Deletes a specified loan from a loanee.

**Format:** `delete loan PERSON_INDEX LOAN_INDEX`
- `PERSON_INDEX` refers to the index number of the loanee in the contact list.
- `LOAN_INDEX` refers to the index number of the loan in the loanee's loan list.

**Example:** `delete loan 2 1`

---

<div style="page-break-after: always;"></div>

### Listing all Loanees: `list`

Displays a list of all loanees in the address book.

**Format:** `list`

---

### Editing Loanee Details: `edit`

Edits the details of a loanee.

**Format:** `edit INDEX [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`
- `INDEX` refers to the index number of the loanee in the contact list.
- Include only the fields that need to be changed.

**Examples:** 
* `edit 2 n/James Lee e/jameslee@example.com`
* `edit 1 a/123 NUS Street t/Enemy`

---

### Exiting the program: `exit`

Exits the program.

**Format:** `exit`

---

### Saving the data

AddressBook data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

AddressBook data are saved automatically as a JSON file `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing that data file.

<box type="warning" seamless>

**Caution:**
If your changes to the data file makes its format invalid, AddressBook will discard all data and start with an empty data file at the next run.  Hence, it is recommended to take a backup of the file before editing it.<br>
Furthermore, certain edits can cause the AddressBook to behave in unexpected ways (e.g., if a value entered is outside the acceptable range). Therefore, edit the data file only if you are confident that you can update it correctly.
</box>

### Archiving data files `[coming in v2.0]`

_Details coming soon ..._

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous AddressBook home folder.

--------------------------------------------------------------------------------------------------------------------

## Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
2. **If you minimize the Help Window** and then run the `help` command (or use the `Help` menu, or the keyboard shortcut `F1`) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.

--------------------------------------------------------------------------------------------------------------------

<div style="page-break-after: always;"></div>

## Command summary

| Action     | Format, Examples                                                                                                                                                                                           |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Add**    | `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]…​` <br> e.g., `add n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665 t/friend t/colleague`                                      |
| **Loan**   | `loan INDEX TYPE(s/c) AMOUNT INTEREST_RATE DUE_DATE​` <br> e.g.,`loan 1 s 100.00 5 2030-12-31`||
| **Clear**  | `clear`                                                                                                                                                                                                    |
| **Delete** | `delete PERSON_INDEX`<br> e.g., `delete 3`<br> <br>`delete loan PERSON_INDEX LOAN_INDEX` <br> e.g., `delete loan 3 1`                                                                                      ||
| **Sort**   | `sort [s/PARAMETER] [o/ORDER]`<br> e.g., `sort s/AMOUNT o/ASC`                                                                                                                                             |
| **Pay**    | `pay PERSON_INDEX LOAN_INDEX AMOUNT`<br> e.g., `pay 1 1 1000`<br> <br> `pay PERSON_INDEX LOAN_INDEX MONTHS'M'`<br> e.g., `pay 1 1 5M` <br> <br> `pay PERSON_INDEX LOAN_INDEX all` <br> e.g., `pay 1 1 all` |
| **Filter** | `filter [INDEX] [pred/PREDICATE] ...`<br> e.g., `filter 3 pred/ amount > 500 pred/ loanType c`                                                                                                     |
| **Edit**   | `edit INDEX [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`<br> e.g.,`edit 2 n/James Lee e/jameslee@example.com`                                                                                |
| **Find**   | `find KEYWORD [MORE_KEYWORDS]`<br> e.g., `find James Jake`                                                                                                                                                 |
| **List**   | `list`                                                                                                                                                                                                     |
| **Help**   | `help`                                                                                                                                                                                                     |

---

## Appendix

---

## Glossary
- `predicate`: An argument that determines the parameter to use (in this case, what to filter by)
- `command terminal`: Called "Terminal" on both Windows and Mac, can be searched from the search bar
- `GUI`: Stands for "Graphical User Interface", essentially the parts of the application that you see
