
IOSVideoBackground is an easy to use Swift framework that provides the ability to play a video on any UIView. This provides a beautiful UI for login screens, or splash pages

## Features

- [x] Play a video with one line of code
- [x] Supports local videos `&&` videos from a web URL
- [x] Automatically adjusts when device orientation changes
- [x] Automatically resumes video when app re-enters foreground
- [x] Pause, resume, restart, and other controls
- [x] Loop videos *(optional)*
- [x] Mute sound *(optional)*
- [x] Darken videos so overlying UI stands out more *(optional)*

## Contents

1. [Requirements](#requirements)
2. [Integration](#integration)
    - [CocoaPods](#cocoapods)
    - [Carthage](#carthage)
    - [Manually](#manually)
3. [Migration Guide](#migration-guide)
4. [Usage](#usage)
    - [Example](#example)
    - [Customization](#customization)
    - [Controls](#controls)
    - [Singleton](#singleton)
    - [Adding Videos To Your Project](#adding-videos-to-your-project)
5. [Issues](#issues)
6. [License](#license)
7. [Authors](#authors)

## Requirements

- Swift 3+
- iOS 8+

## Integration

#### CocoaPods
You can use [CocoaPods](https://cocoapods.org/) to install `SwiftVideoBackground` by adding it to your `Podfile`:

For Swift 4:
```ruby
pod 'SwiftVideoBackground', '~> 3.0'
```

For Swift 3:
```ruby
pod 'SwiftVideoBackground', '0.06'
```

#### Carthage
You can use [Carthage](https://github.com/Carthage/Carthage) to install `SwiftVideoBackground` by adding it to your `Cartfile`:


#### Manually

To use this library in your project manually you may:  

1. for Projects, just drag VideoBackground.swift to the project tree
2. for Workspaces, include the whole SwiftVideoBackground.xcodeproj


#### Version 2.0.0
See the quick [migration guide](migration-2.0.0.md).

## Usage

#### Example

``` swift
import UIKit
import SwiftVideoBackground

class MyViewController: UIViewController {
  override func viewDidLoad() {
    super.viewDidLoad()

    try? VideoBackground.shared.play(view: view, videoName: "myVideo", videoType: "mp4")

    /* or from URL */

    let url = URL(string: "https://coolVids.com/coolVid.mp4")!
    VideoBackground.shared.play(view: view, url: url)
  }
}
```

> Documentation for Version 0.06 (Swift 3) can be found [here](README-0.06.md).

#### Customization

`play()` has four additional optional parameters for customization:
- `darkness`: CGFloat - Value between `0` and `1`. The higher the value, the darker the video. Defaults to `0`.
- `isMuted`: Bool - Indicates whether video is muted. Defaults to `true`.
- `willLoopVideo`: Bool - Indicates whether video should restart when finished. Defaults to `true`.
- `setAudioSessionAmbient`: Bool - Indicates whether to set the shared `AVAudioSession` to ambient. If this is not done, audio played from your app will pause other audio playing on the device. Defaults to `true`.

So for example:

``` swift
VideoBackground.shared.play(
    view: view,
    videoName: "myVideo",
    videoType: "mp4",
    darkness: 0.25,
    isMuted: false,
    willLoopVideo: true,
    setAudioSessionAmbient: true
)
```

-> will play the video with the sound on, slightly darkened, continuously looping, and without affecting other sources of audio on the device.

> Any combination of the parameters can be included or left out.

> `setAudioSessionAmbient` only has an effect in iOS 10.0+. For more information, see the [docs](https://developer.apple.com/library/content/documentation/Audio/Conceptual/AudioSessionProgrammingGuide/AudioSessionBasics/AudioSessionBasics.html).

#### Controls

- `pause()` - Pauses the video.
- `resume()` - Resumes the video.
- `restart()` - Restarts the video.
- `darkness` - Change this `CGFloat` to adjust the darkness of the video. Value `0` to `1`. Higher numbers are darker. Setting to an invalid value does nothing.
- `isMuted` - Change this `Bool` to mute/unmute the video.
- `willLoopVideo` - Change this `Bool` to set whether the video restarts when it ends.
- `playerLayer` - The `AVPlayerLayer` that can be accessed for advanced control and customization of the video.

#### Singleton

`SwiftVideoBackground` includes a singleton instance that can be conveniently accessed with `VideoBackground.shared`. An instance of `VideoBackground` can only play one video on one `UIView` at a time. So if you need to play on multiple `UIView`s, you need to retain an instance of `VideoBackground` for each `UIView`:

```swift
let videoBackground1 = VideoBackground()
```

#### Adding Videos To Your Project

In order to play local videos, you must add them to your project:
1. Open project navigator
2. Select your target
3. Select `Build Phases`
4. Select `Copy Bundle Resources`
5. Click `+` to add a video

![add video to project](https://github.com/peterleng150/IOSVideoBackgroundOverlay/raw/master/Assets/add-video-to-project.png "add video to project")

## Issues

There is a bug in Apple's [AudioToolbox](https://developer.apple.com/documentation/audiotoolbox) that will show a false positive memory leak in Instruments when playing a video with sound on a simulator*. On a device, it's fine.

> *[One](https://crosbymichael.com/avaudioplayer-memory-leak.html) of many sources.

## License

`IOSVideoBackgroundOverlay` is released under an [MIT License][mitLink]. See [LICENSE](LICENSE) for details.

## Authors

Peter Leng https://github.com/peterleng150


[podLink]:https://cocoapods.org/pods/SwiftVideoBackground
[mitLink]:https://opensource.org/licenses/MIT
