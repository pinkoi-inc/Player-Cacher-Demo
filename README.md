# Player-Cacher-Demo

A lightweight implementation of the AVAssetResourceLoaderDelegate protocol that enables AVPlayerItem to support caching streaming files.

> Please note that while this project serves as a demonstration of AVFoundation AVAssetResourceLoaderDelegate and the use of Combine to manage data flow, the code may not be written to the highest standard of cleanliness. If you have any suggestions for improving the code, please feel free to create an issue or pull request on the repository.

- [Technical Detail - AVPlayer 實踐本地 Cache 功能大全](https://medium.com/zrealm-ios-dev/avplayer-%E5%AF%A6%E8%B8%90%E6%9C%AC%E5%9C%B0-cache-%E5%8A%9F%E8%83%BD%E5%A4%A7%E5%85%A8-6ce488898003)


## Installation

### Swift Package Manager

- File > Swift Packages > Add Package Dependency
- Add `https://github.com/pinkoi-inc/Player-Cacher-Demo.git`
- Select "Up to Next Major" with "1.0.0"

or 

```swift
...
dependencies: [
  .package(url: "https://github.com/pinkoi-inc/Player-Cacher-Demo.git", from: "1.0.0"),
]
...
.target(
    ...
    dependencies: [
        .productItem(name: "PlayerCacher", package: "Player-Cacher-Demo"),
    ],
    ...
)
```

## Usage
```swift
import PlayerCacher
let cacher: Cacher = // your implementation of Local Cache policy (Cacher Protocol), ref: PINCacher.md
let logger = DefaultPlayerCacherLogger() // could use default
let factory = CacheableAVURLAssetFactory(cacher: cacher, logger: logger).makeCacheableAVURLAssetIfSupported(url: url)

let playerItem = AVPlayerItem(asset: asset) // than playerItem will support caching
```

## Things to know
- Due to limitations in the Apple iOS system, currently unsupported video formats such as HLS file format(.ts) are not supported.
