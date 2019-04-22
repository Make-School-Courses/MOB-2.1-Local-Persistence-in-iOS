# Core Data Stack & Relationships

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Initial activity          |
| 0:05        | 0:05      | Objectives                |
| 0:10        | 0:10      | Core Data Stack           |
| 0:20        | 0:15      | Relationships             |
| 0:35        | 0:25      | In Class Activity I       |
| 1:00        | 0:10      | BREAK                     |
| 1:10        | 0:25      | In Class Activity I       |
| 1:35        | 0:10      | Wrap Up                   |
| TOTAL       | 1:45      |                           |

<!--## Class Materials

Slides: [CoreData Relationships Slides](core_data_relationships.key) -->

## Initial Activity
- Reminder of updating missing activities. This Friday mid term grades will be sent.
- Any questions with the current tutorial?
- Any questions with the final project?

## Why you should know this

So far in order to use Core Data, we have been using Xcode's template that comes in the AppDelegate. We could leave it as it is and the app's functionality won't be affected. But if we really want to know the details of what's happening, we could implement our own Core Data stack. This helps in two ways: we get to learn about how Core Data works in detail and we get better separation of concerns (the AppDelegate shouldn't be responsible of initializing all the things).

Another situation in which you would encounter the need to write your own CoreData stack is if you are working with migrating data from an old store to a new one.

## Learning Objectives (5 min)

- Create our own Core Data Stack.
- Subclassing NSManagedObject for entities.
- Use the model editor to create relationships between properties.
- Identify different types of relationships.

## The Core Data Stack (10 min)

Let's remember the components that make up the Core Data stack:
- **NSManagedObjectModel**
Represents each object type in the data model, along with its properties and relationships.

- **NSPersistentStore**
Reads and writes data to the storage we want. Core Data gives us four types of NSPersistentStore: three atomic and one non-atomic.

  *Atomic*: needs to be deserialized and loaded into memory before performing any read or write operation.<br>
  *Non-atomic*: can load itself onto memory as needed.

  1. **NSQLiteStoreType** - SQLite database. (the only non-atomic store type, that comes ready to use). Lightweight & efficient = used by default.

  1. **NSXMLStoretype** - XML file. The most easy to read. Atomic.

  1. **NSBinaryStoreType** - Binary data file. Atomic (the entire file must be loaded before using it). Rarely used.

  1. **NSInMemoryStoreType** - Not persistent, only helpful for testing and maybe caching.

- **NSPersistentStoreCoordinator**
Bridge between the managed object model and persistent store. Uses the model and persistent stores to do the hard work. Hides implementation details of the store. In this way the NSManagedObjectContext doesn't care the type of store or how many there are.

- **NSManagedObjectContext**
We ALWAYS need one of these to work with Core Data.

* This is a scratchpad for working with our managed objects.
* All the work done with objects happens here and changes won't affect data until we call save on the context.
* Manages the lifecycle of objects (relationships and validation)
* Every object keeps a reference to its context, can't exist without one.
* Not thread safe, we can only work with objects and contexts on the thread they were created.

- **NSPersistentContainer**
Container that holds everything together (the managed model, the store coordinator, persistent store and managed context)


## Relationships (15 min)

A relationship describes how an entity affects another entity. At minimum, a relationship specifies a name, a destination entity, a delete rule, a cardinality type (To One or To Many), settings for whether the relationship should be saved in the store (transient), and whether it is required to have a value when saved (optional). You should also configure every relationship with an inverse relationship.

Relationships are modeled similar to relational database modeling that means: we create: one-to-one, one-to-many and many-to-many.

- Transient
- Optional
- Destination
- Inverse
  ManagedObject relationships are inherently bidirectional. What does that mean?<br>
  If a User has many Tweets, then a Tweet can have one(Belong to one) User. <br>
  Model relationships in both directions; CoreData uses that to ensure consistency of its objects.

- Cardinality
  - One to one relationships are created using a to-one relationship.
  - One to many relationships are created using a to-many relationship.
- Arragement
- Count


## In Class Activity I (50 min)

Instead of having the stack in the app delegate, we'll create a separate class for it. Let's pair program this time. This means all the coding will be made in just ONE computer while the other person guides with the instructions.

Download the [starter project here](https://github.com/amelinagzz/coredata-starter) and work from there.

**File -> New -> File -> iOS -> Source -> Swift File template -> Next**
And name it CoreDataStack, then save it.

Add the following to the file:

```swift
import Foundation
import CoreData //import the core data module

class CoreDataStack {

  private let modelName: String //create a private property to store the modelName

  //we always need this
  lazy var managedContext: NSManagedObjectContext = {
    return self.storeContainer.viewContext
    }()

  init(modelName: String) {
    self.modelName = modelName //initializer needed to save the modelName into the private property
  }

  //lazy instantiate the NSPersistentContainer, passing the modelName
  private lazy var storeContainer: NSPersistentContainer = {

    let container = NSPersistentContainer(name: self.modelName)
    container.loadPersistentStores {(storeDescription, error) in
      if let error = error as NSError? {
        print("Error: \(error), \(error.userInfo)")
      }
    }
    return container
  }()

}
```

Notice everything is private except for the `NSManagedObjectContext`.

**Q: What do you think is the reason?**

<!-- This is the only thing we need to interact with to use the stack. -->

We need a method to save the context. If we don't call it, data in the store won't change.

```swift
  func saveContext () {
    guard managedContext.hasChanges else { return }

    do {
      try managedContext.save()
    } catch let error as NSError {
      print("Error: \(error), \(error.userInfo)")
    }
  }
```

Now we can move on to use the stack in the main view controller.

Go to `ViewController.swift` and import Core Data. then add a property for the managed object context. Call it `managedContext`.

Now go to the app delegate and import Core Data. Add a property to hold the stack.

```swift
lazy var coreDataStack = CoreDataStack(modelName: "WaterLog")
```

**Q: Why do you think this is a lazy initialization?**
<!-- The stack won't be set up until we need to access the property -->

We need to send the managed context from our stack to the ViewController.
Add the following inside the `didFinishLaunchingWithOptions` method.

```swift
guard let navController = window?.rootViewController as? UINavigationController, let viewController =
        navController.topViewController as? ViewController else {
        return true
    }

viewController.managedContext = coreDataStack.managedContext
```

We want to make sure the app will save any changes if it goes to the background or if it gets terminated. For this, add the `applicationDidenterBackground` and `applicationWillTerminate` methods and call the method `saveContext` in our stack property.

We're done. Now we need to model data. 😀

Before going further, **change the roles** of who is coding and who guiding the activity.

If you notice, we don't have a model file because the project was created without the Core Data template, so there's no `.xcdatamodeld` file. Create a new one.

**File -> New -> File -> iOS -> Core Data -> Data Model -> Next**
Name the file `WaterLog.xcdatamodeld`. Make sure the name matches what you had previously in your stack.

Create a new entity named `Plant` with an attribute named `species` of type String.<br>
Create another entity named `WaterDate` with an attribute named `date` of type Date.<br>

We know each plant can be watered several times a month, there is no type Array to model this. But the thing we do is create a relationship. Go to the Plant entity and add a new relationship, name it `waterDates` and set the destination to `WaterDate`.

Change the view to graph (right option from lower right segmented control). This a great way to see the relationships between entities.

All relationships are by default to-one, meaning you can only track a date once. But we need this to be more times, or else your plant will die. So change the relationship in the Data Model Inspector and change `Type` to `To Many`. See how this changes in the chart.

Now select the WaterDate entity and create an inverse relationship to Plant. Set `plant` as destination and `waterDates` as inverse. again see how this changes in the chart.

**Q: Why are we leaving this relationship as to-one?**
<!-- A plant can be watered many times but each water date belongs to a plant -->

**Q: How are to-one vs to-many relationships represented in the graph editor?**
<!-- to-many with a double arrow, to-one with one arrow -->

Let's create subclasses of managed objects for our entities. Open the `.xcdatamodeld` file and select an entity. Change the Codegen dropdown in the inspector to Manual/Note. Do this for all entities.

Then go to **Editor -> Create NSManagedObject subclass** Choose the WaterLog model and both entities. Then create.

We now have two files per entity. One is for the properties defines in the mode editor and the other one for future functionality.

Open the `Plant+CoreDataProperties.swift` and notice how the relationship is modeled.

Open the `WaterDate+CoreDataProperties.swift` and notice how the inverse relationship is modeled.

Everything is ready for the app to implement Core Data.

Go back to the main ViewController. Suppose we can only see the data of one plant at a time, so instead of having an array of dates, we have `var mainPlant : Plant?`.

Add the following to `viewDidLoad`
```swift
//we will look for Fido for this example. We'll go over how to query in future lessons.

   let plantSpecies = "Cactus"
   let plantSearch: NSFetchRequest<Plant> = Plant.fetchRequest()
   plantSearch.predicate = NSPredicate(format: "%K == %@", #keyPath(Plant.species), plantSpecies)

   do {
     let results = try managedContext.fetch(plantSearch)
     if results.count > 0 {
       // cactus found
       mainPlant = results.first
     } else {
       // not found, create cactus
       mainPlant = Plant(context: managedContext)
       mainPlant?.species = plantSpecies
       try managedContext.save()
     }
   } catch let error as NSError {
     print("Error: \(error) description: \(error.userInfo)")
   }
```

Change `numberOfRowsInSection` to use the count of the plant's waterDates.

Change `cellForRowAt` to display the date.

Finally modify the add method to create new Dates accordingly.

```swift
//new water date entity
  let waterDate = WaterDate(context: managedContext)
  waterDate.date = NSDate()

//add it to the Plant's dates set

  if let plant = mainPlant, let dates = plant.waterDates?.mutableCopy() as? NSMutableOrderedSet {
    dates.add(waterDate)
    plant.dates = dates
  }

//save the managed object context  
  do {
    try managedContext.save()    
  } catch let error as NSError {
    print("Error: \(error), description: \(error.userInfo)")
  }

```

## Stretch challenges
1. Include the functionality to delete dates in today's activity.
1. We will eventually practice unit testing using Core Data. While we get there, take your activity from the Keychain class and include unit tests for getting, deleting and updating values using the library KeychainSwift.

# Additional resources

- [Slides](https://docs.google.com/presentation/d/1N3LG8h3dnLpqIQmhTOqqiX8x3cP87dFn0ybqDy7M4CA/edit?usp=sharing)
- Walkthrough the creation of Entities, Attributes and Relationships can be found [here](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/KeyConcepts.html)
- Configuring entities [here](https://developer.apple.com/documentation/coredata/modeling_data/configuring_entities)<br>
- Configuring attributes [here](https://developer.apple.com/documentation/coredata/modeling_data/configuring_entities)<br>
- Configuring relationships [here](https://developer.apple.com/documentation/coredata/modeling_data/configuring_relationships)<br>
- [Modern Core Data article](https://stoeffn.de/posts/modern-core-data-in-swift/)
- Theory and activity based on content from “Core Data by Tutorials.” By Pietro Rea.



<!--## In Class Activity I (40 min)

Clone/Download the repo below to get started:

[Shop Keep Starter](https://github.com/Product-College-Labs/shop-keep.git)

TODO:
Include the option to delete shops.<br>
Include functionality to add employees and managers.

Extra:
Include functionality to add shops.<br>
Include functionality to edit employees and managers.<br>
-->
