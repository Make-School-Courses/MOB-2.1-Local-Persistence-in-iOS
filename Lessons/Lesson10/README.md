<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Realm

## [Slides](https://make-school-courses.github.io/MOB-2.1-Local-Persistence-in-iOS/Slides/Lesson10/README.html ':ignore')

<!-- > -->

## Why you should know this

We spent time learning about how Core Data works, building our own Core Data Stack and learning how it works under the hood. It's good to know there are other options that will give us the same results with maybe less effort and with a certain level of freedom.

One of this options is Realm, and we'll see how to add it to our projects to get the same results as we did with Core Data.

<!-- > -->

## Learning Objectives

1. Describe how Realm works and it's ties with Core Data.
1. Implement CRUD methods using Realm.
1. Design a solution for an app using Realm.

<!-- > -->

## Realm

Realm is a cross platform database(iOS, Android, Web). It can be used in place of CoreData for persisting data in iOS. It was designed to be faster and more efficient than other solutions.

<!-- > -->

### Why Realm?

- Easy set up.
- Easy to solve queries.
- Thread safe.
- Reactive architecture to always show updated data.
- Widely used.

<!-- > -->

### Core Data vs Realm

| **Feature**     | **Core Data**  | **Realm**      |
| --------------- | -------------- | -------------- |
| Easy to set up  | -              | XX             |
| Speed           | X              | XX             |
| Crossplatform   | -              | XX             |
| Thread safe     | X              | X              |
| Documentation   | X              | XXX            |
| DB Management   | External tools | Realm studio   |

<!-- > -->

## Realm walkthrough

**Installation**

Download Realm here(Manual, Cocoapods, Carthage)

[Realm Download](https://realm.io/docs/swift/latest#installation)

<!-- > -->

## Realm

Realm has two products, a RealmObjectServer and RealmDatabase. We will be using the **RealmDatabase** product its open source and free to use in production.

A **Realm** is an instance of a Realm Mobile Database container.<br>
Realms can be in *memory, synchronized or local.*

- In-memory Realms have no persistence mechanism (temporary storage)
- Synchronized Realms use a RealmObjectServer to sync with other devices (shopping carts, chats).
- Local

<!-- > -->

A Realm is not:
- A single application-wide database. We can have multiple Realms to organize data more efficiently.
- A table. Tables typically store one kind of information, a Realm can have multiple kinds of objects.

<!-- > -->

### Opening a Local Realm

```swift
let realm = try! Realm()
```

<!-- > -->

### Models

Instances of items stored in Realm are referred to as *Objects* - Similar to ManagedObject in CoreData.

Realm data models are defined as regular Swift classes with regular properties.<br>
to create one, we simply subclass `Object`.

These objects work like any other Swift object. We can define methods on them, conform them to protocols, etc. Only restriction: we can only use an object on the thread which it was created.

<!-- > -->

```swift
// Dog model
class Dog: Object {
    @objc dynamic var name = ""
    @objc dynamic var age = 0
}

// Person model
class Person: Object {
    @objc dynamic var name = ""
}
```

<!-- > -->

#### Relationships

To set up a **many-to-one or one-to-one** relationship, give a model a property whose type is one of your Object subclasses.

```swift
class Dog: Object {
    // ... other property declarations
    @objc dynamic var owner: Person? // to-one relationships must be optional
}
```

<!-- > -->

To create a **many-to-many** relationship use List properties. Lists contain other Objects or primitive values of a single type and have an interface very similar to a mutable Array.

```swift
class Person: Object {
    // ... other property declarations
    let dogs = List<Dog>()
}
```

<!-- > -->

#### Writing Objects

```swift
// (1) Create a Dog object using the designated initializer
var myDog = Dog()
myDog.name = "Dexter"
myDog.age = 1

// (2) Create a Dog object from a dictionary using appropriate keys and values
let myOtherDog = Dog(value: ["name" : "Lucy", "age": 2])

// (3) Create a Dog object from an array, where values have to be in the same order as the properties in the model.
let myThirdDog = Dog(value: ["Layla", 2])

// Get the default Realm
let realm = try! Realm()
// You only need to do this once (per thread)

// Add to the Realm inside a transaction
try! realm.write {
    realm.add(myDog)
    realm.add(myOtherDog)
    realm.add(myThirdDog)
}

```

<!-- > -->

#### Fetching Objects

**Queries**

Queries return a `Results` instance which is a collection of Objects.

```swift
let dogs = realm.objects(Dog.self)
```

<!-- > -->

**Filtering**

We can use `NSPredicate` :)

```swift

// Query using an NSPredicate
let predicate = NSPredicate(format: "color = %@ AND name BEGINSWITH %@", "tan", "B")
tanDogs = realm.objects(Dog.self).filter(predicate)

```

<!-- > -->

**Sorting**

`Results` allows you to specify a sort criteria and order based on:
- a key path
- a property
- sort descriptors

```swift
let sortedDogs = realm.objects(Dog.self).filter("color = 'tan' AND name BEGINSWITH 'B'").sorted(byKeyPath: "name")
```

<!-- > -->

### More things to check out
- Chaining queries
- Auto-updating results
- Realm notifications
- [Realm Studio](https://realm.io/products/realm-studio/#download-studio)
  To open your Realm file in the Manager, find it's location in the simulator<br>
  `(lldb) po Realm.Configuration.defaultConfiguration.fileURL` Then drag it into the manager app.

<!-- > -->

## In Class Activity I

Complete the activity on [this repo](https://github.com/amelinagzz/Realm-starter) to get started with Realm.

Stretch challenges:
- Make it possible to update all value types in a book (for example, the year).
- Adjust the find method to bring values that contain the search text, in case the user can't remember the complete name.
- Download Realm Studio and see how your data looks like and add entries right there.

<!-- > -->

## In Class Activity II

Clone this repo and integrate Realm with Cocoa pods:

[TriviaTime Starter](https://github.com/Product-College-Labs/TriviaTime)

Stretch challenges:
- Add Realm notifications to the app to automatically update the table when answering questions.

<!-- > -->

## External Resources
- [Slides](https://docs.google.com/presentation/d/1pJCtx0sLkRzIvqfhDOyD2MRVCu78pcck2JL-bL2Wefc/edit?usp=sharing)
- [Realm vs Core Data](http://www.rockersinfo.com/blog/realm-database-vs-coredata/)
- [Realm's Data Models](https://realm.io/docs/data-model)
- [More on Realms](https://realm.io/docs/swift/latest/#realms)
- [Realm's notifications](https://realm.io/docs/swift/latest/#notifications)
- [On finding the Realm file](https://stackoverflow.com/questions/28465706/how-to-find-my-realm-file)
- [Tutorial & first activity](https://rollout.io/blog/realm-database-tutorial-get-started-quickly-swift/)
