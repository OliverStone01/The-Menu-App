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










