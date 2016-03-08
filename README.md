
## Introduction
  StarConsoleLink add the link to your console, which allows you to click on the link area rapid positioning to the log line

![Smaller icon](https://github.com/iStarEternal/StarConsoleLink/blob/master/example_image.jpg "Title here")

## How to use

1.  Run StarConsoleLink in you Xcode

2.  If you are using Swift, Copy /StarConsoleLink/Plugin/Logger.swift in you project

3.  If you are using Objective-C, Copy below text in you PrefixHeader.pch

4.  If you want to custom you log, please follow the rules: [FileName.extension:LineNumber], Just like [main.swift:15]

### Objective-C
```
#ifdef DEBUG
#define NSLog(format, ...) NSLog(@"[INFO][%@:%d] %@", [[NSString stringWithUTF8String:__FILE__] lastPathComponent], __LINE__, [NSString stringWithFormat:(format), ##__VA_ARGS__])
#else
#define NSLog(...) while(0){}
#endif
```
### Swift
```

import Foundation 


struct LogColor {
    
    static let ESCAPE = "\u{001b}["
    static let RESET_FG = ESCAPE + "fg;" // Clear any foreground color
    static let RESET_BG = ESCAPE + "bg;" // Clear any background color
    static let RESET = ESCAPE + ";"   // Clear any foreground or background color
}

class Logger: NSObject {
    
    class func print<T>(value: T, title: String, color: String, functionName: String, fileName: String, lineNumber: Int) {
        
        Swift.print("\(LogColor.RESET_FG)fg\(color);[\(title)][\((fileName as NSString).lastPathComponent):\(lineNumber)] \(value)\(LogColor.RESET)")
    }
    
    // WEIGHT: 0
    class func debug<T>(value: T, functionName: String = __FUNCTION__, fileName: String = __FILE__, lineNumber: Int = __LINE__) {
        //        guard DEBUG != 0 else {
        //            return
        //        }
        print(value, title: "Debug", color: "0,51,153", functionName: functionName, fileName: fileName, lineNumber: lineNumber)
    }
    
    // WEIGHT: 0
    class func info<T>(value: T, functionName: String = __FUNCTION__, fileName: String = __FILE__, lineNumber: Int = __LINE__) {
        print(value, title: "Info", color: "11,11,11", functionName: functionName, fileName: fileName, lineNumber: lineNumber)
    }
    
    // WEIGHT: 2
    class func warning<T>(value: T, functionName: String = __FUNCTION__, fileName: String = __FILE__, lineNumber: Int = __LINE__) {
        print(value, title: "Warning", color: "204,255,0", functionName: functionName, fileName: fileName, lineNumber: lineNumber)
    }
    
    // WEIGHT: 4
    class func error<T>(value: T, functionName: String = __FUNCTION__, fileName: String = __FILE__, lineNumber: Int = __LINE__) {
        print(value, title: "Error", color: "204,0,51", functionName: functionName, fileName: fileName, lineNumber: lineNumber)
    }
    
    // WEIGHT: 5
    class func important<T>(value: T, functionName: String = __FUNCTION__, fileName: String = __FILE__, lineNumber: Int = __LINE__) {
        print(value, title: "Important[如果发现该行日志，应该及时处理]", color: "204,0,51", functionName: functionName, fileName: fileName, lineNumber: lineNumber)
    }
    
}

```

