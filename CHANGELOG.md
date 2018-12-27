# Changelog

## 1.0.0

Arbitrarily bump version to 1.0.0. API is stable and it doesn't make sense to have it in production and still be on the `0.X` versioning scheme.

- Upgrade to Swift 4.2
- Upgrade to Alamofire 4.7
- Upgrade to SwiftyJSON 4.2
- Upgrade to RealmSwift 3.13

## 0.14.0

- Upgrade to Swift 4.0
- Upgrade to RealmSwift 3.0.1
- Upgrade to Alamofire 4.5
- Don't log headers by default since it might contain sensitive information

## 0.13.0

Breaking changes:

- Change Rails-style callback methods to include the response `ApiModelResponse` instance in the callback parameters. This affects:
  - Api.find
  - Api.findArray
  - Api.update
  - Api.create

This makes it possible to get the error messages from the request, but also lets the caller know more about the request.

For example, with the new parameters:

### New way

```swift
Api<Post>.find { post, response in
  if let post = post {
    print("Got post \(post.title)")
  } else if let errors = response.errorMessages {
    print("got errors: \(errors.join("\n"))")
  }
}
```

### Old way

```swift
Api<Post>.find { post in
  if let post = post {
    print("Got post \(post.title)")
  } else {
    print("error?")
  }
}
```

## 0.12.0

Breaking changes:

- Update to Realm 1.0.0 🎈🎈🎈

## 0.11.0

Breaking changes:

- Changed the interface for `Transform`. The `perform`-method now includes a second parameter:

```swift
func perform(value: AnyObject?, realm: Realm?) -> AnyObject?
```

This will be the Realm object that will be associated with any newly created objects. For example in `ModelTransform` or `ArrayTransform`.

Dependency upgrade:

- This release bumps Realm to version `0.98.4`, which should not break your app installs.

## 0.10.2

- Fixes #22. Code for `rootNamespace` had been broken since a bad rebase. Included tests to verify fix.

## 0.10.1

- Update to `RealmSwift 0.96.3`

## 0.10.0
Breaking changes:

- Rename `API` to `ApiManager`
- Rename `api()` to `apiManager()`
- Rename `ApiForm` to `Api`
- Rename `ApiFormResponse` to `ApiModelResponse`
- Rename `ApiConfiguration` to `ApiConfig`
- Upgrade `RealmSwift` to `0.96` which might be breaking for your app. [Please read the Realm blog post for more details](https://realm.io/news/realm-objc-swift-0.96.0-beta/)
- Upgrade `Alamofire` to `3.0.0` which might require upgrades of your app.

## 0.9.0

(This version was never released to cocoapods.org)

- Implement file uploads. Please se `README.md` for more details.

## 0.8.3
- Fix crash caused by SwiftyJSON when running on device

## 0.8.2
- Fix for when server responds with an unparseable response and with a non-200 status code

## 0.8.1
- When checking for array responses also check if root is an array

## 0.8.0
- Introduce `ApiConfiguration.rootNamespace` for namespaced responses

Behind the scenes:
- Write initial tests for root namespace related methods

## 0.7.0
- Upgrade RealmSwift to 0.94.0
- Add `encoding` to `ApiConfiguration` and make `.URL` default encoding

## 0.6.0
- Add `responseData` and `rawResponse` to `ApiFormResponse`
- Introduce concept of parameter encoding (URL encoding, JSON encoding, etc)
- Upgrade Alamofire to 1.3

## 0.5.3
Fixed:
- Treat nil values as false in `BoolTransform`

## 0.5.2
Fixed:
- If a request path contains a full URL do not prefix with configurated host

## 0.5.1
- Also recognize error responses when error messages are an array

## 0.5.0
Breaking changes:
- Rename ApiResource to ApiRoutes
- Rename entire project to ApiModel instead of APIModel
- Remove legacy ApiForm.load method in favor of ApiForm.find
- Rename ApiForm.post to ApiForm.create, and create a corresponding ApiForm.update

Fixed:
- Create concept of response parsers, with JSONParser as default parser.
- Add basic request logging that is enabled by default
- Create ApiForm.get/post/put/delete methods for more intuitive REST calling
- Add a destroy method on ApiForm with parameters
- Refactor ApiForm internally for more code reuse
- Making it possible to set the path and namespace for .findArray
- Create an ApiFormResponse that is returned by most methods of ApiForm. It contains the parsed objects and other metadata about the request and response
- Correctly deal with pluralized namespaces on save

## 0.4.0
- Change `ToArray(realmArray: myArray).get()` to `toArray(myArray)`

## 0.3.0

- Upgrade to `Realm 0.92`, meaning using `import RealmSwift`
- Create `.xcodeproj` to compile standalone `.framework`
- Add method to retrieve an API url for an object. `Object#apiUrlForResource`
- Fix a crash when `primaryKey` wasn't implemented

## 0.2.0

- More stuff

## 0.1.0

- Got it working
