referenced: [wonderful-objective-c-style-guide](https://github.com/markeissler/wonderful-objective-c-style-guide)

# Objective-C style guide.

## Language

US English should be used.

**Preferred:**

```
UIColor *myColor = [UIColor whiteColor];
```

**Not Preferred:**

```
UIColor *myColour = [UIColor whiteColor];
```

## Code Organization

Use `#pragma mark -` to categorize methods in functional groupings and protocol/delegate implementations following this general structure.

```
#pragma mark - Class Methods

+ (ClassObject)classWithDefaults;
+ (ClassObject)convertToJSON;
+ (ClassObject)convertToXML;

#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```

## Spacing

* **Method braces and other braces** (`if`/`else`/`switch`/`while` etc.) **always open on a new line and close on a new line**.

**Preferred:**

```
if (user.isHappy) {
  // Do something
}
else {
  // Do something else
}
```

**Not Preferred:**

```
if (user.isHappy)
{
    // Do something
}
else {
    // Do something else
}
```

* Prefer using auto-synthesis. But if necessary, `@synthesize` and `@dynamic` should each be declared on new lines in the implementation.

**Preferred:**

```
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```

**Not Preferred:**

```
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

## Documentation

The following items should be documented to facilitiate developer on-boarding, development of new functionality, and the ongoing maintenance cycle:

* Classes
* Prototype
* Constants
* Properties
* Class Methods
* Instance Methods

**Class Documentation**

```
-- **EXAMPLE PENDING** --
```

**Constant Documentation**

```
/**
 *  @memberof PDFReaderConfig
 *  Default value for bookmarksEnabled: TRUE
 */
extern const BOOL kPDFReaderDefaultBookmarksEnabled;
```

**Property Documentation**

```
/**
 *  Enable/disable bookmark support.
 *
 *  @see kPDFReaderDefaultBookmarksEnabled
 */
@property (nonatomic, readwrite, unsafe_unretained, getter=isBookmarksEnabled)
    BOOL bookmarksEnabled;
```

**Class Method Documentation**

```
/**
 * Returns the shared PDFReaderConfig instance, creating it if necessary.
 *
 * @return The shared PDFReaderConfig instance.
 */
+ (instancetype)sharedConfig;
```

**Instance Method Documentation**

```
/**
 *  Initializes and returns a newly allocated PDFReaderViewController object.
 *
 *  @param object Reference to an initialized PDFReaderDocument
 *
 *  @return Initialized class instance or nil on failure
 *
 *  @throws "<MissingArguments>" When object is nil
 *  @throws "<WrongType>" When object is not a reference to a PDFReaderDocument
 *    object
 *
 *  @remark Designated initializer.
 */
- (instancetype)initWithReaderDocument:(PDFReaderDocument *)object;

/**
 *  Update bookmark state for each page in the PDFReaderDocument's bookmarks
 *    list.
 */
- (void)updateToolbarBookmarkIcon;
```

## Naming

### Naming Conventions for Methods and Variables

**Preferred:**

```
UIButton *settingsButton;
NSString *pageTitle = @"My Title";
int pageCounter = 0;
```

**Not Preferred:**

```
UIButton *setBut;
NSString *string = @"My Title";
int c = 0;
```

### Naming Conventions for Constants and Macros
The following naming patterns may at first appear overly complex but the intention is to support a quick way for an engineer to determine the type (i.e. constant or macro), the origin, as well as the location of the item's declaration. The pattern breaks down like this:

  tPRE_Space_Name

Where:

| Element | Definition                   | Value       | Example                              |
| ------- | -----------------------------| ----------- | ------------------------------------ |
| t       | type = constant              | k*          | **k**MIX_MyClass_DefaultTitle        |
|         | type = macro                 | m*          | **m**BUZ_MyClass_doubleIt            |
| PRE     | three-letter prefix          | XXX         | k**XXX**_MyClass_MenuBarHeight       |
| Space   | unique namespace within tPRE | WindowSize  | kXXX\_**MyClass**\_WindowSize        |
| Name    | unique name within tPRE_Space| BorderColor | kZRE_MyClass\_**BorderColor**        |
|         |                              | isIphone    | mZBB_MyClass\_**isIphone**           |

The type (t) element must either be a "k" (for constant) or an "m" (for macro). Other fields are to be defined by the developer.

**Preferred:**

```
static const NSInteger kMIX_PDFReader_DefaultPagingViews = 3;
```

**Not Preferred:**

```
static NSTimeInterval const fadetime = 1.7;
```

#### Macro names

**Preferred**

```
#define mMIX_MacroLib_rgb(r,g,b) [UIColor colorWithRed:r/255.0f green:g/255.0f blue:b/255.0f alpha:1.0f]
```

**Not Preferred**

```
#define RGBColor(r,g,b) [UIColor colorWithRed:r/255.0f green:g/255.0f blue:b/255.0f alpha:1.0f]
```

**Property names** should be camel-case with the leading word being lowercase.

#### Instance variable names
**Preferred:**

```
@property (nonatomic, readwrite, strong) NSString *descriptiveVariableName;

// if/when needed
@synthesize descriptiveVariableName = _descriptiveVariableName;
```

**Not Preferred:**

```
id varnm;
...
@property (strong) id varnm;
...
@synthesize varnm;
```

### Naming Conventions for Enumerated Types

#### Enumerated Type names

**Preferred:**

```
typedef enum eMIX_UtilityLib_PlayerStateType : NSInteger eMIX_UtilityLib_PlayerStateType;
enum eMIX_UtilityLib_PlayerStateType : NSInteger {
  PlayerStateOff,
  PlayerStatePlaying,
  PlayerStatePaused
};

// using the NS_ENUM macro (preferred)
typedef NS_ENUM(NSInteger, eMIX_UtilityLib_PlayerStateType) {
  PlayerStateOff,
  PlayerStatePlaying,
  PlayerStatePaused
};
```

**Not Preferred:**

```
enum {
    PlayerStateOff,
    PlayerStatePlaying,
    PlayerStatePaused
};

typedef NSInteger PlayerState;
```

## Methods

**Preferred:**

```
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

**Not Preferred:**

```
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // Never do this.
```

## Variables

**Preferred:**

```
@interface MyAppTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

**Not Preferred:**

```
@interface MyAppTutorial : NSObject {
  NSString *tutorialName;
}
```

## Property Attributes

**Preferred:**

```
@property (nonatomic, readwrite, weak) IBOutlet UIView *containerView;
@property (nonatomic, readwrite, strong) NSString *tutorialName;
```

**Not Preferred:**

```
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (nonatomic) NSString *tutorialName;
```

## Dot-Notation Syntax

**Example:**

```
- (void)updateMyBackroundColor {
  // dot notation...
  self.bgColor = [UIColor blueColor];

  // is same as sending setBgColor message to self...
  [self setBgColor:[UIColor blueColor]];
}
```

It is because the getter and setter methods are still the underlying implementation involved that dot notation (and explicit messages to self) should generally be avoided within `init` and `dealloc` methods as discussed [here](http://qualitycoding.org/objective-c-init/#more-910). In these methods, access data members directly via the `_variableName`.

**Example:**

```
- (instancetype)init {
  self = [super init];
  if (self)
  {
    _bgColor = [UIColor whiteColor];
  }

  return self;
}
```

Outside of `init` and `dealloc`, dot-notation should **always** be used for accessing and mutating properties as it makes code more concise.

**Preferred:**

```
NSInteger arrayCount = [self.array count];
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**Not Preferred:**

```
NSInteger arrayCount = self.array.count;
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## Literals

**Preferred:**

```
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

**Not Preferred:**

```
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```

## Switch Statements and Case Label Blocks

```
switch (condition) {
  case 1:
    // ...
    break;

  case 2: {
    // ...
    // Multi-line example using braces
    break;
  }

  case 3:
    // ...
    break;

   default:
    // ...
    break;
}

```

When using an enumerated type for a switch, `default` is not needed.   For example:

```
kMIX_LeftMenuTopItemType menuType = kMIX_LeftMenuTopItemMain;

switch (menuType) {
  case kMIX_LeftMenuTopItemMain:
    // ...
    break;
  case kMIX_LeftMenuTopItemShows:
    // ...
    break;
  case kMIX_LeftMenuTopItemSchedule:
    // ...
    break;
}
```

## Private Properties

Private properties should be declared in class extensions (anonymous categories) in the implementation file of a class.

**For Example:**

```
@interface MyAppDetailViewController ()

@property (nonatomic, readwrite, strong) GADBannerView *googleAdView;
@property (nonatomic, readwrite, strong) ADBannerView *iAdView;
@property (nonatomic, readwrite, strong) UIWebView *adXWebView;

@end
```

## Image Naming

**Examples:**

* `RefreshBarButtonItem` / `RefreshBarButtonItem@2x` and `RefreshBarButtonItemSelected` / `RefreshBarButtonItemSelected@2x`
* `ArticleNavigationBarWhite` / `ArticleNavigationBarWhite@2x` and `ArticleNavigationBarBlackSelected` / `ArticleNavigationBarBlackSelected@2x`.

Images that are used for a similar purpose should be grouped in respective groups in an Images folder.

## Booleans

**Preferred:**

```
if (someObject) {
  // code...
}

if (![anotherObject boolValue])  {
  // code...
}
```

**Not Preferred:**

```
if (someObject == nil)
if ([anotherObject boolValue] == NO)
if (isAwesome == YES)     // Never do this.
if (isAwesome == true)    // Never do this.
```

If the name of a `BOOL` property is expressed as an adjective, the property can omit the “is” prefix but specifies the conventional name for the get accessor, for example:

```
@property (nonatomic, readwrite, unsafe_unretained, getter=isEditable) BOOL editable;
```

## Conditionals

**Preferred:**

```
if (!error) {
  return success;
}
```

**Not Preferred:**

```
if (!error)
  return success;
```

or

```
if (!error) return success;
```

### Conditional Expressions

**Preferred:**

```
BOOL continuousPlayEnabled = [[MediaAppPrefs sharedInstance] continuousPlay];
MediaAppTrack *nextMediaTrack = [MediaAppPlayer nextTrack];
if (continuousPlayEnabled && nextMediaTrack) {
  // play the next song
}
```

**Not Preferred:**

```
if ([[MediaAppPrefs sharedInstance] continuousPlay] && [MediaAppPlayer nextTrack]) {
  // play the next song
}
```

### Ternary Operator

**Preferred:**

```
NSInteger value = 5;
result = (value != 0) ? x : y;

BOOL isHorizontal = YES;
result = (isHorizontal) ? x : y;
```

**Not Preferred:**

```
result = a > b ? x = c > d ? c : d : y;

result = isHorizontal ? x : y;
```

## Return Statements

**Preferred:**

```
- (BOOL) playNext {
  BOOL continuousPlayEnabled = [[MediaAppPrefs sharedInstance] continuousPlay];
  MediaAppTrack *nextMediaTrack = [MediaAppPlayer nextTrack];

  return (continuousPlayEnabled && nextMediaTrack);
}
```

**Not Preferred:**

```
- (BOOL) playNext {
  return ([[MediaAppPrefs sharedInstance] continuousPlay] && [MediaAppPlayer nextTrack]);
}
```

## Class Constructor Methods

Where class constructor methods are used, these should always return type of `instancetype` and never `id`. This ensures the compiler correctly infers the result type.

```
@interface Airplane
+ (instancetype)airplaneWithType:(MyAppAirplaneType)type;
@end
```

## CGRect Functions

**Preferred:**

```
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```

**Not Preferred:**

```
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```

## Golden Path

When coding with conditionals, the left hand margin of the code should be the "golden" or "happy" path.  That is, don't nest `if` statements.  Bail out and return early. Multiple return statements are OK.

**Preferred:**

```
- (void)someMethod {
  if (![someOther boolValue]) {
  return;
  }

  //Do something important
}
```

**Not Preferred:**

```
- (void)someMethod {
  if ([someOther boolValue]) {
    //Do something important
  }
}
```

## Error handling

**Preferred:**

```
NSError *error;
BOOL success;
success = [self trySomethingWithError:&error];

if (!success) {
  // Handle Error
  // e.g.
  NSLog(@"Something bad just happened: %@", error);
}
```

**Not Preferred:**

```
NSError *error;

if (![self trySomethingWithError:&error]) {
  // Handle Error
}
```

## Singletons

Singleton objects should use a thread-safe pattern for creating their shared instance.

```
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  // thread-safe init
  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```

An optional addition to the above standard pattern is the following:

```
- (void)dealloc {

    // implement -dealloc & remove abort() when refactoring for
    // non-singleton use.
    abort();
}
```

## Line Breaks

For example:

```
self.productsRequest = [[SKProductsRequest alloc] initWithProductIdentifiers:productIdentifiers];
```

A long line of code like this should be carried on to the second line adhering to this style guide's Spacing section (two spaces).

```
self.productsRequest = [[SKProductsRequest alloc]
  initWithProductIdentifiers:productIdentifiers];
```
