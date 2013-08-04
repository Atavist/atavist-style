These guidelines build on Apple's existing [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html).
Unless explicitly contradicted below, assume that all of Apple's guidelines apply as well.

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
 * Don't use `@synthesize`.
 * Never declare an ivar unless you need to change its type from its declared property.
 * Instance variables should be prefixed with an underscore (just like when implicitly synthesized).
 * Don't put a space between an object type and the protocol it conforms to.
 
```objc
@property (nonatomic, weak) id<Protocol> delegate;
@property (nonatomic, strong) NSObject<Protocol> *object;
```
 
* Long, descriptive method and variable names are good. Single letter variable names should be avoided except in `for()` loops. 
* Asterisks indicating pointers belong with the variable, i.e. `NSString *text` not `NSString* text` or `NSString * text`.

This: `UIButton *settingsButton;`, and not this: `UIButton *setBut;`


## Methods

* There should be a space after the scope (-/+ symbol).
* No space after the return type.
* No space on either side of the `:`.
* A single space between an object argument's type and the `*`.

```objc
  - (BOOL)canDoCoolThingsWithStuff:(Stuff *)stuff andFriends:(NSArray *)friends {}
   ```

## CGRect Declarations

 * This:
 
```objc
  CGRect rect = (CGRect){0.0f, 0.0f, 100.0f, 100.0f};
   ```

* Not this:

```objc
  CGRect rect = CGRectMake(0.0f, 0.0f, 100.0f, 100.0f);
   ```

## Dot-notation Vs. Brackets

Dot-notation should **always** be used for accessing and mutating properties. Bracket notation is preferred in all other instances.

**For example, this:**  
```objc
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**Not this:**
```objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## Conditionals

 * Put a single space after keywords and before their parentheses.
 * No spaces between parentheses and their contents.
 * Conditional bodies should **always** use braces.

**For example:**
```objc
if (!error) {
    return success;
}
```

**Not:**
```objc
if (!error)
    return success;
```

or  

```objc
if (!error) return success;
```

* Braces should not occupy their own line, with the exception of the closing brace. This:

```objc
if (error) {

} else {

}
```

Not this or any variation of it:

```objc
if (error) 
{

} else 
{

}
```

## Private Properties

* Private properties should be declared in anonymous categories in the implementation file of a class, never in the header file.

```objc
@interface Person ()

@property (nonatomic, strong) NSString *nickname;

@end
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
