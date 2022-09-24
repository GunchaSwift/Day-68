# Day-68
### **Bucket List project part 1**

***Adding conformance to Comparable for custom types***

```
static func <(lhs: User, rhs: User) -> Bool {
      lhs.lastName < rhs.lastName
}
```

***Reading and writing data to the documents directory***

First, we must find the app's documents directory and a good idea is to rely on Apple's API for doing that.

```
func getDocumentsDirectory() -> URL {
    // find all possible documents directories for this user
    let paths = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)

    // just send back the first one, which ought to be the only one
    return paths[0]
}
```

And then read/write can be done like this

```
let str = "Test Message"
let url = getDocumentsDirectory().appendingPathComponent("message.txt")

do {
   try str.write(to: url, atomically: true, encoding: .utf8)
   let input = try String(contentsOf: url)
   print(input)
} catch {
   print(error.localizedDescription)
}
```

***Switching View states with enums***

```
enum LoadingState {
    case loading, success, failed
}

struct LoadingView: View {
    var body: some View {
        Text("Loading...")
    }
}

struct SuccessView: View {
    var body: some View {
        Text("Success!")
    }
}

struct FailedView: View {
    var body: some View {
        Text("Failed.")
    }
}
```

All this code can then be used in ContentView.

```
if loadingState == .loading {
    LoadingView()
} else if loadingState == .success {
    SuccessView()
} else if loadingState == .failed {
    FailedView()
}
```
