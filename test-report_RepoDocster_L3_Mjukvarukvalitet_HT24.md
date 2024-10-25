# Test Report - RepoDocster App

- **Project**: Mjukvarukvalitet L3
- **Date**: 2024-10-25
- **Tester**: Mattias Ubbesen <mu222cu@student.lnu.se>

---

## **Manual Test Report**

### **Overview**

The following report summarizes the results from the manual testing of the RepoDocster App. Each main feature and interaction was tested, and covering both functional and user interface aspects. All tests passed successfully.

---

### **Test Summary**

1. **Application Start and UI Load**
   - **Objective**: Ensure the application loads correctly and displays all UI components as expected.
   - **Steps**:
     1. Start the application.
     2. Confirm that all UI components are visible and interactive.
   - **Result**: ✔️ Passed - Application loaded correctly with all UI components displayed as expected.

2. **GitHub Document Fetching**
   - **Objective**: Verify that documents can be fetched from GitHub based on user input.
   - **Steps**:
     1. Enter valid GitHub repository information.
     2. Submit the form to fetch documents.
   - **Result**: ✔️ Passed - Documents were fetched successfully from GitHub based on provided repository information.

3. **Form Input Validation**
   - **Objective**: Ensure form fields validate inputs correctly.
   - **Steps**:
     1. Enter invalid or missing data.
     2. Attempt submission and check for validation messages.
   - **Result**: ✔️ Passed - Validation messages displayed correctly for invalid/missing data.

4. **Display of Parsed Markdown Sections**
   - **Objective**: Confirm parsed document sections display correctly.
   - **Steps**:
     1. Fetch a README.md document.
     2. Verify that installation, usage, and other sections are displayed as expected.
   - **Result**: ✔️ Passed - Parsed sections displayed accurately, matching the structure of the markdown content.

5. **Error Handling and Messaging**
   - **Objective**: Ensure proper error handling for network and application errors.
   - **Steps**:
     1. Disconnect from the internet and attempt to fetch a document.
     2. Enter a non-existent repository and observe error messaging.
   - **Result**: ✔️ Passed - Error messages displayed appropriately for network issues and invalid repository entries.

6. **Toggle and Method Selection**
   - **Objective**: Verify that toggling options and selecting different methods works as expected.
   - **Steps**:
     1. Toggle options to bypass processors.
     2. Select various methods and confirm changes are reflected.
   - **Result**: ✔️ Passed - Toggle and method selections worked correctly, with UI updates reflecting user choices.

7. **Full Path and Owner/Repo Input Modes**
   - **Objective**: Ensure the application correctly switches between full path input and owner/repo input.
   - **Steps**:
     1. Switch between full path input and owner/repo fields.
     2. Verify the input mode is reflected in the application’s behavior.
   - **Result**: ✔️ Passed - The application switched between full path and owner/repo input modes as expected.

8. **Loading Indicators and Feedback**
   - **Objective**: Verify that the app provides feedback during loading and processing states.
   - **Steps**:
     1. Initiate document fetch and observe loading indicator.
     2. Ensure loading disappears once the fetch is complete.
   - **Result**: ✔️ Passed - Loading indicators displayed and disappeared appropriately.

9. **UI Responsiveness**
   - **Objective**: Ensure that the application is responsive across various screen sizes.
   - **Steps**:
     1. Resize browser window and observe UI.
     2. Confirm that UI components adjust layout accordingly.
   - **Result**: ✔️ Passed - The UI was responsive and adjusted correctly across different screen sizes.

---

### **Overall Results**

| **Test Case**                    | **Objective**                           | **Result** |
|----------------------------------|-----------------------------------------|------------|
| Application Start and UI Load    | Verify application loads UI correctly   | ✔️ Passed  |
| GitHub Document Fetching         | Test GitHub document fetch functionality| ✔️ Passed  |
| Form Input Validation            | Validate form fields for correct input  | ✔️ Passed  |
| Display of Parsed Markdown       | Confirm markdown sections display       | ✔️ Passed  |
| Error Handling and Messaging     | Test error handling and messaging       | ✔️ Passed  |
| Toggle and Method Selection      | Verify toggle and method selection      | ✔️ Passed  |
| Full Path/Owner-Repo Input Modes | Test input mode switching               | ✔️ Passed  |
| Loading Indicators               | Check for feedback during loading       | ✔️ Passed  |
| UI Responsiveness                | Ensure responsiveness across screen sizes | ✔️ Passed |

### **Conclusion**

All manual tests for RepoDocster have passed successfully.