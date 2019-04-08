elements# Unit Testing

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:15      | Initial Exercise                |
| 0:15        | 0:05      | Objectives                  |
| 0:20        | 0:25      | Overview - Unit testing       |
| 0:45        | 0:30      | In Class Activity I                 |
| 1:15        | 0:10      | BREAK      |
| 1:20        | 0:10      | Given When Then      |
| 1:30        | 0:10      | In Class Activity II      |
| 1:40        | 0:05      | Wrap up      |
| TOTAL       | 1:45      |                           |

## Initial Exercise (15 min)

Complete/Go over solution for L02 Activity II.

## Why you should know this or industry application

We all know how time consuming it is to make manual testing. It looks something like this: We build and run the app, navigate a few screens, make a few taps and make sure everything works the right way. If everything is good we move on to repeating the same process for different test cases. With unit testing we can automate some of these processes to cut time in testing while still making sure our app works as intended.

## Learning Objectives (5 min)

1. Describe the importance of unit testing.
1. Define unit testing
1. Design & implement basic tests in an Xcode project.
1. Navigate Xcode to create and run tests.


## Overview (20 min)
### What is unit testing?

Unit testing is a level of software testing where individual units/ components of a software are tested. The purpose is to validate that each unit of the software performs as designed.

A unit is the smallest testable part of any software. (ex. a method)

### Benefits of unit tests

**Q:** What are some benefits that come to mind?
Brainstorm in a white board before reading the following suggestions.

The faster we can build features, the faster users get updates in their apps. We increase the pace in which we develop if we can trust our existing code while rolling out new features. Making sure the newly added code doesn't break our existing code. That's when unit tests really show their value.
- You can detect bugs earlier and fix them faster.
- Saving time means saving resources and money.
- Users are happy with an app that doesn't break with every update.
- Refactoring is easier and gives you more confidence to improve without breaking.

### What can we test?

- Models
- Methods
- Interactions with view controllers
- UI workflows

### The first unit test - An example

Steps:
1. Create a new project including unit test targets. We're not using UITests so you can uncheck that option.
1. For simplicity we'll use the storyboard, adding a title tp the current view controller.This is what we will test.
1. Move to the unit test file. We'll go over it first.

When opening the default file in the tests target: What you see here is a **test case**. A test case is a class containing several tests. It's good practice to have a test case for each class in the main target.

```Swift
import XCTest
@testable import UTDemo
```
Every test case needs to import the **XCTest** framework. It defines the **XCTestCase** class and the test assertions that we'll use later.

The second line imports the UTDemo module. All the code we write for the app will be in this module. By default, classes, structs, enums, and their methods are defined as **internal**. This means that they can be accessed within the module. But the test code lives outside of the module. To be able to write tests for your code, you need to import the module with the @testable keyword. This keyword makes the internal elements of the module accessible to the test case.

Next we’ll take a look at the class declaration:

```Swift
class TestingTestsTests: XCTestCase {
```

The **setUp()** method is called before the invocation of each test method in the class. Here, we can insert code that should run before each test.

The opposite of setUp() is **tearDown()**. This method is called after the invocation of each test method in the class. If we need to clean up after our tests, here's the right place to do it.

Now we can continue writing the test, add the following:

```Swift
func testTitle() {
        let storyboard = UIStoryboard(name: "Main", bundle: nil)
        let viewController = storyboard.instantiateInitialViewController() as! ViewController
        XCTAssertEqual("Practice Project", login.title)
}
```

This test creates an instance of ViewController and assigns it to the constant viewController. Then we call the `XCTAssertEqual(_, _)` function to check whether the result is what we expected.

1. Command + U to run all tests OR click the diamond button on each test.

Xcode compiles the project and runs the test. You should see all diamonds green, meaning all of the tests passed.


## In Class Activity I (30 min)

### Test No. 1

Now let's try doing the same thing for a different component in the app.

Add a UITextfield to a view controller, include a placeholder to it and test the integrity of the message, make sure it's the right one.

### Test No. 2

Sometimes we need to test things that are part of processing data, not necessarily graphical elements that we can see in the app. Testing business logic is even more important than testing how the app looks.

Let's simulate a scenario in which we need to test the following method.

```Swift
func vowelsInAString(string: String) -> Int {
       let vowels: [Character] = ["a", "e", "i", "o", "u", "A", "E", "I", "O", "U"]
       var numberOfVowels = 0
       for character in string {
           if vowels.contains(character) {
               numberOfVowels +=  1
           }
       }
       return numberOfVowels
   }
```

Add the method to you view controller and then write a test for it.

Stretch challenge: Just for fun and practice, try refactoring `vowelsInAString` to use the higher order function `reduce`.

### Test No. 3

We want to have a function that given a title, it formats it to have each word capitalized to become a title.

```Swift
func makeTitle(string: String) -> String {
    let words = string.components(separatedBy: " ")

    var headline = ""
    for var word in words {
        let firstCharacter = word.remove(at:word.startIndex)
        headline += "\(String(firstCharacter).uppercased())\(word) "
    }

    headline.remove(at:headline.endIndex)
    return headline
}
```

Write a test to make sure this works.

Stretch challenge: Try refactoring `makeTitle` to use the higher order function `map`.

## Overview/TT

### Given When Then

![givenwhenthen](assets/givenwhenthen.png)

**(5 min)** Take a few minutes to improve your tests and make the more descriptive using the Given When Test approach.

## In Class Activity II (10 min)

Try tests in a playground.<br>
Using the following code, your objective is to write a simple test to make sure we can instantiate TodoItem.

```Swift
import UIKit
import Foundation
import XCTest

struct TodoItem {
    let title: String
    let dueBy: Date?

    init(title: String) {
      // complete initializer
    }
}

class TodoTests: XCTestCase {

    override func setUp() {
        super.setUp()
    }
    override func tearDown() {
        super.tearDown()
    }

    func testTodo() {
      // test making an instance of the struct TodoItem
    }
}

TodoTests.defaultTestSuite.run()

```

## Wrap Up (5 min)
- Code Coverage, should we aim for 100% all the time?
- TDD discussion, how interested are you?
- Highly recommended to complete the tutorial listed in additional resources.
- Keep practicing with small tests.

## Additional Resources

1. [Unit testing tutorial](https://www.raywenderlich.com/709-ios-unit-testing-and-ui-testing-tutorial)
1. [XCTest in Apple's Docs](https://developer.apple.com/documentation/xctest)
1. [Book resource (not free)](https://roadfiresoftware.com/unit-testing-in-swift/)
1. [A LOT of testing resources](https://medium.com/flawless-app-stories/a-complete-list-of-articles-on-unit-testing-with-swift-from-2017-9be8f046ef25)
1. [Testing techniques](https://www.marisibrothers.com/2017/03/common-unit-testing-techniques-on-ios.html#1a)
1. [Example](https://gist.github.com/annjose/1baa75b0796d0d2fef1a10ab74d5bd65)
