# Test Report

- Project: Mjukvarukvalitet L3
- Date: 2024-10-24
- Name: Mattias Ubbesen <mu222cu@student.lnu.se>

## **Test Results**

### **MarkdownParser Test Suite**

- Total Tests: 10
  - ✔️ should read and parse hash-style markdown content
  - ✔️ should return the correct title from hash-style markdown
  - ✔️ should read and parse underline-style markdown content
  - ✔️ should count headings by level in underline-style markdown
  - ✔️ should read and parse markdown content (combination of notations)
  - ✔️ should return the correct title from combination markdown
  - ✔️ should count headings by level from combination markdown
  - ✔️ should return the count of headings for a specific level from combination markdown
  - ✔️ should return sections with matching heading keyword from combination markdown
  - ✔️ should throw an error if no sections match the keyword from combination markdown

### **RepoReadmeProcessor Test Suite**

- Total Tests: 8
  - ✔️ should extract installation instructions
  - ✔️ should extract usage examples
  - ✔️ should extract API documentation
  - ✔️ should extract configuration information
  - ✔️ should extract dependencies list
  - ✔️ should extract contribution guidelines
  - ✔️ should extract license information
  - ✔️ should extract the project title and description

#### **NpmReadmeProcessor Test Suite**

- Total Tests: 3
  - ✔️ should extract CLI usage information
  - ✔️ should extract versioning details
  - ✔️ should extract scripts information

#### **ChangelogProcessor Test Suite**

- Total Tests: 9
  - ✔️ should extract unreleased changes
  - ✔️ should extract added features
  - ✔️ should extract changed features
  - ✔️ should extract deprecated features
  - ✔️ should extract removed features
  - ✔️ should extract bug fixes
  - ✔️ should extract security updates
  - ✔️ should get updates between two close versions 2.2.1 and 2.2.0
  - ✔️ should throw error if no updates found between two versions

  ### **MarkdownParser - Dictionary Methods Test Suite**

- Total Tests: 3
  - ✔️ should return the dictionary object
  - ✔️ should return keywords for a specific section type (1 ms)
  - ✔️ should add a keyword to a section type

### **Coverage Summary**

| **File**               | **Statements** | **Branches** | **Functions** | **Lines** | **Uncovered Lines**                                         |
| ---------------------- | -------------- | ------------ | ------------- | --------- | ----------------------------------------------------------- |
| **All files**          | **85.52%**     | **65%**      | **100%**      | **85.9%** |                                                             |
| ChangelogProcessor.ts  | 96.15%         | 72.72%       | 100%          | 96.15%    | 133                                                         |
| HeadingDictionary.ts   | 71.42%         | 42.85%       | 100%          | 71.42%    | 61-64, 98                                                   |
| MarkdownParser.ts      | 82.02%         | 67.34%       | 100%          | 82.75%    | 77, 82, 98, 126, 148-153, 236, 259, 310, 324, 355, 400, 424 |
| NpmReadmeProcessor.ts  | 100%           | 66.66%       | 100%          | 100%      | 35, 44                                                      |
| RepoReadmeProcessor.ts | 93.75%         | 57.14%       | 100%          | 93.33%    | 126                                                         |

## **Summary**

- **Test Suites:** 4 passed, 4 total
- **Tests:** 36 passed, 36 total
- **Snapshots:** 0 total
- **Time:** 1.503 s
- **Ran all test suites**
