# UserDefaults and Keychain

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:15      | Overview                  |
| 0:20        | 0:45      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 1:15        | 0:45      | In Class Activity II      |
| TOTAL       | 2:00      |                           |


## Class Materials

Slides:

[Intro To Persistence - Slides](intro-to-persistence.key)

## Why you should know this or industry application (optional) (5 min)

Explain why students should care to learn the material presented in this class.

## Learning Objectives (5 min)

- Identify use cases for persisting information in a plist.
- Use a plist to store data and retrieve it.
- Identify use cases for persisting information with UserDefaults in iOS
- Use UserDefaults to store data and retrieve it.

## The plist (15 min)

A property list, or plist, is an XML file that contains key-value data. In iOS, a common plist is the Info.plist file. An information property list file is a structured text file that contains essential configuration information for a bundled executable.

Typically the contents are structured using XML. The root XML node is always an array or a dictionary, whose contents are a set of keys and values describing the bundle. These values are used by the system to obtain information about the app and its configuration.

The file is called Info.plist by convention. The file name is case sensitive so it should have a capital letter I.

The file is created automatically by Xcode when you create a new project.

### Creating an Information Property List File

The easiest way to create an information property list file is letting Xcode create it for us. Every project we create in Xcode comes with a file named <project>-Into.plist. The file comes preconfigured with keys that every plist should have.

To edit the contents of the file, select the file in files inspector. Then double-click the value to select it and type a new value. Most of these values are specified as strings but Xcode also supports other types likes arrays, dictionaries, booleans, date, Data and numbers.

![plist](assets/plist.png)
This is an example of a default plist that gets created with every new project. To see the XML structure, we right-click on the file and choose Open As/ Source Code.

### Reading from a plist
We can save information in the form of key-value pairs in a plist. And here's how to read the information:

```Swift
func getPlist(key name: String) -> [String]?
{
  // we first check to see if the path exists before trying to read the content
    if  let path = Bundle.main.path(forResource: name, ofType: "plist"),
        let content = FileManager.default.contents(atPath: path)
    {
      // deserializing the data from xml as a plist, this will be returned as an array, but needs casting to [String]
        return (try? PropertyListSerialization.propertyList(from: content, options: .mutableContainersAndLeaves, format: nil)) as? [String]
    }
    return nil
}
```
#### Usage
```Swift
if let items = getPlist(key: "Name of your key in the plist") {
    print(items)
}
```

### Writing to a plist
Aside from manually adding new elements to the plist, we can also write to a it.

```Swift
let encoder = PropertyListEncoder()
encoder.outputFormat = .xml

let path = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0].appendingPathComponent("APIkey.plist")

do {
    let data = try encoder.encode("00000000000000")
    try data.write(to: path)
} catch {
    print(error)
}
```


### Adding keys
The default Into.plist file given by Xcode has the required keys, but it's possible that you will need to add more for your project. We can use the plist as a key-value data store.

To add a new item, right-click on the editor and select *Add Row*.
To change the value's type, click on the select button in the Type column.
To change the value, double-click on the Value column.
To remove a row, select it and hit Backspace.

## In Class Activity I (30 min)

### UserDefaults

UserDefaults allows to store Strings, Numbers, Dates, Data and
Arrays or Dictionaries

Usually should be used to store user preferences, can be used to store small amount of persistent information.

**Note:**

Should never be used for sensitive data as its not encrypted (eg. Authentication Token, passwords).

**Example - Storing a boolean indicating a user first downloaded(opened) an app**

```Swift
// Set
UserDefaults.standard.set(false, forKey: "FirstTimeUser")

// Get
let value = UserDefaults.standard.bool(forKey: "FirstTimeUser")
```

Items stored in UserDefault belong to an app. This means deleting your app will clear out its UserDefaults.


### Keychain

Is used to store sensitive information, such as passwords. All information is stored encrypted. Meaning you can use this to store sensitive user information.

**Keychain Use Case - Logging in a User**

For instance, when loggin in a *user*, you will typically have some token/secret that is used to authorize a user's requests to a server. That information should be stored in the keychain.

Items stored in the keychain belong to a container that is shared by the operating system.
This means that if you store a key-value pair in the keychain, and delete your app without clearing the keychain, that item will persist.


> An app can access only its own keychain items, or those shared with a group to which the app belongs. It can't manage the keychain container itself. - Apple

Apple’s API is arcane - Open Source Libraries such as
KeychainSwift will make your life easier!


## In Class Activity II (30 min)

### Encoding/Decoding

Encoding: Creating a binary/textual representation (that can
be stored on disk, transferred via network) from an object
graph

Decoding: Creating an object graph from a binary/textual
representation

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

```swift
let data = NSKeyedArchiver.archivedData(withRootObject: movie)
```

Unarchive

```
let unarchivedMovies = NSKeyedUnarchiver.unarchiveObject(with: data) as? Movie
```

### When to use NSCoding

Use NSCoding when main goal of persistence in your App is
to store the current state of the application
If you additionally want to create queries, need migrations,
etc, there are better solutions (e.g., CoreData)


## Challenges

1. Interate Cocoapods into a project(Trip Planner)
Download KeychainSwift though cocoapods to use the keychain:

[KeychainSwift Link](https://github.com/evgenyneu/keychain-swift#keychain_access_groups)

a. Using the trip planner app from MOB2, only bring up the login screen if the user hasn't logged in. If they have, take them straight to the list of trips.

b. Generate and store the Basic Auth token securely in the keychain.

c. When making a request that requires the API key, retrieve it securely to use in your request headers.


## Resources
[Plist - article](https://learnappmaking.com/plist-property-list-swift-how-to/)<br>
[Info.plist - Apple Docs](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html#//apple_ref/doc/uid/TP40009254-102276)<br>
[Apple Documentation on UserDefaults](https://developer.apple.com/documentation/foundation/userdefaults)
