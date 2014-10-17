**Dispatcher** takes the pain out of [Grand Central Dispatch](https://developer.apple.com/library/mac/documentation/performance/reference/gcd_libdispatch_ref/Reference/reference.html) (at least some parts of it).

```Swift
gcd.async {
	
	// do something that takes time...

	gcd.main.sync {

		// update the user interface...
	}
}
```

### What is a `DispatchQueue`?

A `DispatchQueue` can execute closures in order (a.k.a. serially) or out of order (a.k.a. concurrently).

Use `async()` and `sync()` to add closures to a `DispatchQueue`.

* `async()` returns **before** the closure you pass it is done executing.

* `sync()` returns **after** the closure you pass it is done executing.

-

### What `DispatchQueue`s already exist?

These 5 queues are at your disposal...

* `gcd`: The `Dispatcher` singleton. The concurrent `DispatchQueue` for default-priority tasks.

* `gcd.main`: The serial `DispatchQueue` where all your UI magic takes place.

* `gcd.high`: The concurrent `DispatchQueue` for high-priority tasks.

* `gcd.low`: The concurrent `DispatchQueue` for low-priority tasks.

* `gcd.background`: The concurrent `DispatchQueue` for no-priority tasks.

-

### What `DispatchQueue` am I currently on?

There are two ways to know which `DispatchQueue` you're currently on:

* `gcd.current`: Returns the `DispatchQueue` you're currently on.

* `gcd.isCurrent`: A boolean property available on all `DispatchQueue`s.

-

### How do I make my own `DispatchQueue`?

Simply call `gcd.serial()` to make a serial `DispatchQueue`.

And call `gcd.concurrent()` to make a concurrent `DispatchQueue`.

You **must** retain these yourself!

-

*To be continued...*

-

### Installation

**Dispatcher** is not yet available on CocoaPods.

In the meantime, drag-and-drop the `Dispatcher.xcodeproj` into your own Xcode project. In your application target's **Build Phases**, add `Dispatcher.framework` to **Target Dependencies**, **Link Binary With Libraries**, and **Copy Files**.

If that gives you trouble, open the `Dispatcher.xcodeproj` in Xcode and build the framework target. Right-click `Dispatcher.framework` in the **Products** folder in your **Project Navigator** and click **Show in Finder**. Drag-and-drop the `Dispatcher.framework` from your finder into your Xcode project.
