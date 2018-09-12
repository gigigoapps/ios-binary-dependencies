# ios-binary-dependencies
Vendor frameworks dependencies

## Available frameworks

### Facebook
* Bolts
* CoreKit
* LoginKit

Frameworks downloaded from: [Facebook SDK](https://origincache.facebook.com/developers/resources/?id=facebook-ios-sdk-current.zip)

### Twitter
* TwitterCore
* TwitterKit
* Fabric

Frameworks downloaded from: [Twitter SDK*](https://ton.twimg.com/syndication/twitterkit/ios/2.1/Twitter-Kit-iOS.zip)

*These frameworks are for version 3.1. The 2.8 version are imported manually from an old project we are using

### Vuforia
* Vuforia

Framework downloaded from: [Vuforia SDK*](https://developer.vuforia.com/downloads/sdk)

## Integrations

### Cartfile

Facebook v4.34.1
```
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/facebook/bolts/bolts.json" ~> 4.34.1
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/facebook/corekit/corekit.json" ~> 4.34.1
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/facebook/loginkit/loginkit.json" ~> 4.34.1
```

Twitter v2.8
```
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/twitter/twittercore/twittercore.json" ~> 2.8
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/twitter/twitterkit/twitterkit.json" ~> 2.8
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/twitter/Fabric/fabric.json" ~> 1.6
```

Twitter v3.1 (Fabric is not needed anymore)
```
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/twitter/twittercore/twittercore.json" ~> 3.1
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/twitter/twitterkit/twitterkit.json" ~> 3.1
```

Vuforia
```
binary "https://raw.githubusercontent.com/gigigoapps/ios-binary-dependencies/master/vuforia/vuforia.json" ~> 7.2
```

## FAQ

### Carthage cache errors

Generally, when using carthage binaries, could happen integration errors that can simply be fixed removing carthage cache:

```
$ rm -rf ~/Library/Caches/org.carthage.CarthageKit/
```

Then retry update or bootstrap

### Frameworks plist errors

When uploading a new version, is very common that the vendor doesn't set correctly the Info.plist and carthage show something like `"the DTSDKName key in its plist file is missing"`

Be sure that the Info.plist has the same keys than another working framework. Keys like `DTSDKName` or `Executable file` shouldn't be missed and `Bundle OS Type code` should be set to `FMWK`


### Zip files error

When uploading a new framework, is a common error that the zip generated contains MACOS files that hides some important files when carthage unzip the frameworks.

The error show by carthage is like `Failed to read file or folder at /private/var/blablabla/__MACOSX/theframework.framework bla bla bla`

Be sure that the zip uploaded to this repo doesn't have MACOSX folders or files.

Check the zip with

```
$ unzip -vl <FrameworkName>.framework.zip
```

If contains folders or files like `__MACOSX` remove them with

```
$ zip -d <FrameworkName>.framework.zip "__MACOSX/" "__MACOSX/*"
```
then upload the framework again
