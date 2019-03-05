# Introduction to Realm

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

Explain why students should care to learn the material presented in this class.

## Learning Objectives (5 min)

1. Identify and describe
1. Define
1. Design
1. Implement

## Overview (20 min)
Realm is a cross platform database(iOS, Android, Web). It can be used in place of CoreData for persisting data in iOS.

## In Class Activity I (30 min)

### Installation up Realm

Download Realm here(Manual, Cocoapod, Carthage)

[Realm Download](https://realm.io/docs/swift/latest#installation)

#### Realm

Realm has two products, a RealmObjectServer and RealmDatabase. We will be using the RealmDatabase product its open source and free to use in production.

Realms can be in *memory, synchronized or local.*


#### Realm Setup

```swift
// Setups the default Realm

let realm = try! Realm()
```

#### Modeling Objects

Instances of items stored in Realm are referred to as *Objects* - Similar to ManagedObject in CoreData.

```swift
import RealmSwift

class Inventory: Object {
    @objc dynamic var name: String = ""
    @objc dynamic var quantity: Int = 0
}

```


#### Writing Objects

```swift

let inventory1 = Inventory()
inventory1.name = "Bubbles"
inventory1.quantity = 10


try! realm.write {
    realm.add(inventory1)
}

```

#### Fetching Objects

**Fetching**
```swift
let inventories = realm.objects(Inventory.self)

let arrayInventory = Array(inventories)

```

**Filtering**

```swift
let inventories = realm
                    .objects(Inventory.self)
                    .filter("quantity > 5")

let arrayInventory = Array(inventories)
```

## Challenges

Clone this repo and integrate realm:

[TriviaTime Starter](https://github.com/Product-College-Labs/TriviaTime)
