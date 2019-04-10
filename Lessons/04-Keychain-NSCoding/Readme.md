# Keychain and NSCoding

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:10      | Initial Exercise          |
| 0:10        | 0:05      | Objectives                |
| 0:15        | 0:20      | Overview I                |
| 0:35        | 0:45      | In Class Activity I       |
| 1:20        | 0:10      | BREAK                     |
| 1:30        | 0:10      | Overview II               |
| 1:40        | 0:05      | Wrap Up                   |
| TOTAL       | 1:45      |                           |

## Initial Exercise (10 min)

Review/Go over test activity from last class.

## Why you should know this

At some point you'll need to handle sensitive data in an iOS app. We *never* want to just store or pass that data around as plain text, so we utilize Keychain in iOS to securely store that information.

## Learning Objectives (5 min)
- Describe how to handle the Keychain in iOS.
- Implement data storing/retrieval through Keychain.

## Overview (20 min)

### Keychain

Apps often need access to sensitive user data such as passwords, but keeping the data secure can come at a cost:

Storing data without any encryption = **security risk!**

Prompting the user all the time = **bad user experience!**

Keychain services helps solve this problem by providing easy access to encrypted storage. Your app uses the keychain, along with minimal user interaction, to provide a good user experience.

The keychain services API gives an app a mechanism to store small bits of user data in an encrypted database called a keychain.

Is used to store sensitive information, such as passwords. All information is stored encrypted.

![keychain](assets/keychain.png)

### Things to know
- Is used to store sensitive information, such as passwords, credit card information, or notes.
- All information is stored encrypted.
- Items stored in the keychain belong to a container that is shared by the operating system.
- This means that if you store a key-value pair in the keychain, and delete your app without clearing the keychain, that item will persist.

### How?
Keychain Services consists of two parts: an encrypted database and items inserted into the database .

![keychainhow](assets/keychainhow.png)


**Keychain Use Case - Logging in a User**

Saving a password.

![example](assets/example.png)

The keychain is automatically unlocked when the user unlocks the device and then locked when the device is locked.

> An app can access only its own keychain items, or those shared with a group to which the app belongs. It can't manage the keychain container itself. - Apple

### Terminology

`SecKeychain` 				 - this is the database

`SecKeychainItem			 - this is the item saved to the database`

`SecItemAdd(_:_:)` 			 - adding an item

`SecItemCopyMatching(_:_:)` 	 - searching for an item

`SecItemUpdate(_:_:)` 		 - updating an item

`SecItemDelete(_:)` 			 - deleting an item

`kSecAttrSynchronizable`		 - make the item sync with iCloud

Apple’s API might be complex at first - Open Source Libraries such as
[KeychainSwift](https://github.com/evgenyneu/keychain-swift) will make your life easier!

- Get, set and delete string, boolean and Data Keychain items
- Specify item access security level
- Synchronize items through iCloud
- Share Keychain items with other apps


## In Class Activity I (45 min)
1. Intergate Cocoapods into a new project.
Download KeychainSwift though Cocoapods to use the keychain: [KeychainSwift Link](https://github.com/evgenyneu/keychain-swift#keychain_access_groups)

1. The idea is to practice how to handle Keychain while using best practices to implement an intermediary layer between the third party library and your project. This means we only want to use a single instance of KeychainSwift in the entire project in case we were to use it in several view controllers.

1. Create a very simple UI for your demo. Maybe something similar to this:
![keychaindemo](assets/keychaindemo.png)

1. Make sure you implement saving an item, updating it, retrieving it and showing it (when created and modified) and deleting it.

When you finish, you will have a class that you can reuse in other projects to manage storing sensitive data in Keychain. 😀

### NSKeyedArchiver (Review)

NSKeyedArchiver encodes and decodes classes as long as they are NSCoding compliant.

NSCoding is a protocol that requires two methods — required init(coder decoder: NSCoder) and encode(with coder: NSCoder). If we have a class that conforms to NSObject AND NSCoder, then that class can be serialized and deserialized into data that can be saved to a user’s disk.

Encoding: Creating a binary representation (that can be stored on disk, transferred via network) from an data structure.

Decoding: Creating a data structure from a binary/textual representation.

**Implementing NSCoding**

To Encode/Decode, your class has to be NSCoding compliant. That means it has to conform to NSCoding. This gives you two methods that correspond to decoding an object, and encoding it.


#### Step 1: Implement NSCoding

```swift
class Movie: NSObject, NSCoding {
    var title: String
    var duration: Int

    init(title: String, duration: Int) {
        self.title = title
        self.duration = duration
    }

    required convenience init?(coder aDecoder: NSCoder) {
        guard let title = aDecoder.decodeObject(forKey: "title") as? String
            else { return nil }
        let duration = aDecoder.decodeInteger(forKey: "duration")

        self.init(title: title, duration: duration)
    }

    func encode(with aCoder: NSCoder) {
        aCoder.encode(self.title, forKey: "title")
        aCoder.encode(self.duration, forKey: "duration")
    }
}

```

#### Step 2: User Archiver - Archiving to filesystem

Archive

```Swift
NSKeyedArchiver.archivedData(withRootObject: someObject, requiringSecureCoding: false)
```

Unarchive

```Swift
NSKeyedUnarchiver.unarchiveTopLevelObjectWithData(someData)
```

A keyed archive differs from a non-keyed archive in that all the objects and values encoded into the archive are given names, or keys. When decoding a non-keyed archive, values have to be decoded in the same order in which they were encoded. When decoding a keyed archive, because values are requested by name, values can be decoded out of sequence or not at all.


## After Class

Take the Movie class and in an Xcode project use it to store an instance of it using the NSKeyedArchiver.

- Combine it with UserDefaults to store the data with a key.
- Make it modular to reuse a save and load method in more than one place.


## Resources

1. [Slides](https://docs.google.com/presentation/d/1f4T6j-mC32A7dK1j6ygw0lSoCB6VZ83FMQGaONORAG4/edit?usp=sharing)<br>
1. [Apple Documentation on Keychain](https://developer.apple.com/documentation/security/keychain_services)<br>
1. [Apple Documentation on NSKeyedArchiver](https://developer.apple.com/documentation/foundation/nskeyedarchiver)<br>
1. [Keychain dive in - article](https://medium.com/halcyon-mobile/diving-into-keychain-services-c71782313a3c)<br>
1. [Using keychain to manage user secrets](https://developer.apple.com/documentation/security/keychain_services/keychain_items/using_the_keychain_to_manage_user_secrets)<br>
1. [Keychain items](https://developer.apple.com/documentation/security/keychain_services/keychain_items)
1. [Library used](https://github.com/evgenyneu/keychain-swift)
