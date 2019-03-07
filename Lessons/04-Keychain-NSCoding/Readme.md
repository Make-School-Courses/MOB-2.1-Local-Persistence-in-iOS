# Keychain and NSCoding

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:15      | Overview                  |
| 0:20        | 0:45      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 1:15        | 0:45      | In Class Activity II      |
| TOTAL       | 2:00      |                           |

<!-- [Intro To Persistence - Slides](intro-to-persistence.key) OLD SLIDES -->

## Why you should know this

At some point you'll need to handle sensitive data in an iOS app. We *never* want to just store or pass that data around as plain text, so we utilize Keychain in iOS to securely store that information. 

## Learning Objectives (5 min)
- Practice storing sensitive information with Keychain in iOS.
- Implement data storing/retrieval through Keychain.

## Overview (20 min)

### Keychain

The keychain services API gives an app a mechanism to store small bits of user data in an encrypted database called a keychain.

Is used to store sensitive information, such as passwords. All information is stored encrypted.

![keychain](assets/keychain.png)

**Keychain Use Case - Logging in a User**

For instance, when logging in a *user*, you will typically have some token/secret that is used to authorize a user's requests to a server. That information should be stored in the keychain.

Items stored in the keychain belong to a container that is shared by the operating system.
This means that if you store a key-value pair in the keychain, and delete your app without clearing the keychain, that item will persist.


> An app can access only its own keychain items, or those shared with a group to which the app belongs. It can't manage the keychain container itself. - Apple

Apple’s API might be complex at first - Open Source Libraries such as
[KeychainSwift](https://github.com/evgenyneu/keychain-swift) will make your life easier!

## In Class Activity I (30 min)
1. Intergate Cocoapods into a new project.
Download KeychainSwift though Cocoapods to use the keychain: [KeychainSwift Link](https://github.com/evgenyneu/keychain-swift#keychain_access_groups)

1. Simulate you're logging in to a service and getting back a token.

1. Generate and store the Basic Auth token securely in the keychain.

1. When making a request that requires the token (make a dummy method for it), retrieve it securely to use in your request headers.

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


## In Class Activity II (20 min)

Take the Movie class and in an Xcode project use it to store an instance of it using the NSKeyedArchiver.

- Combine it with UserDefaults to store the data with a key.
- Make it modular to reuse a save and load method in more than one place.


## Resources

1. [Apple Documentation on Keychain](https://developer.apple.com/documentation/security/keychain_services)
1. [Apple Documentation on NSKeyedArchiver](https://developer.apple.com/documentation/foundation/nskeyedarchiver)
