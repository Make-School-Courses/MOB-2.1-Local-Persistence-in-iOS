# NSFetchRequests, NSSortDescriptors & NSFetchedResultsController

## Minute-by-Minute [OPTIONAL]

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:15      | Overview                  |
| 0:20        | 0:45      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 1:15        | 0:45      | In Class Activity II      |
| TOTAL       | 2:00      |                           |

## Why you should know this or industry application (optional) (5 min)

So far we have been experimenting with Core Data and learning how it works below the surface. When retrieving data, we've used simple examples of fetching all entities. There are ways to make more refined or specific fetches and it will save us time and resources if we learn how to do them.

## Learning Objectives (5 min)

- Fetch data from Core Data with NSFetchedRequest
- Refine a search using NSPredicate
- Sort data with NSSortDescriptor
- Fetch and display data with NSFetchedResultsController

### Predicates

Provides an interface for querying much like a mixture of sql and a regular expression

**Example**

```swift

// Filter for results with property firstName == "Bubbles"

let firstName = "Bubbles"
fetchRequest.predicate = NSPredicate(format: "firstName == %@", firstName)
```

#### Gist of Predicates

1. Simple Comparison Operators
We can use ```>, <, >=, <=, ==, !=```

**Example**

*Simple Comparison*
```swift
let pred = NSPredicate(format: "population >= 10")
```

*Comparison with like*
```swift
let fruit = "mango"
let pred = NSPredicate(format: "fruit like %@", fruit)
```

*Logical Operations (OR, AND)*
```swift
let pred = NSPredicate(format: "name like John OR age == 5")
```

*Filter with a list*

```swift
// Will yield any results containing the name Apples and Mango

let pred = NSPredicate(format: "name in %@", ["Apples", "Mango"])
```


2. Formating

%i is for substituting integers, %@ is for substituting strings

**Example**

*Strings*
```swift
let pred = NSPredicate(format: "quantity > %i", 4)
```

*Numbers*

```swift
let pred = NSPredicate(format: "name == %@", "Eliel")
```

##### Full Cheatsheet of Predicates

[Realm Predicate Cheatsheet](https://academy.realm.io/posts/nspredicate-cheatsheet/)

## In Class Activity I (30 min)

https://github.com/dfreniche/NSPredicate-Swift/tree/master/NSPredicate.playground

## NSFetchRequest

We fetch entities from Core Data by creating an instance of NSFetchRequest. Then we configure it as we need and hand it over to NSManagedObjectContext to to the search and work.

There are different ways to set up a fetch request, here are a few:

```swift
let fetchRequest = NSFetchRequest<Shop>()
let entity = NSEntityDescription.entity(forEntityName: "Shop",in: managedContext)!
fetchRequest.entity = entity
```

Initializing an instance of `NSFetchRequest` using a generic type `NSFetchRequest<Shop>`. Then initialize an instance of `NSEntityDescription` and use it to set the fetch request's entity.

```swift
let fetchRequest = NSFetchRequest<Shop>(entityName: "Shop")
```
Using NSFetchRequest's convenience initializer. It also sets the entity property in the same step. You only need to specify the string for the entity name, instead of a description.

```swift
let fetchRequest = managedObjectModel.fetchRequestTemplate(forName: "coffeeShop")
```
Retrieve the fetch request from the `NSManagedObjectModel`.

```swift
let fetchRequest = managedObjectModel.fetchRequestFromTemplate(
    withName: "coffeeShop",
    substitutionVariables: ["Name" : "Sightglass"])
```

Get the fetch request from the managed object model with some extra variables. These are used in a predicate to filter the results.


### Sort Descriptors

Sort Descriptors enables us to sort results from a fetch request.

```swift
let sortDescriptor = NSSortDescriptor(key: "name", ascending: true)
fetchRequest.sortDescriptors = [sortDescriptor]
```
To initialize an instance of NSSortDescriptor you need three things: a key path to specify the attribute which you want to sort, a specification of whether the sort is ascending or descending and an optional selector to perform the comparison operation.

### NSFetchedResultsController

Performing queries to Core Data and displaying them has never been easier.
Using NSFetchedResultsController, we can perform

1. Initialize your fetch request

```swift
// Initialize a FetchRequest
let fetchRequest: NSFetchRequest<Inventory> = Inventory.fetchRequest()
```

2. Add any sort descriptors (Optional)

```swift
// Add any SortDescriptors
let sortDescriptor = NSSortDescriptor(key: "name", ascending: true)
fetchRequest.sortDescriptors = [sortDescriptor]
```

3. Add any predicates (Optional)

```swift
let quantityFilter = 4
let pred = NSPredicate(format: "quantity > %i", quantityFilter)

fetchRequest.predicate = pred
```

4. Initialize a FetchedResultsController with our FetchRequest and MOC

```swift
let fetchedResultsController = NSFetchedResultsController(
    fetchRequest: fetchRequest,
    managedObjectContext: self.stack.viewContext,
    sectionNameKeyPath: nil,
    cacheName: nil
)
```

5. Set the FetchedResultsController delegate

```swift
fetchedResultsController.delegate = self
```

6. Implement NSFetchedResultsControllerDelegate (Optional)

7. UITableView/UICollectionView number of rows in section and cellForRow change to use fetched results

```swift

func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    guard let sections = fetchedResultsController.sections else {
        return 0
    }

    let sectionInfo = sections[section]
    return sectionInfo.numberOfObjects
}


func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "InventoryCell", for: indexPath)

    // FetchedResultsController controls fetching of ManagedObjects
    let item = fetchedResultsController.object(at: indexPath)

    cell.textLabel?.text = item.name
    cell.detailTextLabel?.text = "x\(item.quantity)"

    return cell
}
```

8. Fetch from FetchedResultsController and reload data as needed

```swift
override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)

    try? fetchedResultsController.performFetch()
    tableView.reloadData()
}
```
## In Class Activity II (30 min)

Individually - follow the activity described [here]

[here]:Activity.md.

## Resources

[Realm Predicate Cheatsheet](https://academy.realm.io/posts/nspredicate-cheatsheet/)

[NSPredicate](http://nshipster.com/nspredicate/)

[Sort Descriptors]()

Core Data by Tutorials by Pietro Rea.
