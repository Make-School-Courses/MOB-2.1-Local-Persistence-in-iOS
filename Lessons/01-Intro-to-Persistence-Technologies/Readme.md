# Intro to Persistence Technologies

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:10      | Intro to course           |
| 0:10        | 0:05      | Objectives                |
| 0:15        | 0:05      | Overview                  |
| 0:20        | 0:45      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 1:15        | 0:15      | Advanced persistence      |
| 1:30        | 0:10      | Closing Exercise          |
| 1:40        | 0:05      | Wrap Up                   |
| TOTAL       | 1:45      |                           |

## Intro to course
Go over the course repo identifying:
  - Course description & Learning outcomes
  - Class schedule
  - Office Hours
  - Course repo link
  - Course tracker link
  - Projects and Tutorials
  - Evaluation criteria

## Why you should know this

Most iOS applications have a way of persisting data. Whether an app needs to store lightweight data such as user preferences or larger data that needs to be stored in a relational database, knowing different options of persistence is useful to decide what method to use. Choosing the ideal method depending on your data will help you make the best use of the resources available on the device.

## Learning Objectives (5 min)

- Identify the main tools to persist data in iOS.
- Compare and contrast – at a high level – every method of persistence.
- List some advanced persistence technologies for iOS.

## Overview (5 min)
How we store data in iOS devices depends, among other criteria, on:
- The size/amount of the data.
- The type of data.
- The level of sensitivity of the data.
- How often we need to consult the data.

This lesson is intended to portray an overview of each persistence method. And upcoming classes will dive deeper on each one.

## In Class Activity I (45 min)

The class will be divided into 5 groups. Each group will take 15 minutes to do a quick research on a specific method to save data (these will be assigned at random). The purpose is to get a general idea of how it works, you don't need to learn how to implement it now.

Then for the next 10 minutes each member of the group will contribute in a discussion to agree on the following criteria for the method given:

- 3 key points describing the persistence Method
- Pros
- Cons
- Mention some use cases

Methods:
- NSUserDefaults
- Keychain
- FileSystem
- Plist
- CoreData

Each group will fill out the corresponding slide for their method with the 4 ideas that were required. In the order above, each team will share their findings with the rest of the class in no more than 5 minutes.

At the end of each mini presentation, if a student from another team wants to add something they know already, their contributions can be added to the slide.

## Advanced Persistence Technologies (15 min)
![databases](assets/databases.png)

### Core Data
The last method covered was [Core Data](https://developer.apple.com/documentation/coredata).

"Core Data is a framework that you use to manage the model layer objects in your application. It provides generalized and automated solutions to common tasks associated with object life cycle and object graph management, including persistence."

This is a powerful tool that has a lot of built in features. Getting comfortable using Core data takes time and a lot of errors.

### Realm
[Realm](https://realm.io/) is a good alternative for Core Data.

"Realm is a mobile database that runs directly inside phones, tablets or wearables."

Its purpose is to make managing data faster and simpler.

From the official [Github site](https://github.com/realm/realm-cocoa):

#### Features

- Mobile-first: First database built from the ground up to run directly inside phones, tablets and wearables.
- Simple: Data exposed as objects and queryable by code. Most of our users pick it up intuitively, getting simple apps up & running in minutes.
- Modern: Supports relationships, generics, vectorization and Swift.
- Fast: Faster than even raw SQLite on common operations, while maintaining an extremely rich feature set.

### SQLite
[SQLite](https://www.sqlite.org/index.html) is a relational database that can be used by iOS apps. It is contained in a C-library embedded to the app.

#### Features
- Lightweight
- Works as part of the app, no extra services needed
- Fast & reliable
- SQL knowledge can be used

## Closing Exercise (10)

In a piece of paper, list two things you are hoping to get out of this course.

Turn in your answer to the instructor.

## Wrap Up (5 min)
- Update the tracker with your Github profile link.

## Additional resources
[Slides](https://docs.google.com/presentation/d/17TMA-xdVtfvTO-fGrwvNyFn-7-tuau6ONJZD42FmFfE/edit?usp=sharing)<br>
[Realm](https://github.com/realm/realm-cocoa)<br>
[What is CoreData](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/index.html)<br>
[SQLite](https://www.simplifiedios.net/swift-sqlite-tutorial)
