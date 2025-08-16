## 🍴 The Menu App

### Lesson 1 - Introduction

This series is a contiuation of the "How to make an app in 8 days".

We are creating a new app in Xcode called "Menu".

The first thing we are going to is change the name of the `ContentView` to `MenuView`. Then we are going to add the images into the asset folder.

When it comes to renaming something like the `ContentView`, it is important that you use the `Refactor` tool. This will change the name where `ContentView` is being used. To do this, you can right click on the name you want to change, go down to `Refactor`, and click `rename`. 

When uploading assets to the asset library, it is good practice to add these into a folder. To create a folder, right click the navigational area in the asset manager and click `New folder`.

-----

### Lesson 2 - Swift Arrays

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

### Quiz:

If we wanted to access the first element in an array, what index would we use?

**Answer =** A (0)


An array is ideal for data where order matters. True or false?

**Answer =** B (True)


-----

### Lesson 3 - Swift Structures 

For each item on the menu, we need 3 peices of information:
- Image
- Name
- Prices

To manange the data in our app, we are going to use 


















