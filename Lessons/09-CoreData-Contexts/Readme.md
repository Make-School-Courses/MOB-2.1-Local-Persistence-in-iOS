# CoreData - Multiple ManagedObjectContexts

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:25      | Overview                  |
| 0:30        | 0:35      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 1:15        | 0:15      | Discussion                |
| 1:30        | 0:15      | Wrap Up                   |
| TOTAL       | 1:45      |                           |

## Why you should know this

A managed object context is an in-memory scratchpad for working with your managed objects.

Most apps need only one. This managed object context is associated with the main queue. As apps get more complex, this may cause the UI to fail.

Multiple managed object contexts make apps harder to debug so it's important that you evaluate if you really need it.

Long-running tasks like exporting data, will block the main thread on apps that have one managed object context. This looks like a good place to add another one and we must know how to do this.

## Learning Objectives (5 min)

- Learn about having multiple ManagedObjectContexts.
- Discuss and use child contexts.
- Discuss thread safety with ManagedObjectContexts.


### ManagedObjectContexts & Thread safety

ManagedObjectContexts are not thread safe. This means we can't just dispatch to a background queue and use the same Core Data stack. We have to use them with caution when concurrency is at play.

If we have multiple threads (main and some background thread for example) access the same ManagedObjects, we should have consistent behavior.

A solution is to use a private background queue for long running tasks.

### How?
The PersistentContainer makes dealing with private contexts easy.

The ```performBackgroundTask``` method of the PersistentContainer spins up a new private background context in a closure.


```swift
persistentContainer.performBackgroundTask { (context) in
    for object in objectArray {
        //heavy processing
    }
    do {
      //save context
        try context.save()
    } catch {
        fatalError("Failure to save context: \(error)")
    }
}
```

**Recomended Use of Contexts**

We use the **main context** for interacting with core data on the application's view layer.

But complex operation such as saving multiple ManagedObjects in core data takes a long time and hence will block the main thread(if using main context).

What we want to do is hand off saves to a **background context** so write operations can be performed on the background.

## Fetching ManagedObjects from the main ManagedObjectContext & saving on a background Context

One way we can handle a save in this situation is to change the ManagedObjectContext.
Since fetching from the main context, all objects retrieved will be associated with the main managed object context.

**Option 1: Changing Contexts**
1. Grab the objectID from the ManagedObject.
```swift
let objectID = myManagedObject.objectID
```
2. Fetch the same ManagedObject from the background ManagedObjectContext.
```swift
let myBackgroundManagedObject = coreDataStack.privateContext.object(with: objectID)
```
3. Do any modifications to your ManagedObject
4. Perform a save on the privateContext


**Option 2: Using Child Contexts**

Think of a notes application. We create a new note and make edits, delete text, modify, keep changing the content until we're happy with our text and then we want to hit save. In an app like this, we can simplify how Core Data works by making the changes as the user edits the note. Then we either save the changes or discard them. Depending on the final decision of the user.

Child managed object contexts are temporary scratch pads that we can save or discard. If saved, we send the changes to the parent context.

All managed object contexts have a parent store from which we can retrieve and change managed objects.

The parent store is a persistent store coordinator. But we can also set the parent store to another managed object context, turning it into a child context.


![Contexts](contexts.png)


NOTE: Whenever we save a child context, the changes go up to the parent context. BUT these changes won't be sent to the persistent store coordinator until the parent context is saved.

You can set one ManagedObjectContext as a child to another.

To solve the problem of saving to a background context, we can create a new privateContext and set the main context as the parent.

```swift
privateContext.parentContext = viewContext
```

## In Class Activity

Making the necessary changes in a core data app to use multiple ManagedObjectContexts is not that complicated and it doesn't require many steps.

What's challenging is identifying the need to apply multiple MOC.

[This tutorial](https://www.raywenderlich.com/7586-multiple-managed-object-contexts-with-core-data-tutorial) uses an app that logs entries in a surf journal and rates surf sessions. The starter code can be found [here](https://koenig-media.raywenderlich.com/uploads/2018/09/multiple-managed-ob-ject-contexts-Swift-4.2.zip)

Before starting the tutorial, make sure you are able to run the project. See that there is an export functionality that will take all the contents of the table into a CSV file. Try scrolling the table and then try to export the content. Look out for the main problem we want to solve. What is it?

Go over the tutorial to fix the issue.
There are two main things you should have in the end:
- Created a `ManagedObjectContext` that works in the background.
- Used a child context to make edits in the ManagedObjects before hitting save.

## Discussion questions

- How did the app populated all the data when we fist opened it?
- What was the problem with exporting the data to CSV?
- When is it a good moment to start introducing multiple managed object contexts?
- What is a benefit from doing this?
- What can go wrong?
- What is `performBackgroundTask` doing in the app?
- What is the difference between Private an Main queues?
- What is `childContext.parent = coreDataStack.mainContext` doing for us?
- Why you we to pass the managed object *and* the managed object context to the `detailViewController`?


## Stretch Challenge for the tutorial
Change `SegueListToDetailAdd` to use a child context when adding a new journal entry. You will need to create a child context that has the main context as its parent. And create the new entry on the correct context.

## Additional Resources

- [Slides](https://docs.google.com/presentation/d/1mx-_ELFm5_zCMzEIgTnfM2RhxVgq_pX2k8tAo9bsUB8/edit#slide=id.g514c043897_0_135)
- https://www.raywenderlich.com/7586-multiple-managed-object-contexts-with-core-data-tutorial
- “Core Data by Tutorials.” By Pietro Rea.
