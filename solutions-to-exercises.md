# Solutions to Exercises

## Objects: United Data and Operations

### A String Object

 I named the object `sloganString`. Inside the object, I placed the data, which is the string `"Just Do It!"`. I also changed the name of the data variable from `slogan` to `value`. Since the object name itself already represents both the data and the functions, repeating the name `slogan` inside it would be unnecessary. Along with the data, the object also contains the two functions. These functions do not need parameters because their bodies can directly access the data through `value = "Just Do It!"`.

 In a real program, we could simply reuse the earlier utility functions inside these methods rather than rewriting the full logic again. However, if we imagine a design where every string in our program is treated as an object with its own methods, then this approach is perfectly fine.

 ```text
sloganString = {
    value = "Just Do It!"
   
    function uppercase() {
        newStr = ""
        length = getStringLength(value)
        for (i = 0; i < length; i++) {
            character = getCharacterAt(value, i)
            asciiValue = getASCIIValue(character)
            if (asciiValue >= 97 and asciiValue <= 122) {
                uppercaseASCII = asciiValue - 32
                uppercaseChar = getCharacterFromASCII(uppercaseASCII)
                newStr = newStr + uppercaseChar
            } else {
                newStr = newStr + character
            }
        }
        return newStr
    }
   
    function lowercase() {
        newStr = ""
        length = getStringLength(value)
        for (i = 0; i < length; i++) {
            character = getCharacterAt(value, i)
            asciiValue = getASCIIValue(character)
            if (asciiValue >= 65 and asciiValue <= 90) {
                lowercaseASCII = asciiValue + 32
                lowercaseChar = getCharacterFromASCII(lowercaseASCII)
                newStr = newStr + lowercaseChar
            } else {
                newStr = newStr + character
            }
        }
        return newStr
    }
   
}


// Usage:
upperSlogan = sloganString.uppercase()  // "JUST DO IT!"
lowerSlogan = sloganString.lowercase()  // "just do it!"
 ```

### A Counter Object

 I did several things in this solution. I kept the name `counter` for the object variable itself, but I changed the original variable to `currentValue`. I also added another variable called `endValue` to represent the final value of the counter. Inside the object I placed two functions: the first one increments the counter, and the second one checks if the counter has reached its end value.

I decided to reverse the condition in the check function because it is not common to name a method negatively. For example, I could have named it `isNotDone()` and kept the original logic, but then using it in code would look awkward, such as `while (not counter.isNotDone())`. Writing it positively as `isDone()` makes the condition easier to read and understand.

I could add other methods as well, for example, to get the current value, reset the counter, or change the end value, but for illustration purposes, I kept the object simple.

```text
counter = {
    currentValue = 0
    endValue = 10
   
    function increment() {
        currentValue++
    }
   
    function isDone() {
        return currentValue >= endValue
    }  
}


// Usage:
while (not counter.isDone()) {
    // code


    counter.increment()
}
```

### An Array Object

The process is the same, I put the array and its related operations inside the object. Here I kept the name `colors` for the object and changed the internal array name to `items`. I also adjusted the method names a little, because the methods already belong to the array object, so it would be redundant to mention “array” again in their names.

```text
colors = {
    items = ['red', 'green', 'blue', 'yellow', 'purple']
   
    function count() {
        return count(items)
    }
   
    function exists(color) {
        return inArray(items, color)
    }
   
    function add(color) {
        addToArray(items, color)
        return true
    }
   
    function remove(color) {
        if (inArray(items, color)) {
            removeFromArray(items, color)
            return true
        }
        return false
    }
   
    function getItems() {
        return items
    }
}


// Usage:
colors.count()           // count the elements in the array
colors.exists('red')  // check if an element exists in the array
colors.add('white')  // add an item to the array
colors.remove('blue')  // remove an item from the array
```

### Text File Object

I took everything that was inside the original object and moved it out into the global scope. Many of the functions that were part of the object are no longer necessary because the data can now be accessed directly. I renamed the `textFile.load()` and `textFile.getSize()` methods to `loadFile()` and `getFileSize()` functions. Since they are no longer part of the `textFile` object, they don’t carry the object’s name as a prefix, and just from the function name it’s not immediately obvious what they do. That is why I kept the word File in the function names, so their purpose is still clear. You could even go further and remove the `loadFile()` and `getFileSize()` functions completely, using the low-level functions directly instead. But I think keeping these two functions is useful, because they make the program easier to read and understand.

```text
// Global variables to store file state
content = ""
exists = false
error = ""


// Function to load a file
function loadFile(filepath) {
    error = ""
   
    // Check if file exists using low-level OS function
    exists = fileExists(filepath)
   
    if (!exists) {
        error = "File does not exist - " + filepath
        return false
    }
   
    // Read all content using low-level file operations
    content = readAllText(filepath)
   
    if (content == null) {
        error = "Could not read file - " + filepath
        return false
    }
   
    return true
}


function getFileSize() {
    if (!exists) {
        return 0
    }
    return getStringLength(content)
}


// Usage
success = loadFile("example.txt")
if (success) {
    show("File content: " + content)
    show("File size: " + getFileSize() + " characters")
} else {
    show("Error: " + error)
}
```