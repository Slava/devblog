Recently I started learning Objective-C and Cocoa framework. I thought it would be easy as I already have some experience with C# and Java. But it appears to be not that easy. Here are some notes I took to map Objective-C to C#.

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
- In NSLog `%@` accepts object pointer and expands it to string by calling `[obj description]`.
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

### Manual memory management rules
- If you create an object by using a method whose name starts with `alloc` or `new` or contains `copy`, you have taken ownership of it. (That is, assume that the new object has a retain count of 1 and is not in the `autorelease pool`.) You have a responsibility to release the object when you no longer need it. Some of the common methods that convey ownership are `alloc` (which is always followed by an `init` method), `copy`, and `mutableCopy`.
- An object created through any other means, such as a convenience method, is not owned by you. (That is, assume that it has a retain count of 1 and is already in the autorelease pool and thus doomed unless it is retained before the autorelease pool is drained.)
- If you don’t own an object and want to ensure its continued existence, take ownership by sending it the message retain. (This increments the retain count.)
- When you own an object and no longer need it, send it the message `release` or `autorelease`. (The message release decrements the retain count immediately; autorelease causes the message release to get sent when the `autorelease pool` is drained.)
- As long as it has at least one owner, an object will continue to exist- (When its retain count goes to zero, it is sent the message `dealloc`.)

### Controls
#### `NSButton`
Can be oval, square, checkbox. Most common messages sent to buttons:

```objectivec
- (void)setEnabled:(BOOL)yn
- (NSInteger)state
- (void)setState:(NSInteger)aState
```

#### `NSSlider`
Used to select values in ranges. Can be vertical, horizontal and circular. Can send messages continiously while dragging and can send once on mouse button release. Can have markers and prevent selecting values between markers. Two most used messages:

```objectivec
- (void)setFloatValue:(float)x
- (float)floatValue
```

#### `NSField`
Single line input field. Uneditable fields are used as labels.  `NSSecureTextField` is subclass which is used for passwords. 

```objectivec
- (NSString *)stringValue
- (void)setStringValue:(NSString *)aString
- (NSObject *)objectValue
- (void)setObjectValue:(NSObject *)obj
```

Second pair is used in case you use `NSFormatter`s or just `description` method of object.

### My mappings for Cocoa objects

- `NSMutableArray <=> vector`
- `NSString <=> string`
- `for (LotteryEntry *entryToPrint in array) <=> foreach`
- `NSAssert <=> assert`


