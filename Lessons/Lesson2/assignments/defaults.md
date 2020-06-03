## UserDefaults & Property Wrappers

Let's say we want to manage saving a user's token with UserDefaults. We will be accessing this token in several parts within the app. We can make the process of requesting data much easier if we have the UserDefault request in one place only, in a way that we can reuse that piece of code. (Similar to what we did with the Plist)

Complete the implementation of this helper struct and then test it in an empty project to see if you can successfully store and retrieve the token.

```Swift
   struct Defaults {

        static let token = "token"
        static let tokenKey = "tokenKey"

        struct Model {
            var token: String?

            init(token: String) {
              //complete the initializer
            }
        }

        static var saveToken = { (token: String) in
          //complete the method
        }

        static var getToken = { () -> Model in
          //complete the method
        }

        static func clearUserData(){
          //complete the method using removeObject
        }
    }

```

## What if...?

We not only want to save the token, but also the first time the user entered a section of the app, or user settings, whether they prefer light or dark mode, language selection etc.

That's a lot of structs we need to back up with UserDefaults.

<!-- > -->

## Property Wrappers

We can solve the inconvenience using Property Wrappers, introduced in Swift 5.1

First read about what they are in [this article](https://www.swiftbysundell.com/articles/property-wrappers-in-swift/) by John Sundell. (Stop when you get to the  Decoding and overriding section)

Before you read about it, think how you can improve the implementation of your `Defaults` struct.

Now take a look at how this article combines property wrappers with UserDefaults and see if you can adjust your implementation to store:

- Token : String
- FirstTimeUser : Bool
- DarkMode: Bool
- Languague : String (Ex. EN, SP) note: always capitalized


Complete the assignment for this activity on [Gradescope](https://www.gradescope.com).
