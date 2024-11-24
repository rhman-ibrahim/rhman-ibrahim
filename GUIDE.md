## Overview

This documentation serves as the central reference for all of my projects documentations. By adhering to a consistent structure across all projects, it ensures clarity and ease of use and provides both high-level overviews and in-depth technical knowledge, catering to individuals with diverse backgrounds and expertise.

## Structure

In order to cater to various levels of understanding and technical needs, I have created a two-part documentation structure **README** and **Schema** with different purposes and structures. **README** focuses on explaining the project conceptually, outlining its workflow, detailing the project structure, and providing instructions for setup and usage through the following sections: **Overview**, **Structure**, **Workflow**, and **Guide**. The **Structure** sections consists of 2 sections ***File System*** and ***Index*** each list the project directories and files differently.

***File System*** lists the project using the [tree](https://launchpad.net/ubuntu/+source/tree) command with variations according to the project nature as: `tree --dirsfirst` to list directories before files, `tree -I "venv" --prune --dirsfirst` for Python projects and `tree -I "node_modules" --prune --dirsfirst` for JavaScript projects. While ***Index*** is a table that lists directories and files according the *tree* command ordering through this columns: ***#*** the directory/file order, ***Directory/File*** the directory/file name, ***Description*** the directory/file name role, and ***Index*** the directory/file section in **Schema**.

|section|Description|Order|
|--|--|--|--|
|Overview|A short paragraph describing the project as an idea and the purpose behind it, or the problem it addresses.|1|
|Structure|Explains how the project's files are organized, it provides detailed descriptions for each directory and file.|2|
|File System|The output of the tree command that displays an indented directory tree of the project's files.|2.1|
|Index|A table listing the project directory and files according to tree command ordering.|2.2|
|Workflow|Explains the project conceptually as a story.|3|
|Guide|Acts as footnotes|4|

## README Notes

- Use the template below to create a **README**
- All sections must be included. If a section is not required, replace its content with a blockquote declaring this message: This section is not applicable to this project.
  
```md
# PROJECT_NAME

    1. [Overview](#overview)
    2. [Structure](#structure)

        - [File System](#file-system)
        - [Index](#index)

    3. [Workflow](#workflow)
    4. [Guide](#guide)

## Overview

`REPLACE_ME_WITH_OVERVIEW_CONTENT`

> Reviewing this [document](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/Documentation-Guide) may help with understanding and navigating through this document easily.

## Structure

### File System

`REPLACE_ME_WITH_FILE_SYSTEM_CONTENT`

### Index

`REPLACE_ME_WITH_INDEX_CONTENT`

## Workflow

`REPLACE_ME_WITH_WORKFLOW_CONTENT`

## Guide

`REPLACE_ME_WITH_GUIDE_CONTENT`

```

### Index Table Notes

- The *Directory/File* column values must be formatted as links that navigate to the corresponding section in **Schema**, as `[module-name](Schema.md#1234)` if its index is `1.2.3.4`
- Directories' names must end with a `/`, while file names must end with their extension.
- Even if the directory has a single file, each of the directory and the file must have a row in the table.

## Schema Notes

- Use the template below to create a **SCHEMA**
- **Schema** sections must be in order and its respecting heading nesting.
- Replace these ***PROJECT_NAME*** and ***PROJECT_NAME_REPOSITORY_LINK*** with their actual values.

```md
# PROJECT_NAME

This is the Schema of [PROJECT_NAME](PROJECT_NAME_REPOSITORY_LINK) please review the **README** first before reading the Schema.

## 1

### 1.2

#### 1.2.1

#### 1.2.2

# 2

# 3

## 3.1

## 3.2

# 4

# 5

```
