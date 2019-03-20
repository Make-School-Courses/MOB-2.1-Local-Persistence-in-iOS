# CoreData Relationships

## Minute-by-Minute [OPTIONAL]

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:15      | Overview                  |
| 0:20        | 0:45      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 1:15        | 0:45      | In Class Activity II      |
| TOTAL       | 2:00      |                           |

## Class Materials

Slides: [CoreData Relationships Slides](core_data_relationships.key)

## Why you should know this or industry application (optional) (5 min)

Explain why students should care to learn the material presented in this class.

## Learning Objectives (5 min)

- Identify 1 to 1 and one to many relationships.
- Provide examples of these relationships.
- Use the model editor to create relationships between properties.

## Overview (20 min)

Slides to explain the following concepts:

- Creating _ManagedObject_ relationships
- Inverse relationships
- Reflexive relationships
- Optional relationships
- Unique constraints
- Merge Policy (?)
- Relationship Delete Rules

### Creating a managed object model

Much of Core Data’s functionality depends on the schema you create to describe your application’s entities, their properties, and the relationships between them. Core Data uses a schema called a managed object model — an instance of NSManagedObjectModel. In general, the richer the model, the better Core Data is able to support your application.

A managed object model allows Core Data to map from records in a persistent store to managed objects that you use in your application. The model is a collection of entity description objects (instances of NSEntityDescription). An entity description describes an entity (which you can think of as a table in a database) in terms of its name, the name of the class used to represent the entity in your application, and what properties (attributes and relationships) it has.

Walkthrough the creation of Entities, Attributes and Relationships [here](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/KeyConcepts.html)


More documentation on the same topic

Configuring entities [here](https://developer.apple.com/documentation/coredata/modeling_data/configuring_entities)<br>
Configuring attributes [here](https://developer.apple.com/documentation/coredata/modeling_data/configuring_entities)<br>
Configuring relationships [here](https://developer.apple.com/documentation/coredata/modeling_data/configuring_relationships)

## In Class Activity I (15 min)
Using the same app idea from last class, model how the relationships will work.

**Favorites:**
Lets create a User. A "logged in" *User* will have only one cart. You can add products to this cart.
We will also have favorites, a "logged in user" can favorite many products.

8. Create a *User* NSManagedObject.
9. There should be only one instance of a user in your app.
10. Add a favorites tab. Users can *favorite* products, and that will appeart on the favorites tab.

Then move to the model editor in a new project to map it out.

## In Class Activity I (40 min)

Clone/Download the repo below to get started:

[Shop Keep Starter](https://github.com/Product-College-Labs/shop-keep.git)

TODO:
Include the option to delete shops.<br>
Include functionality to add employees and managers.

Extra:
Include functionality to add shops.<br>
Include functionality to edit employees and managers.<br>
