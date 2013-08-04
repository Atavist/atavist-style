These guidelines intend to make projects easier to work with, make codebases more readable, and make collaboration easier. 

These guidelines build on Apple's existing [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html).
Unless explicitly contradicted below, assume that all of Apple's guidelines apply as well.

After all, [style](http://alfiehanssen.com/images/dapperdan.jpeg) is everything.

## Xcode Project

* The physical files should be kept in sync with the Xcode project files in order to avoid file sprawl. Any Xcode groups created should be reflected by folders in the filesystem. Code should be grouped not only by type, but also by feature for greater clarity.
* When possible, always turn on "Treat Warnings as Errors" in the target's Build Settings and enable as many [additional warnings](http://boredzo.org/blog/archives/2009-11-07/warnings) as possible. If you need to ignore a specific warning, use [Clang's pragma feature](http://clang.llvm.org/docs/UsersManual.html#controlling-diagnostics-via-pragmas).

## Whitespace

 * Tabs, not spaces.
 * One line of whitespace in between methods.
 * One line of whitespace in between logical code blocks. 

## Organization

 * Use `#pragma mark`s to categorize methods into functional groupings and protocol implementations, following this general structure:

```objc
#pragma mark - Lifecycle

- (void)viewDidLoad {}

#pragma mark - Drawing

- (void)drawRect:(CGRect) {}

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - Another Functional Grouping

- (BOOL)canDoCoolThingsWithStuff:(Stuff *)stuff {}

#pragma mark - ATSuperclass

- (void)someOverriddenMethod {}

```

## Variables

 * Always declare atomicity before memory-management semantics.
 * Always declare memory-management semantics even on `readonly` properties.
 * Declare properties `readonly` if they are only set once in `-init`.
 * Declare properties `copy` if they return immutable objects and aren't ever mutated in the implementation.
 * If Xcode can automatically `@synthesize` the variable, then let it.
 * Never declare an ivar unless you need to change its type from its declared property.
 * Prefix instance variables with an underscore (just like when implicitly synthesized).
 * No space between an object type and the protocol it conforms to.
 * Properties should be camel-case with the leading word being lowercase.

```objc
@property (nonatomic, weak) id<Protocol> storyDelegate;
@property (nonatomic, strong) NSObject<Protocol> *object;
```
 
* Asterisks indicating pointers belong with the variable, i.e. `NSString *text` not `NSString* text` or `NSString * text`.
* Long, descriptive method and variable names are good, i.e. `UIButton *settingsButton;` not `UIButton *setBut;`.
* Single letter variable names should be avoided except in `for()` loops. 

## Methods

* There should be a space after the scope (-/+ symbol).
* No space after the closing paranenthesis of the return type, or before or after parentheses in argument type specification.
* No spaces between parentheses and their contents.
* A single space between an object argument's type and the `*`.

```objc
  - (BOOL)canDoCoolThingsWithStuff:(Stuff *)stuff andFriends:(NSArray *)friends {}
   ```
   
## Dot-notation vs. Brackets

* Always use dot-notation when accessing and mutating properties. Bracket notation is preferred in all other cases.

**This:**  
```objc
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**Not this:**
```objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## init and dealloc

* `dealloc` methods should be placed at the top of the implementation, directly after the `@synthesize` and `@dynamic` statements. `init` should be placed directly below the `dealloc` methods of any class.

## Private Property

* Private properties should be declared in anonymous categories in the implementation file of a class, never in the header file.

```objc
@interface Person ()

@property (nonatomic, strong) NSString *nickname;

@end
```

## Conditionals

 * One space after keywords and before their parentheses.
 * No spaces between parentheses and their contents.
 * Conditional bodies should always use braces.
 * No single line conditionals.

**This:**

```objc
if (!error) {
    return success;
}
```

**Not this:**

```objc
if (!error)
    return success;
```

**Or this:**

```objc
if (!error) return success;
```

* Braces should not occupy their own line, with the exception of the closing brace. 

**This:**

```objc
if (error) {

} else {

}
```

**Not this or any variation of this:**

```objc
if (error) 
{

} else 
{

}
```

## CGRect and Friends

 **This:**
 
```objc
  CGRect rect = (CGRect){0.0f, 0.0f, 100.0f, 100.0f};
   ```

**Not this:**

```objc
  CGRect rect = CGRectMake(0.0f, 0.0f, 100.0f, 100.0f);
   ```
   
## Blocks

 * Blocks should have a space between their return type and name.
 * Block definitions should omit their return type when possible.
 * Block definitions should omit their arguments if they are `void`.
 * Parameters in block types should be named unless the block is initialized immediately.

```objc
void (^blockName1)(void) = ^{
    // do some things
};

id (^blockName2)(id) = ^ id (id args) {
    // do some things
};
```
