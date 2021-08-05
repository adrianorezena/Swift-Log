# Swift-Log
This is a helper class, to help organize logs in the XCode console.
You can drag this class into your project and start using it. Is easy!
You can add your own LogEvent's and activate logs as you need.


You can simple call:
```swift
Log.e("This is a warning log!")
Log.i("This is an information log!")
Log.d("This is a debug log!")
Log.v("This is a verbose log!")
Log.w("This is a warning log!")
Log.api("This is an api log!")
Log.event(.d, "This is an event log!")
```

And you get a very cool log in your console, to fast track your bugs or help in analisys.
```swift
2021-08-05 07:33:48914 [‼️][ViewController.swift]:27 viewDidLoad() | This is a warning log!
2021-08-05 07:33:48957 [ℹ️][ViewController.swift]:28 viewDidLoad() | This is an information log!
2021-08-05 07:33:48957 [💬][ViewController.swift]:29 viewDidLoad() | This is a debug log!
2021-08-05 07:33:48957 [🔬][ViewController.swift]:30 viewDidLoad() | This is a verbose log!
2021-08-05 07:33:48958 [⚠️][ViewController.swift]:31 viewDidLoad() | This is a warning log!
2021-08-05 07:33:48958 [🌍][ViewController.swift]:32 viewDidLoad() | This is an api log!
2021-08-05 07:33:48958 [💬][ViewController.swift]:33 viewDidLoad() | This is an event log!
```


## New events
You can customize your events adding new items to the LogEvent enum.

```swift
enum LogEvent: String {
    case e = "[‼️]"
    case i = "[ℹ️]"
    case d = "[💬]"
    case v = "[🔬]"
    case w = "[⚠️]"
    case api = "[🌍]"
    case myNewAwesomeEvent = "[❤️]" // <-- New event
}
```

And then call it like this:
```swift
Log.event(.myNewAwesomeEvent, "This is my own Log event!")
```

Having this on the console:
```swift
2021-08-05 07:52:22834 [❤️][ViewController.swift]:34 viewDidLoad() | This is my own Log event!
```


## Custom Log

I don't like to keep passing the event, can I customize my log?
Of course you can!

Just add a new func class like the others:
```swift
class func myNewAwesomeEvent(_ object: @autoclosure () -> Any?,
    filename: String = #file,
    line: Int = #line,
    funcName: String = #function) {

    #if DEBUG
    print(event: .myNewAwesomeEvent, "[\(sourceFileName(filePath: filename))]:\(line) \(funcName) | \(object() ?? "")")
    #endif
}
```

And calling it:
```swift
Log.myNewAwesomeEvent("OMG, it's working!")
``` 

## Activating logs
If you also hate when your console is full of unnecessary "print" call's, you can enable/disable logs as you need.
Just look for the activeLogs property and change it as needed.

```swift
private static let activeLogs: [LogEvent] = [
    .e
    //,.i   <-- you can comment or remove logs you don't want to see
    ,.d
    ,.v
    ,.w
    ,.api
    ,.myNewAwesomeEvent // <-- Don't forget to add your custom log events here
]
```
