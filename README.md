# ios-style-guide
Objective-C Style Guide

* [Оформление](#Оформление)
    * [Пробелы](#Пробелы)
    * [Скобки](#Скобки)
    * [Объявление функций](#Объявление-функций)
    * [Вызов функций](#Вызов-функций)
    * [Классы](#Классы)
    * [Объявление переменных](#Объявление-переменных)
    * [Литералы](#Литералы)
    * [Порядок функций в классе](#Порядок-функций-в-классе)
* [Документация](#Документация)
* [Свойства объекта](#Свойства-объекта)
* [Синглтоны](#Синглтоны)
* [Константы](#Константы)
* [Перечисления](#Перечисления)
* [Булевские выражения](#Булевские-выражения)

## Оформление

### Пробелы

Не следует ставить лишних пробелов. Нужно всегда использовать одинарный пробел. (Если есть сомнения, то можно проверить себя выделив кусок кода, затем нажав правую клавишу, затем Structure -> Re-Indent)

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

### Скобки

Скобки нужно ставить в стиле K&R (на програмистском жаргоне "египетские").

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

### Объявление функций

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

### Вызов функций

Нужно вызывать функции заключая их в скобки, а свойства вызывать через точку.

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

### Классы

Каждый класс следует писать в отдельном файле. Следует называть классы таким образом, чтобы было понятно их назначение. Можно использовать в названии класса название класса, от которого он был унаследован.

**Верно:**
```objc
@interface MyAwesomeButton : UIButton
```

### Объявление переменных

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

При объявлении переменных не следует ставить лишних пробелов. Следует называть переменные таким образом, чтобы было понятно их назначение.  Иногда для понятности можно в имени переменной использовать название класса. 

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

### Литералы

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

### Порядок функций в классе

Следует группировать функции по смыслом нагрузке. Свойства класса всегда следует писать наверху. Следует выделять такие группы при помощи макроса ```#pragma mark -```.

**Верно:**
```objc
#pragma mark - Some functions
``` 

## Документация

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

## Свойства объекта

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

## Синглтоны

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

## Константы

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

## Перечисления

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

## Булевские выражения

Не следует перегружать булевские выражения в условиях.

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
