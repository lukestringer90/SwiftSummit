# Swift Summit

291 days after the launch of the Swift programming language, Swift Summit was held in London, March 21st 22nd. What an amazing 2 days it was. I met some amazing people, learnt some incredibly interesting and thought provoking things, and came away highly inspired and enthusiastic about the future of iOS development.

Many thanks to Beren Rumble ([@devberen](http://www.twitter.com/devberen)) , Ida Kristiansson ([@NomadicIda](http://www.twitter.com/NomadicIda)) and Morgan Evetts ([@morqon](http://www.twitter.com/morqon)) for organising and hosting such an amazing event. 👏

Swift Summit [website link](https://www.swiftsummit.com), [twitter link](http://www.twitter.com/swiftsummit).

---

Here are the notes I took. They should not be considered definitive or 100% accurate to the content presented, they are more just a reminder of some cool and interesting things that were said. Where possible I have tried to find links to the slides or presentation material.

**Pull requests to correct inaccuracies are very welcome.**

## Functional View Controllers

By **Chris Eidhof**, [@ChrisEidhof](http://www.twitter.com/ChrisEidhof)

* View controllers have a tendency to do a lot of things.
	* Setup views.
	* Load data.
	* Show new view controllers.
	* etc...
* Use functional techniques to solve this problem.
* See the "flow" of the application:

```swift
let flow = navigationController(loginViewController()) >>> orgsScreen >>> reposScreen >>> issuesScreen
```

* No need to create view controller subclasses.
* Complete decoupling of view controllers from data and other view controllers.

GitHub repo: [chriseidhof/github-issues](https://github.com/chriseidhof/github-issues)

Shortly after Swift Summit Chris shipped [Scenery](https://www.getscenery.com/); a Mac app written entirely in Swift. He wrote his thoughts on using Swift in production [here](http://chris.eidhof.nl/posts/scenery-launch.html).

## Share Your Code, Swift API Design: Getting Results

By **Brian Gesiak**,  [@modocache](http://www.twitter.com/modocache)

[Slides](https://github.com/modocache/talks/blob/3a0feaa5db7fc6c8fef8444772b99f7a930f29a4/swiftsummit.key?raw=true)

* How do you write code other people want to use?
* How do you write *compelling code*?
* Code should be:
	1. Precise
	2. Convenient
* When you have to write documentation to explain code, users will not read it and ultimately it is not precise.
* LLamaKit ([repo](https://github.com/LlamaKit/LlamaKit)) includes `ResultType` which allows for a more precise way for error handling.
* "Railway Oriented Programming" concept facilitates handling errors that can occur at different times.
* Uses `map` and `flatMap`
	* `map` when you only have a collection of values.
	* `flatMap` when you have a collection of failable results.

Gift ([repo](https://github.com/modocache/Gift)) for interacting with the GitHub API in Swift, which uses the railway concept

Brian's [retrospective blog post](http://modocache.io/swift-summit) on Swift Summit.

## Closures In API Design

By **Hermés Piqué**, [@hpique](http://www.twitter.com/hpique)

[Slides](https://speakerdeck.com/hpique/closures-in-api-design)

* Closures are self contained blocks of functionality
* UIAlertController is block based.
* Closures encourage code locality, particularly in comparison to the delegate pattern.
* `@autoclosure` is for parameter values we may not use. Looks like it automatically wraps the parameter in a closure for use inside the function.
* `@noescape` is for parameters that will not outlive the function call.
* no-op as default parameter for closures.

## Back To The Futures

By **Javier Soto**, [@Javi](http://www.twitter.com/Javi)

[Slides](https://speakerdeck.com/javisoto/back-to-the-futures).

* Do not use NSError.
	* Too easy to just pass `nil` - I often do
	* Do you check the domain?
	* Do you check the error code?
	* Probabbly not - I often don't
* Better to create your own `ErrorType` to define the error cases which you care about.
* Introduces Futures, also known as Promises.
	* Encapsulate a deferred computation.
	* More declarative for failable asynchronous computation.
	* Errors are carried though.
	* Look really cool and useful having implemented (attempted) asynchronous operations before. Will make things *much* clearer.
* Futures are related to Reactive Cocoa.
* In fact Signals > Futures.
	* Futures only work 1 day.
	* Signals allow objects to be told about things that happen in the future as well as say what things should happen.
* Reactive Cocoa 3 is in alpha and uses Swift.

Playground demo [link](https://github.com/JaviSoto/Talks/tree/master/SwiftSummit2015).

## The Monad Among Us

By **Al Skipp**, [@ChromophoreApp](http://www.twitter.com/ChromophoreApp)

[GitHub repo](https://github.com/alskipp/Swift-Adventures-In-Monad-Land)

* Code without `nil` is saner code
* Optionals are simple values, but they do add complexity

## Static Types and Zero-Cost Abstractions

By **Airspeed Velocity**, [@AirSpeedSwift](http://www.twitter.com/AirSpeedSwift)

* Structs pay no runtime penalties like classes do.
* Don't unintentionally rewrite the standard library functions.
* For example, `sort` is very efficient. Use it to sort your own data types rather than writing your own (less efficient) implementation.

## How Swift is Swift?

By **Joseph Lord**, [@jl_hfl](http://www.twitter.com/jl_hfl)

[Slides](http://blog.human-friendly.com/how-swift-is-swift)

* Swift is designed for speed.
* Use `final` for classes.
* Use constants with `let`
* `ContiguousArray` is more performant for arrays of `NSObject` 
* For performance avoid
	* global / class / static vars
	* Function calls that cannot be inlined.
	* `@objc` objects
	
## What Haskell Taught Me About Writing Swift

By **Abizer Nasir**, [@abizern](http://www.twitter.com/abizern)

[Slides](https://speakerdeck.com/abizern/what-haskell-taught-me-about-writing-swift)

* Favour structs over classes as much as possible.
* Do not mutate structs.
	* Use [lensing](http://chris.eidhof.nl/posts/lenses-in-swift.html) approach.
* `typealias` is useful for making code cleaner.
	* Higher order functions are easier to read.

Recommended books:
	
* [Learn You A Haskel For Great Good](http://learnyouahaskell.com) Book 
* [Real World Haskell](http://book.realworldhaskell.org) Book
* [Functional Programming In Swift](http://www.objc.io/books/)

## Swift Scripting

By **Ayaka Nonaka**, [@ayanonagon](http://www.twitter.com/ayanonagon)

[Slides](https://speakerdeck.com/ayanonagon/swift-scripting), [Git Repo](https://github.com/ayanonagon/talks/tree/master/swiftsummit)

* Design assets difficult to keep track of.
* Use a cocoapod for images and other assets designers create that are used in apps.
* Designers make a pull request on the cocoapod repo.
* UIImage category is automatically created to make each asset available in code.
	* Not sure how this works when using `.xcassets`?
		* [@indragie](https://twitter.com/indragie)’s [swiftsrc](https://github.com/indragiek/swiftrsrc) (also written in Swift!) looks like a great option to achieve the same result if you are using `.xcassets`.
* Category creation is done with a script... in Swift!
* Writing Swift scripts is a good way to learn Swift before writing it for production software.
* Get access to all the frameworks in iOS within your script.
* [Carthage](https://github.com/Carthage/Carthage) is a dependency manager that builds a framework to integrate with your code. Works well with Swift scripts that live outside an Xcode project.
* [cocoapods-rome](https://github.com/neonichu/Rome) works in a similar way by building a framework.
	* Carthage vs Rome. Get it?
	
## JSON, Swift and Type Safety: It’s a wrap

By **Anthony Levings**, [@SketchyTech](http://www.twitter.com/SketchyTech)

[Slides](http://www.slideshare.net/AnthonyLevings/json-swift-and-type-safety-its-a-wrap)

* A number of approaches to dealing with JSON parsing in swift.
* Enum type wrapping approach uses associated values.
* Used in.
	* [Argo](https://github.com/thoughtbot/Argo).
	* [Swiftz](https://github.com/typelift/swiftz)
	* [json-swift](https://github.com/owensd/json-swift).
* Also [Iolcos](https://github.com/sketchytech/Iolcos) and [Aldwych	](https://github.com/sketchytech/Aldwych_JSON_Swift), which uses principles outlined in the talk.
	
Wonderful use of a drama-school-esque prop. Good work!

## Death By Indecision

By **Alexsander Akers**, [@a2](http://www.twitter.com/a2)

[Slides](http://www.slideshare.net/pandamonia/death-by-indecision)

* Emoji-Driven-Presentation 📈😃👍
* Everyone has a side project.
	* Weird when you think about it really.
	* Consider a farmer: After a hard day of harvesting crops, do they go home and work on their crop harvesting side project?
* Parkinson's law states "work expands so as to fill the time available for its completion".
	* Something will take as much time as you set your self, not less.
	* Set (stricter) deadlines to stop this.
* Work with other people to ship something.
* Commit to talking.
* Open source while the code is still embarrassing so you *have* to fix it. Keeping it private gets you off the hook.

If you have a OSS Swift app contact Beren Rumble ([@devberen](http://www.twitter.com/devberen)) and he can help promote and share it.

## Extracurricular Swift

By **Sally Shepard & Mark Martin**, [@mostgood](http://www.twitter.com/mostgood) & [@urban_teacher](http://www.twitter.com/urban_teacher)

[Slides](http://www.slideshare.net/mostgood/extracurricular-swift)

* Swift can *totally* be used in education for teaching programming
* The language itself is great, but the tooling is not there yet.

Links:

* [http://www.runswiftlang.com](http://www.runswiftlang.com) to run Swift in the browser.
* [https://www.codeclub.org.uk](https://www.codeclub.org.uk)
* [http://www.stemnet.org.uk](http://www.stemnet.org.uk)

## (Functional) Programming For Everyone

By **Daniel Steinberg**, [@dimsumthinking](http://www.twitter.com/dimsumthinking)

[GitHub repo](https://github.com/dimsumthinking/TurtlePlayground): Swift playground using Logo-like commands to teach kids programming.

* Playgrounds with swift can be used for teaching children to code.
* Realtime inline feedback!
* Playgrounds now get their own directory structure much like an Xcode project.
	* Allows you to provide helper code.
	* And a place where children can put their own implementations.

* Interesting question: **Should we teach kids functional programming from the start rather than procedural programming?**
* Interesting answer from Daniel: (paraphrasing)**In the same way I don't want kids to be drinking alcohol, I'm not sure how much functional programming they should be doing either!**

## Day 1 Panel Discussion

Panel: [Brian Gesiak](http://www.twitter.com/modocache), [Ayaka Nonaka](http://www.twitter.com/ayanonagon), [Chirs Eidhof](http://www.twitter.com/ChrisEidhof) & [Airspeed Velocity](http://www.twitter.com/AirSpeedSwift)

* Swift can be a backend language, but it is the infrastructure that is missing, like Heroku and AWS.
* Exciting to see the development of a new language that is less than a year old! 
* Apple changing the language based on our feedback.
* We can decide it's destiny.
* We can decide the best practises.
* An amazing opportunity.

The big question: **Is Swift ready for production?**

Fantastic answer from Ayaka: **Do you think Objective-C is ready for production?**

## let swift: Race?

By **Jack Nutting**, [@jacknutting](http://www.twitter.com/jacknutting)

[Slides](http://assets.nuthole.com/swiftsummit2015_jacknutting.pdf)

* Starts off with a [translation of a Bible quote into Swift](https://twitter.com/jacknutting/status/580284786339647488/photo/1).
* He has not written any Objective-C since November.
* Advice is not not just use Swift for the sake of it - be pragmatic.
* After all Objective-C is not a bad thing.
* Nested method calls like `[[[object foo] bar] baz]` isn't just bad syntax, it is bad form. 
* When using Swift, don't just use enums where subclassing would be better for customisability.
	* Inheritance and polymorphism are good things, use them!
	* Subclassing and comparability are sometimes better than using enums.
* If a huge chunk of code revolves around switching on an enum, maybe using classes would be better.
* Using `final` limits customisation through subclassing. 
* However, future developers will want the flexibility to extend your system in ways you cannot foresee. A compromise is therefore necessary,
* "Premature optimisation is the root of all evil".
* Remember functional programming is not a silver bullet.
* Use the [lensing](http://chris.eidhof.nl/posts/lenses-in-swift.html) approach to avoid mutability.


## Swift, Meet Objective-C

By **Daniel Tomlinson**, [@dantoml](http://www.twitter.com/dantoml)

[Slides](https://speakerdeck.com/danieltomlinson/swift-meet-objective-c)

* "All Objective-C you write now is technical debt". *Controversial* 😮
* Swift is the future, we need to look to it.
	* Try building new APIs in Swift.
	* Experiment when building new features.
* Remember, you can use Objective-C and Swift together. 👫
* Bridging exposes Objective-C headers to Swift.
* Previously when using Objective-C APIs in Swift there was a mess of implicitly unwrapped values. Additions in Obj-C to help this:
	* `__nullable`
	* `__nonull`
	* `__null_resetable` for properties
	* `__null_unspecified` is the default
* What you **do** get when using Swift code in Objective-C (limited to the runtime):
	* Classes, but not generics or subclassing.
	* Protocols
	* Methods
		* No generic methods
		* No default methods
	* Properties
		* No KVO
		* Cannot be swizzled, except when using the `dynamic` keyword
	* Enum, which is converted to NSEnum
		* No associated values
* What you **don't** get:
	* Structs
	* Functions
	* Operators
	* Generics
* WWDC 2014 videos 406 & 407 go through a lot.
* Advice: create your API in Objective-C and then bridge to Swift. Pick which one you want.
* Remember to include what namespace you want when using `@Objc`, other wise you will lose it.

## Swift Funtime

By **Boris Bügling**, [@NeoNacho](http://www.twitter.com/NeoNacho)

[Slides](https://speakerdeck.com/neonichu/swift-funtime-2) & [Github Repo](https://github.com/neonichu/swift-funtime)

* Boris is on the core team at cocoapods.
* In Swift import `ObjectiveC.runtime`
* You can use dynamic introspection for Swift objects.
* The `reflect` method is in the standard library, but it is private so be careful.
* `NSInvocation` does not exist in Swift.

## Testing In Swift

By **Jan Riehn**, [@jriehn](http://www.twitter.com/jriehn)

[Slides](https://speakerdeck.com/jriehn/testing-in-swift-swiftsummit-2015) & [GitHub Repo](https://github.com/jriehn/testing-in-swift)

* Testing is an art.
	* Creative.
	* Challenging.
* Swift offers some reflection, but it is private, so don't use it.
	* Cannot set variables through reflection so don't use it.
* Learn to create your own test doubles rather than relying on mocking.
	* This is easier and nicer in Swift as you can do it inline.
* You can use OCMock in Swift with some setup.
	* But restricts you writing your tests in Objective-C 😞
* Create different test classes.
	* One for the success cases.
	* One for the failure cases.
* Separate your UI from the business logic.
	* Create thin view controllers.
* From Swift 1.2 onwards no need to add your production test code to the test target.
* OCHamcrest has nice syntax for optionals.

## Debugging In Swift

By **Carola Nitz**, [@_Caro_N](http://www.twitter.com/_Caro_N)

[Slides](https://speakerdeck.com/carola/debugging-in-swift)

* Swift can be hard to debug.
	* Output from lldb it not helpful.
	* Error messages make no sense.
* In lldb, `po` is just an alias for `expression -O -- myObject`
* For nicer output use `expression -l objc -O -- (id) <memoryAddress>`
* Utilise conditional breakpoints. e.g. play a sound for feedback.
* Use exception breakpoint.
* Use symbolic breakpoints.
	* Stop when a method is called.
	* Can also stop on private methods.
* Tips for dealing with compilation errors:
	* Remove variables.
	* Split up instructions.
* You can use launch arguments passed at the start to override defaults.
* In the scheme editor:
	* Add concurrency arguments for Core Data to check for thread safety.
	* `SQLDebug`
	* `NSDoubleLocalizedStrings 1`
	* `NSShowNonLocalisedStrings 1`
	* `AppleLanguages (es de)`
* Use can use the Swift repl from inside lldb.
	* run `xcrun swift` to clean the repl session.
* You can use activity tracing with breadcrumbs.
	* Included in the crash report,
	* However cannot log strings for user privacy.
	* More info in objc.io

## Swifty Methods

By **Radek Pietruszewski**, [@radexp](http://www.twitter.com/radexp)

[Slides](http://www.slideshare.net/radexp/swifty-methods-swifty-apis) & [related blogpost](http://radex.io/swift/methods)

* Focus on clarity
* Don't write clever code. "Keep it simple, stupid".
* Clarity ≠ Verbosity.
	* Find the sweetspot between brevity and verbosity.
	* This is where clarity lies.
* Remove the noise.
	* Good example of this is the `replace` string method, and a rewrite of [NSTimer](www.radex.io/swift/nstimer).
* Have an open mind when writing Swift.
* Programs must be read as well as executed.
* Use default arguments for methods that usually take arguments.

## Crypto Swift

By **Marcin Krzyżanowski**, [@krzyzanowskim](http://www.twitter.com/krzyzanowskim)

[GitHub Repo](https://github.com/krzyzanowskim/CryptoSwift)

* Common Crypto framework available in Swift.
* SwiftSSL is a Swift wrapper around CommonCrypto.
* NaCL (Salt).
* Crypto Swift is pure Swift framework, but is slower. Supports:
	* Hashing
	* Symmetric Ciphers
	* Block Cipher
	* AES
	* ChaCha20 
	* Authenticators
	
## Swift & Metal

By **Simon Gladman**, [@FlexMonkey](http://www.twitter.com/FlexMonkey)

[Slides](https://speakerdeck.com/flexmonkey/ios-gpu-programming-with-swift-and-metal) & [related blogpost](http://flexmonkey.blogspot.co.uk/2015/03/swift-metal-four-million-particles-on.html)

* Metal is faster then SceneKit as it is lower level.
* But there is more of a development overhead.
* Has C++ style syntax.

## Taylor Swift HTTP Framework

By **Jorge Izquierdo**, [@izqui9](http://www.twitter.com/izqui9)

[GitHub repo](https://github.com/izqui/taylor)

* Taylor is an HTTP server written in Swift.
* Can use Taylor in Playgrounds.
* Can embed it in your app for workarounds with WKWebView.

## View From The Otherside

By **Gem Barrett**, [@gembarrett](http://www.twitter.com/gembarrett)

* Stereotype of Apple developers from web developers:
	* Don't touch this.
	* Unstable.
	* Secrecy, lack of open source.
* Web / Native / Hybrid argument

## RESTful

By **Kyle Fuller**, [@kylefuller](http://www.twitter.com/kylefuller)

[Slides](https://speakerdeck.com/kylef/embracing-change-with-rest)
[Representor](https://github.com/the-hypermedia-project/representor-swift) - Hypermedia resource framework in Swift

* Kyle is the tech lead at CocoaPods
* REST is for good API design
* Lets us embrace change
* You should anticipate change. 
* Facebook freeze their API for 2 years to ensure compatibility.
* REST promotes change.
* Take on Mark Zuckerberg quote: "Move fast and *dont* break things."
* REST let's us embrace change, so we can move fast and break nothing.
* REST is not about exposing a database.
* Design your API around representations, i.e. states.
* This avoids coupling implementation details, which can change.
* HATEOAS is a REST constraint. If you are not using HATEOAS you are not doing REST.
* API can be dynamic in what things it can do.
* Client is taught about the semantics so it can discover things for itself.
* Gracefully handle features that the API lacks / turns off.
* Use the SIREN JSON format for hypermedia.

[Representor](https://github.com/the-hypermedia-project/representor-swift): Swift library for building and consuming Hypermedia messages 

A collection of REST (HATEOAS) APIs:

- [Polls API](https://github.com/apiaryio/polls-api) - Siren and HAL, completely OSS and configurable.
- [PayPal API](https://developer.paypal.com/docs/api/#hateoas-links) - HAL
- [Heroku](https://blog.heroku.com/archives/2014/1/8/json_schema_for_heroku_platform_api) - JSON Schema
- [GitHub](https://api.github.com) - Custom (url in responses)
- [Artsy](http://artsy.github.io/blog/2014/09/12/designing-the-public-artsy-api/) - HAL
- [FizzBuzz as a Service](http://smizell.com/weblog/2014/solving-fizzbuzz-with-hypermedia) - Siren

## Day 2 Panel Discussion & Closing Remarks

* Exploring new concepts in Swift we didn't have in Objective-C.
* You could use 👍 and 👎 emoji to indicate success and failure.
* We still need dynamic features in Swift as we have to use Objective-C for them still.
* Swift tooling needs improving.
* We can decide and make the best practises ourselves - golden opportunity.
* Be pragmatic about using Swift and Objective-C.
* Core Data is ripe for Swift rework. *Hell Yes*
* Maybe Apple would open source Swift? Only a question of when?
* Open sourcing would lead to Swift web frameworks as it would be available on every platform. 
