# ios-style-guide
iOS Style Guide

Нужно вызывать методы заключая их в скобки, а свойства вызывать через точку.

**Верно:**
```objc
array.count;
[UIApplication sharedApplication].delegate;
```

**Не верно:**
```objc
[array count];
UIApplication.sharedApplication.delegate;
```

Скобки нужно ставить в стиле K&R (на жаргоне "египетские").

**Верно:**
```objc
- (void)describeCodingStyleWithCodingStyle:(MCSCodingStyle)style {
    if (MCSCodingStyleKAndR == style) {
        [self doSomething];
    } else {
        [self doSomething];
    }
}
```

**Не верно:**
```objc
- (void)describeCodingStyleWithCodingStyle:(MCSCodingStyle)style 
{
    if (MCSCodingStyleKAndR == style) 
    {
        [self doSomething];
    }
}
```

Всегда присваеваем значения переменной сразу после объявления.

**Верно:**
```objc
NSObject *object = nil;
NSArray *array = @[];
```

**Не верно:**
```objc
NSObject *object;
// some actions
```

Не нужно ставить лишних пробелов. Нужно всегда использовать одинарный пробел. (Если есть сомнения, то можно проверить себя выделив кусок кода, затем нажав правую клавишу, затем Structure -> Re-Indent)

**Верно:**
```objc
- (BOOL)tableView:(UITableView *)tableView canMoveRowAtIndexPath:(NSIndexPath *)indexPath;

NSObject *object = nil;
```

**Не верно:**
```objc
- (BOOL) tableView: (UITableView *) tableView canMoveRowAtIndexPath: (NSIndexPath *) indexPath;
-(BOOL)tableView:(UITableView*)tableView canMoveRowAtIndexPath:(NSIndexPath*)indexPath;

NSObject * object     =      nil;
```

Если у функции много переменных то можно разбить объявление функции на несколько строк. В таком случае нужно поставить закрывающую скобку на следующей строке. Аналогично можно поступить с вызовом функции в коде.

**Верно:**
```objc
- (void)observeValueForKeyPath:(NSString *)keyPath
                      ofObject:(id)object
                        change:(NSDictionary *)change
                       context:(void *)context
{

}
```

При объявлении переменных не следует ставить лишних пробелов. Следует называть переменные таким образом, чтобы было понятно их назначение. Иногда для понятности можно в имени переменной использовать название класса. 

**Верно:**
```objc
NSArray *array = ...
UIButton *cancelButton = ...
```

**Не верно:**
```objc
NSArray* array = ...
NSArray * array = ...
NSObject * object     =      ...
NSObject *o1 = ...
```

Следует использовать свойства вместо простого объявления переменных. Следует инкапсулировать свойства в .m файле, если они не должны использоваться извне класса.

**Верно:**
```objc
@interface MCSObject: NSObject

@property (nonatomic, strong, readonly) NSManagedObjectContext *managedObjectContext;
@property (nonatomic, weak) IBOutlet UILabel *detailDescriptionLabel;
@property (nonatomic) BOOL selected;

@end
```

**Не верно:**
```objc
@interface CustomObject : NSObject {
    NSString *title;
}
```

Следует использовать константы вместо дефайнов.

**Верно:**
```objc
// MCSCompany.h
extern NSString * const MCSCompanyTagline;

// MCSCompany.m
NSString * const MCSCompanyTagline = @"We make award-winning apps for Apple devices.";

static NSString * const kOfficeLocation = @"Warsaw, Poland";
```
**Не верно:**
```objc
#define CompanyTagline @"We make award-winning apps for Apple devices."
#define maxNumberOfRows 2
```

Не следует синтезировать переменные самостоятельно (не нужно использовать @synthesize). Компилятор делает это автоматически.

**Не верно:**
```objc
@synthesize myButton = _myAwesomeBtn
```

Не следует использовать переменные класса напрямую (с нижним подчеркиванием). Всегда следует использовать свойства. Переменные напрямую следует использовать только в методах доступа.

**Верно:**
```objc
self.someProperty = ...
```
**Не верно:**
```objc
_someProperty = ...
```

Следует комментировать сложные участки кода и функции в .h файле. В идеале все функции в .h файле должны быть задокументированы при помощи специальных комментариев поддерживаемых Xcode'ом.

**Верно:**
```objc
/**
* This function do ...
*
* @param obj An object.
* @return Some array.
*/
- (NSArray)someFunction:(NSObject *)obj;

/// Short documentation for function
- (NSArray)someFunction:(NSObject *)obj;
```

Следует использовать [литералы](http://clang.llvm.org/docs/ObjectiveCLiterals).

**Верно:**
```objc
NSArray *names = @[@"Agata", @"Ania", @"Bartek", @"Daniel", @"Dawid", @"Dominik", @"Jarek",
@"Karol", @"Klaudia", @"Maciej", @"Maciej", @"Marcin", @"Rafał", @"Wojtek",
@"Wojtek", @"Zbigniew", @"Janek"];
NSDictionary *animals = @{@"dogs" : @[@"Boomer"]};
NSNumber *officeIndoorSwimmingPool = @YES;
NSNumber *over9000 = @9001;
```

Следует использовать перечисления следующего вида.

**Верно:**
```objc
// MCSFishEye.h

typedef NS_ENUM(NSInteger, MCSFishEyeState) {
    MCSFishEyeStateCollapsed,
    MCSFishEyeStateExpandedActive,
    MCSFishEyeStateExpandedPassive
};

typedef NS_OPTIONS(NSUInteger, MCSCustomerHappiness) {
    MCSCustomerHappinessVeryHapy = 1 << 0,
    MCSCustomerHappinessExtremelyHappy = 1 << 1,
    MCSCustomerHappinessEnormouslyHappy = 1 << 2
};
```

Не следует перегружать бушевские выражения в условиях.

**Верно:**
```objc
if (!someObject) {
}

if (isAwesome) {
}

if (![someObject boolValue]) {
}
```

**Не верно:**
```objc
if (someObject == nil) {
}

if (isAwesome == YES) {
}

if ([someObject boolValue] == NO) {
}
```

Синглтоны следует писать следующим образом.

**Верно:**
```objc
static APIManager *api_manager = nil;

+ (instancetype)manager {
    @synchronized(api_manager) {
        if (!api_manager) {
            api_manager = [self new];
        }
    }

    return api_manager;
}

- (id)init {
    static dispatch_once_t onceTokenAPIManager;
    dispatch_once(&onceTokenAPIManager, ^{
        api_manager = [super init];
        if (api_manager) {
            //custom initialization
        }
    });
    
    return api_manager;
}
```
