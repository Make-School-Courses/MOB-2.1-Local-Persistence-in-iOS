# MOB-2.1 - Local Persistence in iOS

## Course Description

This courses covers how and why to persist data in mobile development. We will learn the various options for saving data locally in iOS including Core Data, Realm, NSCoder, UserDefaults, and Keychain.  Understand best practices in storing and retrieving sensitive data and how to work with the iOS file system.


## Course Specifics

Weeks to Completion:  7 <br>
Total Seat Hours:  37.5 hours <br>
Total Out-of-Class Hours: 75 hours <br>
Total Hours: 112.5 hours <br>
Units:  3 units <br>
Delivery Method:  Residential <br>
Class Sessions:  14 classes, 7 labs

## Prerequisites:  

- [MOB 1.3](https://github.com/Make-School-Courses/MOB-1.3-Dynamic-iOS-Apps)
- [BEW 1.3](https://github.com/Make-School-Courses/BEW-1.3-Server-Side-Architectures-and-Frameworks)

## Learning Outcomes

Students by the end of the course will be able to ...

1. Build apps that store information locally on an iOS device
1. Identify various ways of storing persistent information in iOS
1. Compare and contrast various persistence options such as Core Data, Realm, NSCoder, UserDefaults, Keychain and chose the best options for their project.
1. Use the built in persistence mechanisms in iOS as well as some third party options for persistence
1. Store and retrieve sensitive information in iOS.
1. Discover, learn and understand the iOS filesystem.

## Lessons

### **[INSTRUCTOR NOTE: PLEASE REMOVE THIS BEFORE APRIL 1]**
If you teach **M/W** or **Tu/Th**, please pick from a template below and delete the other one

---
### M/W Template **[PLEASE REMOVE THIS HEADER BEFORE APRIL 1]**
**Course Dates:** Monday, April 1 – Wednesday, May 15, 2019 (7 weeks)

**Class Times:** Monday and Wednesday at 3:30–5:20pm (14 class sessions)

| Class |          Date          |                 Topics                  |
|:-----:|:----------------------:|:---------------------------------------:|
|  1 |  Monday, April 1                         | [Introduction to Persistence Technologies in iOS] |
|  2 |  Wednesday, April 3                      | [UserDefaults, Keychain and NSCoding] |
|  3 |  Monday, April 8                         | [The iOS FileSystem - Introduction] |
|  4 |  Wednesday, April 10                     | **NO LESSON]: The iOS FileSystem - Use cases and applications** |
|  5 |  Monday, April 15                        | [CoreData - Introduction] |
|  6 |  Wednesday, April 17                     | **[NO LESSON]: CoreData - Use cases and drawbacks** |
|  7 |  Monday, April 22                        | [CoreData - Relationships and Heirarchies] |
|  8 |  Wednesday, April 24                     | [CoreData - Using multiple contexts and child contexts] |
|  9 |  Monday, April 29                        | [CoreData - Retrieving information from the stack] |
| 10 |  Wednesday, May 1                        | [Third Party Persistence Options - Realm] |
| 11 |  Monday, May 6                           | **[NO LESSON]** |  
| 12 |  Wednesday, May 8                        | **[NO LESSON]** |
| 13 |  Monday, March 13                        | Final Class (presentations, etc) |
| 14 |  Wednesday, March 15                     | Final Exams/Presentations |

### Tu/Th Template **[PLEASE REMOVE THIS HEADER BEFORE APRIL 1]**
**Course Dates:** Tuesday, April 2 – Thursday, May 16, 2019 (7 weeks)

**Class Times:** Tuesday and Thursday at 3:30–5:20pm (14 class sessions)

| Class |          Date          |                 Topics                  |
|:-----:|:----------------------:|:---------------------------------------:|
|  1 |  Tuesday, April 2                        | [Introduction to Persistence Technologies in iOS] |
|  2 |  Thursday, April 4                       | [UserDefaults, Keychain and NSCoding] |
|  3 |  Tuesday, April 9                        | [The iOS FileSystem - Introduction] |
|  4 |  Thursday, April 11                      | **[NO LESSON]: The iOS FileSystem - Use cases and applications** |
|  5 |  Tuesday, April 16                       | [CoreData - Introduction] |
|  6 |  Thursday, April 18                      | **[NO LESSON]: CoreData - Use cases and drawbacks** |
|  7 |  Tuesday, April 23                       | [CoreData - Relationships and Heirarchies] |
|  8 |  Thursday, April 25                      | [CoreData - Using multiple contexts and child contexts] |
|  9 |  Tuesday, April 30                       | [CoreData - Retrieving information from the stack] |
| 10 |  Thursday, May 2                         | [Third Party Persistence Options - Realm] |
| 11 |  Tuesday, May 7                          | **[NO LESSON]** |  
| 12 |  Thursday, May 9                         | **[NO LESSON]** |  
| 13 |  Tuesday, March 14                       | Final Class (presentations, etc) |
| 14 |  Thursday, March 16                      | Final Exams/Presentations |

[Introduction to Persistence Technologies in iOS]: Lessons/00-Intro-to-Persistence-Technologies/Readme.md
[UserDefaults, Keychain and NSCoding]: Lessons/01-UserDefaults-Keychain-NSCoding/Readme.md
[The iOS FileSystem - Introduction]: Lessons/02-FileSystem/Readme.md
[Lesson 4]: Lessons/Lesson4.md
[CoreData - Introduction]: Lessons/04-Intro-to-CoreData/Readme.md
[Lesson 6]: Lessons/Lesson6.md
[CoreData - Relationships and Heirarchies]: Lessons/06-CoreData-Relationships/Readme.md
[CoreData - Using multiple contexts and child contexts]: Lessons/07-CoreData-Contexts/Readme.md
[CoreData - Retrieving information from the stack]: Lessons/08-CoreData-Retrieving-Info/Readme.md
[Third Party Persistence Options - Realm]: Lessons/09-Realm-Intro/Readme.md
[Lesson 11]: Lessons/Lesson11.md
[Lesson 12]: Lessons/Lesson12.md


## Class Assignments

### Tutorials
**[NEED TO ADD]**

### Other Class assignments
- [Keychain Playground]

[Keychain Playground]: Assignments/KeychainSwiftPlayground

### Projects
- [Course Planner]
- [Document Management]
    - **[BROKEN API IN THIS PROJECT]**

[Course Planner]: Assignments/Project-Course-Planner/Readme.md
[Document Management]: Assignments/Project-Document-Management/Readme.md

**All projects will require a minimum of 10 commits, and must take place throughout the entirety of the course**

- **Good Example:** 40+ commits throughout the length of the course, looking for a healthy spattering of commits each week (such as 3-5 per day).
- **Bad Example:** 10 commits on one day during the course and no others. Students who do this will be at severe risk of not passing the class.
- **Unacceptable Example:** 2 commits the day before a project is due. Students who do this should not expect to pass the class. 

#### Why are we doing this?

We want to encourage best practices that you will see working as a professional software engineer. Breaking up a project by doing a large amount of commits helps engineers in the following ways:

- It's much easier to retrace your steps if you break your project/product/code up into smaller pieces
- It helps with being able to comprehend the larger problem, and also will help with your debugging (i.e. finding exactly when you pushed that piece of broken code)
- It allows for more streamlined, iterative communication in your team, as it's much easier to hand off a small change to someone (updating a function) than a huge one (changed the architecture of the project)

Through this requirement, we hope to encourage you to think about projects with an iterative, modular mindset. Doing so will allow you to break projects down into smaller milestones that come together to make your fully-realized solution.

## Evaluation

To pass this course you must meet the following requirements:

- No more than two no call no shows
- No more than four excused absences
- Make up all classwork from all absences
- Finish all required tutorials and projects
- Pass the final exam (summative assessment) with >=80%

## Attendance
Just like any job, attendance at Make School is required and a key component of your success. Attendance is being onsite from 9:30 to 5:30 each day, attending all scheduled sessions including classes, huddles, coaching and school meetings, and working in the study labs when not in a scheduled session. Working onsite allows you to learn with your peers, have access to support from TAs, instructors and others, and is vital to your learning.

Attendance requirements for scheduled sessions are:
- No more than two no call no shows per term in any scheduled session.
- No more than four excused absences per term in any scheduled session.

Failure to meet these requirements will result in a PIP (Participation Improvement Plan).  Failure to improve after the PIP is cause for not being allowed to continue at Make School. 


## Make School Course Policies

[Academic Honesty](https://make.sc/academic-honesty)<br>
[Accommodations for Students](https://make.sc/accommodations-for-students)<br>
[Attendance Policy](https://make.sc/attendance-policy)  
[Diversity and Inclusion Policy](https://make.sc/diversity-and-inclusion-policy)<br>
[Grading System](https://make.sc/grading-system)
<br>
[Title IX Policy](https://make.sc/title-ix-policy)<br>
[Program Learning Outcomes](https://make.sc/program-learning-outcomes)
