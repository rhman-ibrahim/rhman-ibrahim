# The Documentations Reference

1. [Overview](#overview)
2. [Structure](#structure)

    - [File System](#file-system)
    - [Index](#index)

3. [Workflow](#workflow)
4. [Guide](#guide)

## Overview

This documentation serves as the central reference for all projects under the GitHub username **rhman-ibrahim** and the Petrichor project. By adhering to a consistent structure across all projects, it ensures clarity and ease of use and provides both high-level overviews and in-depth technical knowledge, catering to individuals with diverse backgrounds and expertise.

## Structure

1. ### README

    Focuses on explaining the project conceptually, outlining its workflow, detailing the project structure, and providing instructions for setup and usage. It consists of the following sections and sub-sections:

    1. Overview
    2. Structure
        - File System
        - Index
    3. Workflow
    4. Guide

2. ### Schema

    Offers an in-depth explanation of each module, discussing their functionalities and relationships in detail. Its sections vary based on the project's nature, but their links must always be provided in the [README](#readme) Structure/Index.

## Workflow

1. ### The Overview Section

    The overview is a short paragraph describing the project as an idea and the purpose behind it, or the problem it addresses.

2. ### The Structure Section

    The structure section explains how the project's files are organized. It provides detailed descriptions for each directory and file. This section includes two parts: ***File System*** and ***Index***.

   - #### File System

        The file system is the output of the [`tree`](https://launchpad.net/ubuntu/+source/tree) command that displays an indented directory tree of the project's files.

        **Example:**

        ```bash
        .
        ├── directory1/
        │   ├── directory2/
        │   │   ├── file1.extension1
        │   │   ├── file2.extension2
        │   ├── file3.extension3
        ├── directory3/
        │   ├── file4.extension3
        └── file5.extension4
        ```

   - #### Index

        The index is a table with the following columns: *#: the order in the project's file system*, *File/Directory: the directory/file name*, *Description: the role of the directory/file*, and *Index: the order of the file in the **Schema**'s documentation*.

        **Example:**

        |#|Directory/File|Description|Index|
        |----|----|----|----|
        |01|directory1/|*Contains files and subdirectories for module 1.* | 1      |
        |02|directory1/directory2/|*Subdirectory within directory1 containing files related to functionality A.*|1.1|
        |03|directory1/directory2/file1.extension1|*File for functionality A1.*|1.1.1|
        |04|directory1/directory2/file2.extension2|*File for functionality A2.*|1.1.2|
        |05|directory1/file3.extension3|*Main configuration file for module 1.*|1.2|
        |06|directory3/|*Contains files related to module 2.*|2|
        |07|directory3/file4.extension3|*File for functionality B.*|2.1|
        |08|file5.extension4|*Standalone file for functionality C.*|3|

3. ### The Workflow Section

    The workflow is an extended explanation of how the project works as a story.

    **Example:**

    > This application begins by authenticating the user. After login, users can upload files, which are stored securely in the cloud. These files can be organized into folders for easy management.

4. ### The Guide Section

    The guide consists of multiple custom sections depending on the documentation needs. Each must have a proper heading.

## Guide

1. ### Mentioning the reference

    This documentation has to be mentioned as a reference in each documentation following it as a blockquote paragraph in the [overview](#overview) section.

    Blockquote message:

    ```Reviewing this [document](https://github.com/rhman-ibrahim/rhman-ibrahim/blob/main/DOCUMENTATION_GUIDE) may help with understanding and navigating through this document easily.```

2. ### If there is no need for a certain section

    All sections must be included. If a section is not required, replace its content with a blockquote declaring this message:  
    **This section is not applicable to this project.**

3. ### Index Table Notes

    - The *Directory/File* column values must be formatted as links that navigate to the corresponding section in [Schema](Schema.md), as `[module-name](Schema.md#-1234---module-title)` if its index is `1.2.3.4`
    - Directories' names must end with a `/`, while file names must end with their extension.
    - Even if the directory has a single file, each of the directory and the file must have a row in the table.

4. ### The Schema Documentation

    While its sections vary according to the project's nature, they must be indexed as the index column states. ***Following the [workflow](#the-workflow-section)*** table, heading levels must match the nesting depth in the file system.

    **Example:**

    ```md
    # Project's Name
    ## 1 - Directory1
    ### 1.1 - Directory2
    #### 1.1.1 - File1 (File1.extension1)
    #### 1.1.2 - File2 (File2.extension2)
    ### 1.2 - File3 (File3.extension3)
    ## 2 - Directory3
    ### 2.1 - File4 (File4.extension3)
    ## 3 - File5 (File5.extension4)
    ```
