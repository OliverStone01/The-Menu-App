# 🍴 The Menu App

## Lesson 1 - Introduction

This series is a contiuation of the "How to make an app in 8 days".

We are creating a new app in Xcode called "Menu".

The first thing we are going to is change the name of the `ContentView` to `MenuView`. Then we are going to add the images into the asset folder.

When it comes to renaming something like the `ContentView`, it is important that you use the `Refactor` tool. This will change the name where `ContentView` is being used. To do this, you can right click on the name you want to change, go down to `Refactor`, and click `rename`. 

When uploading assets to the asset library, it is good practice to add these into a folder. To create a folder, right click the navigational area in the asset manager and click `New folder`.

-----

## Lesson 2 - Swift Arrays

Arrays are similar to variables but they are able to store mulitple peices of data. To initalise an array, we begin similarly to how we create a variable. Although, when declaring the data type, we use square brackets arround the data type. Then we use square brackets to contain the data that is seperated with commas:
```
var b:[Int] = [5, 10, 15, 20, 25]
```

To access data from the array, we call the array name with the index of the array (location inside the array) where the data we want to call is being stored:
```
print(b[0])
```

Its important to know that indexes start at 0. Its also important to know that the order of an array is also preserved. This means that if you need to keep your data in a specific order, using an array is a good idea. 

If you wanted to replace all the items inside of the array, you can do:
```
b = [100, 2000]
```

Or if you only wanted to change one specific item in the array, you can do:
```
b[0] = 100
```


-----

## Quiz:

If we wanted to access the first element in an array, what index would we use?

**Answer =** A (0)


An array is ideal for data where order matters. True or false?

**Answer =** B (True)


-----

## Lesson 3 - Swift Structures 

For each item on the menu, we need 3 peices of information:
- Image
- Name
- Prices

To manange the data in our app, we could use three diffrent arrays to store this data, but then all you are spliting up the data for one item 3 times.

Instead we are going to use `Structures`.

A structure is an array that contains key value pairs. For example:
- Price: value
- Name: value

We could define our function within the same file that contains our view, but its better practice to move this to its own file. To do this, we are going to right click on the folder that contains out files and assets in the file navigator area. Select 'new file -> IOS -> Swift file'. We can name this file `MenuItem`.

Inside of this new file, we are going to define our structure:
```
struct MenuItem {
    var name:String
    var price:String
    var imageName:String
```

Now we can go back to our `MenuView` file. What we are going to do now is create an array that is going to store all our menu items. Each menu item will be made up using the structure that we made called `MenuItem`. 

```
var menuItems:[MenuItem] = []
```

These items we put into this array that use the structure `MenuItem` are known as `instances`. 


-----

## Lesson 4 - Instances

To declare an instance, you need to do the following:
```
var firstItem = MenuItem(name: "Onigiri", price: "$1.99", imageName: "onigiri")
```

What about if you wanted one of the peices of data to be the exact same for every item. Well instead of typing it out each time, we can define this in our structure like this:
```
struct MenuItem {
    var name: String
    var price: String = "$2.99"
    var imageName: String
```

Now, when we want to set a instance, it will look like this:
```
var firstItem = MenuItem(name: "Onigiri", imageName: "onigiri")
```

To get access to the data now set in the instance, we use something called `Dot Notation`. First, you write the name of the instance followed by a dot (.) then the name of the item you are trying to access. Here is a print example:
```
print(firstItem.name)
```

The other thing we can do with structures, is we can add functions to them. For example:
```
struct MenuItem {
    var name: String
    var price: String = "$2.99"
    var imageName: String

    func testPrint() {
        print(name)
    }
}
```

What this now allows us to do is call to the function using dot notation like this:
```
firstItem.testPrint()
```

To declare an array of instances, we can do the following:
```
var Items:[MenuItem] = [MenuItem(name: "Onigiri", imageName: "omigiri"), MenuItem(name: "other", imageName: "other")]
```

As you can see, this can get difficult to read. What we can do is add line breaks:
```
var Items:[MenuItem] = [MenuItem(name: "Onigiri", imageName: "omigiri"),
                        MenuItem(name: "other", imageName: "other")]
```

Now I must use this and add all the items into our app in an array.


-----

## Lesson 5 - SwiftUI Lists

To display an array in the form of a list, we can do:
```
// Array
var wordList:[String] = ["Cactus", "Cheese", "Camera"]

// List
List(wordList) { word in
    Text(word)
}
```

As you can see, we use `word` (which can be called anything) to iterate through every item in the array displaying each item in a list.

Lets now do this with our new array in our app.

First, we need to modify our structure to set an id to each item. To do this, we add the `identifiable` tag. After, we also need to add the property (variable) to the struct called `id` and set the data type to `UUID`. This stands for `Universal Unique ID`. It provides a unique identifier for each item made with this structure:
```
struct MenuItem: Identifiable {
    var id: UUID = UUID()
    var name:String
    var price:String
    var imageName:String
}
```

```
List(menuItems) { item in
    Text(item.name)
}
```

This will create a very basic list. Now lets look at customising this layout.

```
List(menuItems) { item in
    HStack {
        Image(item.imageName)
          .resizable()
          .apectRatio(contentMode: .fit)
          .frame(height: 50)
          .cornerRadius(10)

        Text(item.name)
          .bold()

        Spacer()

        Text("$" + item.price)
    }
    .listRowSeperator(.hidden)
    .listRowBackground(
        Color(.brown)
            .opacity(0.1)
    )

}
.listStyle(.plain)
```

<img alt="Final" src="/image-assets/final.png" style="width:150px">

-----

## Lesson 6 - Complexity of larger apps

Everything we have build so far has only had one page for the view and storing data. This is good for learning, but with morecomplex apps there are a few more challenges we need to look at.

The first is files. At the moment, we are building our apps with one or two files. This is ok for these lightweight apps but as these apps get more complex, it is better to split up the app into segments to make it easier to work on parts of the app and for debugging.

The second is data. Apps generaly do not start with data pre written to them. Instead, when the app boots, it calls to a server or database where the data required is being stored. It will only collect data depending on what is required. This is becuase these apps are installed on mobile apps where performance is limited compared to super powerful computers and servers.

Finally, if you need to use a button or an element on every view of your app. Instead of writing out the element each time and coding it into each view. We can define it as an independent view and use it accross our app instead.


-----

## Lesson 7 - Structures Part 2

We are going to look at how we can split up our app into diffrent sections. Every view is a structure. Every app entry point is also a struct. 

It is important that you are not constanly duplicating code. To prevent this, if you find you need to use an element or logic you have created mulitplple times, then create it as a structure. 

This way, if you need to edit the code, you can do it in the structure and it will change it everywhere it has been used. 

Lets take a look at moving the data from the current menu app, to its own database service. In a new file called `DataService`, we can write the following code:
```
import Foundation

struct DataService {

    func getData() -> [MenuItem] {

        return [MenuItem(name: "Onigiri", price: "1.99", imageName: "onigiri"),
                                MenuItem(name: "Meguro Sushi", price: "5.99", imageName: "meguro-sushi"),
                                MenuItem(name: "Tako Sushi", price: "4.99", imageName: "tako-sushi"),
                                MenuItem(name: "Avocado Maki", price: "2.99", imageName: "avocado-maki"),
                                MenuItem(name: "Tobiko Spicy Maki", price: "4.99", imageName: "tobiko-spicy-maki"),
                                MenuItem(name: "Salmon Sushi", price: "4.99", imageName: "salmon-sushi"),
                                MenuItem(name: "Hamachi Sushi", price: "6.99", imageName: "hamachi-sushi"),
                                MenuItem(name: "Kani Sushi", price: "3.99", imageName: "kani-sushi"),
                                MenuItem(name: "Tamago Sushi", price: "3.99", imageName: "tamago-sushi"),
                                MenuItem(name: "California Roll", price: "3.99", imageName: "california-roll"),
                                MenuItem(name: "Shrimp Sushi", price: "3.99", imageName: "shrimp-sushi"),
                                MenuItem(name: "Ikura Sushi", price: "5.99", imageName: "ikura-sushi")]

    }
}

```

Now, we can change the array that is in our main view to be empty array of `MenuItem`:
```
var menuItems:[MenuItem] = [MenuItem]()
```


-----

## Lesson 8 - State and Updating Views

When an app requires data, it displays a temp screen like a loading screen or a spinner, then it requests data to a `DataService` which then sends a data request to a database. The database will then send the data to the DataService which is then returned to the main view and displayed.

Lets now implement this in our menu app. We laid out the basics in the last lesson, but now we are going to have the view call to the data service to request the data being stored. We then need the view to detect that its been assigned this data and to update the view.

What we did last lesson in the view is make the array that was holding the data an empty array. This has caused the UI to be blank becuase the list was getting its data from this array.

To tell the view to update automatically is by adding the modifier `@State` to the begining of the empty array. This will tell the app that the UI depends on the array and if it changes, update to the latest. 

`@State` is a property wrapper. 

We are going to also add the modifier `.onAppear` to the list element. First at the top of the pagem we are going to create a variable that calls to the function `DataService:
```
var dataService = DataService()
```

Now we can call to this using the `.onAppear` modifier:
```
}
.onAppear {
    menuItems = dataService.getData()
}
```

As you can see, we are then assigning the data returned to the `menuItems` which updates the list. 


-----

## Lesson 9 - Reusing your views

let's now look at how we can have diffrent views in the app and specifically how we can change the main screen that is displayed when the app is launched. 

First, lets create a new `SwiftUI View` file called `TestView`.

To now change the inital loading view, we can go into the `view_testApp` file and under `WindowGroup`, lets change the view loaded by doing:
```
WindowGroup {
    TestView
}
```

Say we now have multiple pages in our app and we want to create a reusable ui template. For example a button that appears on multiple views. To do this, we can create a new `Swift UI View` called `customButton`. 

We can get rid of everything inside of the view for now and replace it with a button.
```
import SwiftUI

struct CustomButton: View {

    var body: some View {
        Button {

        } label: {
            Text("My button")
                .padding()
                .border(.green)
        }
    }
}           
```

To then use this button anywhere, we can go to another view and add it using:
```
CustomButton()
```

We can make this dynamic for example by making the text element be able to change on each view:
```
import SwiftUI

struct CustomButton: View {

    var buttonText: String

    var body: some View {
        Button {

        } label: {
            Text(buttonText)
                .padding()
                .border(.green)
        }
    }
}
```

Now, when we create an instance of this button in another view, we need to provide text for the button by doing:
```
CustomButton(buttonText: "New Text")
```

-----
