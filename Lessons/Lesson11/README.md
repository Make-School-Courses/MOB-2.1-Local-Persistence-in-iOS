<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# CloudKit

## [Slides](https://make-school-courses.github.io/MOB-2.1-Local-Persistence-in-iOS/Slides/Lesson11/README.html ':ignore')

<!-- > -->

## Why you should know this

Everything should sync -> We turn to cloud storage
As the app creates data, it can be backed up and recovered anytime.


<!-- > -->

## Learning Objectives

1.

<!-- > -->

## CoreData & CloudKit

We've learned to use Core Data API to manage data locally in an app.
CloudKit gives access to a large distributed database.

Both are very similar and model their APIs in terms of Objects, Models and Stores.

|         |      CoreData            |       CloudKit               |
|:-------:|:------------------------:|:----------------------------:|
| Objects |   NSManagedObject        |     CKRecord                 |
| Model   |   NSManagedObjectModel   |     Schema                   |
| Store   |   NSPersistentStore      |     CKRecordZone/CKDatabase  |

<!-- > -->

## Creating a new project

When creating a new project we must make sure to select support for CoreData & CloudKit.

We also need to set up Capabilities:
- iCloud & we automatically get the Notifications support.
- Background Modes

<!-- > -->

## NSPersistentCloudKitContainer

- Encapsulation of common patterns used to build sync with iCloud
- Gives us a copy of all CloudKit data to store locally
- Robust scheduling and error recovery
- Handles transformation between NSManagedObject and CKRecord

<!-- > -->

## Why a local replica of CloudKit?

[Video](https://developer.apple.com/videos/play/wwdc2019/202/) min 9:00

<!-- > -->


## External resources

- [Using Core Data with CloudKit](https://developer.apple.com/videos/play/wwdc2019/202/)
