# SLAM User Guide
Welcome to **SLAM**! **SLAM** is a desktop application for student group leaders in NUS to manage their group events, tasks, members and various activities. This application allows you to effectively plan and manage the organisation of events by allowing users to create and add such events to their schedule. Leading up to the actual date and time of the event, committee heads can add tasks (e.g. meetings, purchase of logistics) to complete under each event to keep track of progress. Group members can also be added and assigned to these tasks. This application uses a Command Line Interface (CLI); that is, the application is operated by typing commands into a Command Box.

---

# Table of Contents
1. [Quick Start](#1-quick-start)
2. [Navigating This Document](#2-navigating-this-document)
   1. [Events](#21-events)
   2. [Tasks](#22-tasks)
3. [General Commands](#3-general-commands)
   1. [Help](#31-help)
   3. [List all Events](#32-listing-events-tasks-or-members)
   2. [Exiting the program](#33-exiting-the-program)
4. [Event Commands](#4-event-commands)
   1. [Add an event](#41-add-an-event)
   2. [Select an event](#42-select-an-event)
   3. [Mark an event as done](#43-mark-an-event-as-done)
   4. [Mark an event as undone](#44-mark-an-event-as-undone)
   5. [Delete an event](#45-delete-an-event)
   10. [Delete all Events](#46-delete-all-events)
   6. [Find Event(s) based on keywords(s)](#47-find-events-based-on-keywords)
   8. [Display next upcoming Event](#48-display-next-upcoming-event)
   9. [Update an Event](#49-update-an-event)
5. [Task Commands](#5-task-commands)
   1. [Add a task](#51-add-a-task)
   2. [Select a task](#52-select-a-task)
   3. [Mark a task as done](#53-mark-a-task-as-done)
   4. [Mark a task as undone](#54-mark-a-task-as-undone)
   5. [Delete a task](#55-delete-a-task)
6. [Member Commands](#6-member-commands)
   1. [Add a member](#61-add-a-member)
   2. [Select a member](#62-select-a-member)
   3. [Delete a member](#63-delete-a-member)
7. [Saving the data](#7-saving-the-data)
8. [FAQ](#8-faq)
9. [Command summary](#9-command-summary)

---

## 1. Quick Start

1. Ensure that you have Java 11 or above installed on your computer.
2. Download the latest `.jar` file release of SLAM from [here](https://github.com/AY2122S1-CS2113T-W12-3/tp/).
3. Place the downloaded `.jar` file in the directory you intend to store **SLAM**’s data at.
4. Double-click the `.jar` file to launch the app. If double-clicking does not work, open the command prompt, navigate to the directory the file is located at, and enter the following command to launch the program:
```
 java -jar SLAM.jar
```
5. Congratulations! You are good to go. 

---

## 2. Navigating this document 
This document shows you the available features in **SLAM**, and provides you with the relevant commands to use them.

> 💡 **Notes about reading this document:**
> - Parameters that are supplied by the user are written in `UPPER_CASE`<br /> E.g. in `add -e n/TITLE`, a possible parameter for `TITLE` can be `Concert`
> - 🚨 **IMPORTANT** 🚨<br /> When inputting date & time as commands, the format should always be DD-mm-YYYY hhMM<br /> E.g. 31-12-2021 2359
    Since **SLAM** is an application revolving around the management of events, tasks and committee members, it is important to be aware of the respective details that **SLAM** can use in managing the overall catalog.

### 2.1 Events
The following two tables show the fields which **SLAM** works with in managing events in the overall catalog.

| **Required Fields** | **Description**                  |
| ------------------- | -------------------------------- |
| Title | The title of the event                         |
| Date & Time | The date and time the event is happening | 
| Venue | The venue at which the event is happening      |
| Budget | The amount of budget allocated to the event   |

| **Optional Fields** | **Description**                  |
| ------------------- | -------------------------------- |
| Description | A brief description of the event         |

### 2.2 Tasks
The following two tables show the fields which **SLAM** works with in managing the tasks you can add and keep track of under each event created.

| **Required Fields** | **Description**                   |
| ------------------- | --------------------------------- |
| Title | The title of the task                           |
| Deadline | The deadline the task has to be completed by |

| **Optional Fields** | **Description**                 |
| ------------------- | ------------------------------- |
| Description         | A brief description of the task |


[Back to table of contents](#table-of-contents)

---

## 3. General Commands
This section contains the general basic commands for **SLAM**.

### 3.1 Help 
This allows you to quickly view all the available commands and how to use them, all in one place.

**Format:** `help`

### 3.2 Listing Events, Tasks or Members
You may use this feature of **SLAM** to view the desired selection of your **SLAM** database. 

You may choose to view all your scheduled `events` in SLAM. SLAM sorts this chronologically for you so you don't have to. 

**Format:** `list -e`

**Example:** 
```
> list -e
```

```
OVERALL SCHEDULE
=======================
1. [E][ ] Tembusu Concert (at: 19 Feb 2022 - 20:00)
2. [E][ ] Faculty Funfair (at: 20 Mar 2022 - 16:00)

FURTHER COMMANDS
-----------------------
To list Task: list [Event Index] -t
To list Members of a Task: list [Event Index] t/[Task Index]
--------END OF LIST-----------
```

💡 `list` can also be used to display all members in your current roster. 

**Format:** `list -m`

**Example:** 
```
> list -m
```

```
List of members in MemberRoster
1. JOHN DOE
2. JANE DOE
--------END OF LIST-----------
```

💡 You may also choose to view all the `tasks` you have assigned to any specified event.

**Format:** `list -t EVENT_INDEX`

**Example:** `list -t 1`

**Expected Output:** 
```
> list 1 -t
```
```
Event: Tembusu Concert
========================
1. [T][X] Buy stage lights (by: 10 Feb 2022 - 22:00)
2. [T][ ] Stage layout meeting (by: 12 Feb 2022 - 20:00)
--------END OF LIST-----------
```

💡 **SLAM** also allows you to choose to **view all the assigned members for a particular task** too.

**Format:** `list -m e/EVENT_INDEX t/TASK_INDEX`

**Example:** `list -m e/1 t/1`

**Expected Output:**
```
Event: Tembusu Concert
Task: Buy stage lights
=======================
1. JOHN DOE
2. JANE DOE
--------END OF LIST-----------
```

### 3.3 Exiting the program
This allows you to safely terminate the program.

**Format:** `bye` 

[Back to table of contents](#table-of-contents)

---

## 4. Event Commands
This section contains the available commands to manage events in **SLAM**.

### 4.1 Add an Event
Adds an event to your current catalog of events.

To add an event, first describe the event using the following command:

**Format:** `add -e n/TITLE d/DATE_&_TIME v/VENUE b/BUDGET`

**Example:** `add -e n/Tembusu Concert d/19-02-2022 2000 v/MPH b/1000`

Following which, **SLAM** will prompt you for an optional description for your event which should look like this:

```
> add -e n/Tembusu Concert d/19-02-2022 2000 v/MPH b/1000
```
```
Please add an optional description for your item and press enter.
```
```
>
```
Key in your description and press `enter`, or just press `enter` if you have none. You have successfully added an event into **SLAM**!

### 4.2 Select an Event
Selects an Event to view its details. You can then perform additional commands with the selected Event.

**Format:** `select -e EVENT_ID`

**Example:** `select -e 1`

**Expected Output:**
```
> select -e 1
```
```
Here are the details of the event:
Title: Tembusu Concert
Date: 19 Feb 2022 - 20:00
Description: Semesterly Arts Week Fundraiser
Venue: MPH
Budget: $1000.0
Tasks:
1. Buy stage lights
```

> 💡 The `select` command is especially useful to keep in mind! An event needs to be selected before any changes to its tasks can be done.
>
> See how to [Select a Task](#52-select-a-task).


### 4.3 Mark an Event as `done`
This will allow you to mark an event as done after the event is over. 

**Format:** `done -e EVENT_ID`

**Example:** `done -e 1`

**Expected Output:**
```
> done -e 1
```
```
Nice! I have marked these items as done!
[E][X] Tembusu Concert (at: 19 Feb 2022 - 20:00)
--------LIST UPDATED--------
```

### 4.4 Mark an Event as `undone`
This will allow you to undo an event that was marked done if the event is not over yet.

**Format:** `undo -e EVENT_ID`

**Example:** `undo -e 1`

**Expected Output:**
```
Ok, I have unmarked these items:
[E][ ] Tembusu Concert (at: 19 Feb 2022 - 20:00)
--------LIST UPDATED--------
```

### 4.5 Delete an Event
Deletes an event from the list.

**Format:** `delete -e EVENT_ID`

**Example:** `delete -e 1`

> 🚨 If you choose to `delete` an event, all of its associated tasks will be deleted too.

**Expected Output:**
```
> delete -e 1
```
```
This event has been removed: Tembusu Concert
```
### 4.6 Delete all Events
This allows you to delete all events, tasks and members.

> 🚨 As this will affect all your data, please make sure you want to delete everything before proceeding. The program will delete everything once the command is entered!

**Format:** `delete all`

After entering `delete all`, this is what you will see:

```
> delete all

I have deleted everything!
```
> 🚨 This action is irreversible!

### 4.7 Find Event(s) based on keyword(s)
Finds one or more Event(s) that matches the keyword(s) that you enter.

**Format** `find -e KEYWORD [KEYWORDS]`

**Expected Output:**
```
> find -e Concert
```
```
Here are are the events found:
1. Tembusu Concert
```
> 💡 You can only find Events with this command. After finding the Event(s) of your choice, you could use `select` to further see the details of the event's tasks, and `select` again for a particular task's member.
>
> See how to [Select a task](#52-select-a-task) and [Select a member](#62-select-a-member).


### 4.8 Display next upcoming Event
The next command displays to you the next upcoming event or task of an event on the calendar

To display the next upcoming event we key in `next -e`

**Format:** `next -e`

**Expected Output:**
```
> next -e
```
```
Title: Tembusu Concert
Date: 19 Feb 2022 - 20:00
Description: Semesterly Arts Week Fundraiser
Venue: MPH
Budget: $1000.0
Tasks:
1. Buy stage lights
```

To display the next upcoming task we key in `next -e EVENT_ID`

**Format:** `next -t EVENT_ID`

**Expected Output:**
```
> next -t 1
```
```
Title: Buy stage lights
Date: 10 Feb 2022 - 22:00
Description: Stage lights for concert
Members:
1. JOHN DOE
```
### 4.9 Update an Event
The Update command can be used to update details of events and tasks

> 🚨 Any updates made is irreversible! So make updates with caution.

To begin the update process we first key in `update EVENT_ID`

**Format:** `update EVENT_ID`

**Expected Output:**
```
> update 3
```
```
Here are the details of the event:
======================================
Title: Tembusu Concert
Date: 19 Feb 2022 - 20:00
Description: Semesterly Arts Week Fundraiser
Venue: MPH
Budget: $1000.0
Tasks: 
1. [T][X] Buy stage lights (by: 10 Feb 2022 - 22:00)
2. [T][ ] Stage layout meeting (by: 12 Feb 2022 - 20:00)
_________________________________________________________________________________
Please type the item you would like to update in the following manner 
-----------------------------------------------------------------------   
n/[NEW NAME]   
d/[NEW DATE[d/dd-MM-yyyy HHmm]]
p/[NEW DESCRIPTION]
v/[NEW VENUE]
b/[NEW BUDGET]
t/[TASK NUM YOU WANT TO UPDATE]
Only type a singular update at given time!
Only the first command will be updated if multiple updates are written
_________________________________________________________________________________
```
We can then update the detail of the specifc event by following the list of commands below to update. We can update multiple in a single like by seperating each item by a `>`.

1. `title/NEW_NAME` to update the title of the event
2. `date/[dd-MM-yyyy HHmm]` to update the date of the event
3. `description/[NEW DESCRIPTION]` to update the description of the event
4. `venue/[NEW VENUE]` to update the venue of the event
5. `budget/[NEW BUDGET]`to update the budget of the event
6. `task/[TASK NUM YOU WANT TO UPDATE]` to update information on the task attached to these events

We can then update the detail of the specifc task by keying in `task/[TASK NUM YOU WANT TO UPDATE]` in this segment.

**Expected Output:**
```
> t/1
```
```
Title: Buy stage lights
Deadline: 10 Feb 2022 - 22:00
Description: Stage lights for concert
Members: 
1. JOHN DOE
____________________________________________________________________________________
Please type the item for task you would like to update in the following manner 
-----------------------------------------------------------------------
n/[NEW NAME]   
d/[NEW DATE[d/dd-MM-yyyy HHmm]]
p/[NEW DESCRIPTION]
member/[MEMBER INDEX]
remove/[MEMBER INDEX]
To add a member to a task, enter 'add'

Only type a singular update at given time!
Only the first command will be updated if multiple updates are written
____________________________________________________________________________________
```
We can then update the details of the specifc task by following the list of commands below to update. We can update multiple in a single like by seperating each item by a `>`.

1. `n/[NEW NAME]` to update the title of the event
2. `d/[NEW DATE[d/dd-MM-yyyy HHmm]]` to update the date of the event
3. `p/[NEW DESCRIPTION]` to update the description of the event
4. `member/[MEMBER INDEX]` to change a member assigned to this task
5. `remove/[MEMBER INDEX]` to remove a member assigned to this task
6. `add` to assign a member to this task

[Back to table of contents](#table-of-contents)

---

## 5. Task Commands
This section contains the available commands for managing tasks for events in **SLAM**. Because all tasks belong to a specific event in your catalog, an event must first be selected ([see Section 4.2 on Selecting Events](#42-select-an-event)) before any of the below commands can be used.

### 5.1 Add a task 
Note: For this current version of **SLAM**, pre-selecting an `Event` is not required for this command.

**Prerequisite:** You must have added at least one event and at least one member before adding a task.

Adds a task to an existing event in your current catalog of events.

To add a task, first describe the task using the following command:

**Format:** `add -t n/TITLE d/DATE_&_TIME`

**Example:** `add -t n/Buy stage lights d/10-11-2021 1600`

Following which, **SLAM** will prompt you for an optional description for your task which should look like this:

```
> add -t n/Buy stage lights d/10-02-2022 1600
```
```
Please add an optional description for your item and press enter
```
```
>
```
After pressing `enter`, **SLAM** will prompt you to select an event to assign your task to. Enter the number corresponding to the event:
```
Please choose which event you want to add your task to.
1. [E][ ] Tembusu Concert (at: 19 Feb 2022 - 20:00)
```
```
> 1
```
After pressing `enter` again, **SLAM** will prompt you to select members to assign your task to. You may choose to select multiple members:
```
Please choose which member(s) you want to assign your task to. 
1. AL
2. BOB
3. CHARLIE
```
```
> 1 2
```
After pressing `enter` for the last time, you have keyed in your description, event and member(s). You have successfully added a task into **SLAM**! 

### 5.2 Select a Task
Select a Task to view its details. You can then perform additional commands with the selected Task.

**Format**: `select -t TASK_ID`

**Example**: `select -t 1`

> 🚨 You need to `select` an Event before selecting the task of your choice!

**Expected Output**:
```
> select -t 1
```
```
Here are the details of the task:
Title: Buy stage lights
Deadline: 10 Feb 2022 - 16:00
Description: Stage lights for concert
Members:
1. JOHN DOE
```

> 💡 You can use `select` again to view the details of the Task's `Member`. See [Select a Member](#62-select-a-member).

### 5.3 Mark a Task as `done`

This will allow you to mark a task as done after the task is accomplished.

**Format:** `done -t TASK_ID`

**Example:** `done -t 1`

> 🚨 You need to `select` an Event before marking the task of your choice as done!

**Expected Output:**
```
> done -t 1
```
```
Nice! I have marked these items as done!
[T][X] Buy stage lights (at: 10 Feb 2022 - 16:00)
--------LIST UPDATED--------
```

### 5.4 Mark a Task as `undone`

This will allow you to undo a task that was marked done if the task is not done yet.

**Format:** `undo -t TASK_ID`

**Example:** `undo -t 1`

> 🚨 You need to `select` an Event before undoing the task of your choice!

**Expected Output:**
```
Ok, I have unmarked these items:
[T][ ] Buy stage lights (at: 10 Feb 2022 - 16:00)
--------LIST UPDATED--------
```

### 5.5 Delete a Task
Deletes a task from an `Event`.

**Format**: `delete -t TASK_ID`

**Example**: `delete -t 1`

> 🚨 You need to `select` an Event before deleting the task of your choice!

**Expected output**: (after entering `select -e 1` for example)
```
> delete -t 1
```
```
This task has been removed: Buy stage lights
```

[Back to table of contents](#table-of-contents)

---

## 6. Member Commands
This section contains the available commands for managing members in `SLAM`.

### 6.1 Add a member 

Adds a member to your current member roster.

**Format:** `add -m`

**Example:** `add -m John Doe, Bob Tan`

> 💡 You can use a comma and a space to separate different members you want to add, if you choose to add more than one member at a time.

### 6.2 Select a member
Selects a member to view what tasks the member is assigned to.

**Format**: `select -m MEMBER_NAME`

**Example**: `select -m JOHN DOE`

**Expected Output**:
```
> select -m JOHN DOE
```
```
Here are the details of the member:
JOHN DOE
[T][ ] Buy stage lights (by: 10 Feb 2022 - 22:00)
```

> 💡 You can use `list -m` to first list all the members, then select the member based on name. See [Listing Events, Tasks or Members](#32-listing-events-tasks-or-members).

### 6.3 Delete a member
Deletes a member. This will also remove the member from all tasks the member is assigned to.

**Format**: `delete -m MEMBER_NAME`

**Example**: `delete -m JOHN DOE`

**Expected Output**:
```
> delete -m JOHN DOE
```
```
This member has been removed: JOHN DOE
```

> 🚨 A task must have at least one `Member`.
> 
> If the `Member` you choose to delete is the only `Member` assigned to a task, you will have to assign more members to that particular task first before you can delete the `Member`!

In this case, you will be prompted to add more members to the tasks that only has that member assigned to it. This is what you may see:
```
Please assign more members to these tasks:
[Event: Tembusu Concert; Task: Buy stage lights]
```

[Back to table of contents](#table-of-contents)

---

## 7. Saving the Data
**SLAM** data is saved in the hard disk automatically after you exit the program. There is no need to save manually.

> 🚨 WARNING: Do not edit this save file! It might cause the save data to be corrupt and cause errors when starting **SLAM** again.

[Back to table of contents](#table-of-contents)

---

## 8. FAQ

>**Q**: How do I transfer my data to another computer? 
>
>**A**: You can transfer your data to another computer by copying the `data` folder found in the directory where **SLAM** was used, and pasting it in the directory of the device where **SLAM** is intended to be run.

[Back to table of contents](#table-of-contents)

---

## 9. Command Summary

### General commands

| **Command**               | **Format**                                          |
|---------------------------|-----------------------------------------------------|
| Display user manual       | `help`                                              |
| List events/members/tasks | For events: `list`<br />For tasks: `list EVENT_INDEX -t`<br />For members: `list -m`<br />For members assigned to a task: `list EVENT_INDEX t/TASK_INDEX`|
| Exit program              | `bye`                                               |
| 

### Event commands

| **Command**           | **Format**                                          |
|-----------------------|-----------------------------------------------------|
| Add an event          | `add -e n/TITLE d/dd-MM-yyyy HHmm v/VENUE b/BUDGET` |
| Delete an event       | `delete -e INDEX`                                   |
| Delete all events     | `delete all`                                        |
| Select an event       | `select -e INDEX`                                   | 
| Find event(s)         | `find EVENT_KEYWORD(S)`                             |
| Mark event as done    | `done -e INDEX`                                     | 
| Un-mark event as done | `undo -e INDEX`                                     |
| Update an event       | `update INDEX`                                      |
| Next event            | `next -e`                                           |

### Task commands

| **Command**           | **Format**                    |
|-----------------------|-------------------------------|
| Add a task            | `add -t n/TITLE d/dd-MM-yyyy` |
| Delete a task         | `delete -t INDEX`             | 
| Select a task         | `select -t INDEX`             |
| Mark a task as done   | `done -t INDEX`               |
| Un-mark a task as done| `undo -t INDEX`               |
| Next task             | `next -t`                     |

### Member commands

| **Command**     | **Format**              |
|-----------------|-------------------------|
| Add a member    | `add -m MEMBER NAME`    | 
| Delete a member | `delete -m MEMBER NAME` |
| Select a member | `select -m MEMBER NAME` | 

[Back to table of contents](#table-of-contents)
