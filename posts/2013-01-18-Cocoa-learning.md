Recently I started learning Objective-C and Cocoa framework. I thought it would be easy as I already have some experience with C### and Java. But it appears to be not that easy. Here are some notes I took to map Objective-C to C#.

### Objective-C
- Weakly typed
- Object oriented
- Has manual memory management (Arc)
- Uses LLVM or GCC compiler
- Using LLVM we can combine C, C++, Objective-C code in one file

### Cocoa
Three main frameworks:

- Foundation (Strings, Dates, etc)
- AppKit (UI related framework)
- Core Data (persistence framework)

### Naming conventions
- `NSObject` class names are capitalized
- `dealloc` method names are started with lowercase
- camelCase for local vars

### Some new info for me

- Instance variables that are pointers to other objects are called outlets. 
- Methods that can be triggered by user interface objects are called actions.
- Single inheritance
- Objective-C keywords are prefixed with `@` sign
- Option+Click on any piece of code shows docs
- `@` sign before string literal means Objective-C string class `NSString`
- NSLog has printf-like syntax, but has different identifiers (`%d`, `%qi` for `long long`, `hi` for `short`, etc)
- `NSObject.isEqual:anotherObject` by default compares pointers
- Methods starting with `-` are instance methods, starting with `+` are class methods, or static methods
- ARC - automatic reference count is GC and can be disabled for project for manual memory management

### Some types and constants
- `id` is pointer to any type of object
- `BOOL` is the same as `char` but is used as Boolean
- `YES` is 1, `NO` is 0
- IBOutlet is a macro that avaluates to nothing. Ignore it. (`IBOutlet` is a hint to Interface Builder).
- IBAction is the same as `void`. It also acts as a hint to Interface Builder
- `nil` is the same as NULL. We use `nil` instread of `NULL` for poiners to objects.
- `NSArray` can not have `nil` in it
- `NSArray`, `NSNumber` and `NSString` are immutable

### My mappings for Cocoa objects

- `NSMutableArray <=> vector`
- `NSString <=> string`
- `for (LotteryEntry *entryToPrint in array) <=> foreach`
- `NSAssert <=> assert`


