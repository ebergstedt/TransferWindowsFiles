# Automatic Windows File Manager
Simple windows file management program with logging and json configuration. 

**Automatic Windows File Manager** is a lightweight background program that will handle day to day file transfers without the need for a monolith backup service or paid equivalent.

You should probably [schedule it as a background service](http://windows.microsoft.com/en-au/windows/schedule-task#1TC=windows-7).

# Features

It can do the following operations for your files, running automatically in the background if you set it as a background service.

* **Move files** 
* **Copy files** 
* **Delete files** 

You idenfity files by filtering on your own **globpattern**.

Configuration is done in a simple **json** file.

Events are **logged** so you can identify errors and stuff that happened.

# Glob?

Glob is used to identify files, and is a simplification of regex. Here's an introduction guide: [glob (programming)](https://en.wikipedia.org/wiki/Glob_(programming))

# Configuration

You configure the program within the **config.json** file that is in the root folder.

There are three types of operations you can apply on your files:  **Move**, **Copy** and **Delete**.

## Move

**Move** will remove files from the Source folder and put them in the Target folder.

| Name                             | Type   | Required | Description                                                                      |
|----------------------------------|--------|----------|----------------------------------------------------------------------------------|
| Source                           | String | Yes      | Directory path to move files from.                                               |
| Target                           | String | Yes      | Directory path to move files into.                                               |
| GlobPattern                            | String | Yes      | GlobPattern to identify files.                                                         |
| ReplaceTargetFileIfAlreadyExists | Bool   | No       | If files that already exists should be deleted (in order to update them) or not. Default value is **false**. |
| Operation                        | String | Yes      | Must be "Move"                                                                           |

## Copy

**Copy** will copy files from the Source folder and put the copy in the Target folder.

| Name                             | Type   | Required | Description                                                                      |
|----------------------------------|--------|----------|----------------------------------------------------------------------------------|
| Source                           | String | Yes      | Directory path to copy files from.                                               |
| Target                           | String | Yes      | Directory path to copy files into.                                               |
| GlobPattern                            | String | Yes      | GlobPattern to identify files.                                                         |
| ReplaceTargetFileIfAlreadyExists | Bool   | No       | If files that already exists should be deleted (in order to update them) or not. Default value is **false**. |
| Operation                        | String | Yes      | Must be "Copy"                                                                           |

## Delete

**Delete** will remove files from a folder.

| Name      | Type   | Required | Description                        |
|-----------|--------|----------|------------------------------------|
| Source    | String | Yes      | Directory path to delete files from. |
| GlobPattern     | String | Yes      | GlobPattern to identify files.           |
| Operation | String | Yes      | Must be "Delete"                             |

### Example: 

The first operation will take all chrome downloaded files with the .mp4 extension and move (cut and paste) to a youtube folder on google drive.

The second operation will copy your text files from your documents folder to a backup documents folder on google drive.

The third operation will empty your Trash folder.

You can of course add more as you wish!

**config.json**
```json
{
  "FileOperations": [
    {
      "Source": "E:\\Chrome Download",
      "Target": "E:\\Google Drive\\Youtube",
      "GlobPattern": "*.mp4",
      "ReplaceTargetFileIfAlreadyExists": false,
      "Operation": "Move"
    },
    {
      "Source": "E:\\Documents",
      "Target": "E:\\Google Drive\\Documents",
      "GlobPattern": "*.txt",
      "ReplaceTargetFileIfAlreadyExists": false,
      "Operation": "Copy"
    },
    {
      "Source": "E:\\Trash",
      "GlobPattern": "*",
      "Operation": "Delete"
    }
  ]
}
```

# Logs

Logs will be created in the /logs folder with a timestamp and a description of what the program has done. Use this for searching for errors.

# Todo

Test

# License

The MIT License (MIT)

Copyright (c) 2016 Erik Bergstedt

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.