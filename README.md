# ios-style-guide
iOS Style Guide

Вызываем функции через точку, если они возвращают значение. Вызываем функцию в скобках, если нет возвращаемого значения.

**Надо так:**
```objc
array.count;
[UIApplication sharedApplication].delegate;
```

**Не так:**
```objc
[array count];
UIApplication.sharedApplication.delegate;
```

Скобки всегда египедские.

**Надо так:**
```objc
- (void)describeCodingStyleWithCodingStyle:(MCSCodingStyle)style {
    if (MCSCodingStyleKAndR == style) {
        [self doSomething];
    }
}
```

Всегда присваеваем значения переменной сразу после объявления.

**Надо так:**
```objc
NSObject *object = nil;
NSArray *array = [NSArray array];
```

**Не так:**
```objc
NSObject *object;
// some actions
```

Не надо лишних пробелов и не надо не ставить пробелов вовсе!

**Надо так:**
```objc
- (BOOL)tableView:(UITableView *)tableView canMoveRowAtIndexPath:(NSIndexPath *)indexPath;
```
**Не так:**
```objc
- (BOOL) tableView: (UITableView *) tableView canMoveRowAtIndexPath: (NSIndexPath *) indexPath;
-(BOOL)tableView:(UITableView*)tableView canMoveRowAtIndexPath:(NSIndexPath*)indexPath;
```

Объявление переменных должно выглядеть так.

**Надо так:**
```objc
NSArray *array = ...
```
**Не так:**
```objc
NSArray* array = ...
NSArray * array = ...
```

Предпочитай использовать свойства. Инкапсулируй переменные, которые не должны быть видны вне класса, в интерфейсе в .m файле.

**Надо так:**
```objc
@interface MCSObject: NSObject

@property (nonatomic, strong, readonly) NSManagedObjectContext *managedObjectContext;
@property (nonatomic, weak) IBOutlet UILabel *detailDescriptionLabel;
@property (nonatomic) BOOL selected;

@end
```
**Не так:**
```objc
@interface CustomObject : NSObject {
    NSString *title;
}
```

Называй переменные так, чтобы можно было легко понять для чего они нужны и объектами какого класса являются.

**Надо так:**
```objc
UIButton *magicButton;
```
**Не так:**
```objc
UIButton *mag;
```

Используй константы вместо дефайнов.

**Надо так:**
```objc
// MCSCompany.h
extern NSString * const MCSCompanyTagline;

// MCSCompany.m
NSString * const MCSCompanyTagline = @"We make award-winning apps for Apple devices.";

static NSString * const kOfficeLocation = @"Warsaw, Poland";
```
**Не так:**
```objc
#define CompanyTagline @"We make award-winning apps for Apple devices."
#define maxNumberOfRows 2
```

Не синтезируй переменные сам. Компилятор делает это за тебя. Не пиши @synthesize

Не используй переменные класса напрямую (с нижним подчеркиванием). Всегда используй свойства. Переменные напрямую используются только в методах доступа.

**Надо так:**
```objc
self.someProperty = ...
```
**Не так:**
```objc
_someProperty = ...
```

Комментируй сложные участки кода. В идеале все функции в .h файле должны быть задокументированы при помощи специальных комментариев поддерживаемых Xcode'ом.

Используй синтаксический сахар

**Надо так:**
```objc
NSArray *names = @[@"Agata", @"Ania", @"Bartek", @"Daniel", @"Dawid", @"Dominik", @"Jarek",
                   @"Karol", @"Klaudia", @"Maciej", @"Maciej", @"Marcin", @"Rafał", @"Wojtek",
                   @"Wojtek", @"Zbigniew", @"Janek"];
NSDictionary *animals = @{@"dogs" : @[@"Boomer"]};
NSNumber *officeIndoorSwimmingPool = @YES;
NSNumber *over9000 = @9001;
```

Используй правильные перечисления.

**Надо так:**
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

Булевские выражения.

**Надо так:**
```objc
if (!someObject) {
}

if (isAwesome) {
}

if (![someObject boolValue]) {
}
```

**Не так:**
```objc
if (someObject == nil) {
}

if (isAwesome == YES) {
}

if ([someObject boolValue] == NO) {
}
```

Синглтоны.

**Надо так:**
```objc
+ (instancetype)sharedInstance {
    static id sharedInstance = nil;

    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        sharedInstance = [[self alloc] init];
    });

    return sharedInstance;
}
```
