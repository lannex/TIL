# Native Module Setup for iOS
javascript만으로 처리하기 힘든 상황이 제법있다.
어떻게든 고쳐야 된다면 native로 접근해야 한다.

## Xcode
1. 메뉴에서 **File** > **New** > **File…**
2. **Swift File** 선택
3. 파일명을 정하고 폴더를 만들어진 app폴더로 설정
4. Objective-C Bridging Header가 안되어 있으면 **Create Bridging Header**를 선택
5. 헤더명은 `YourProject-Bridging-Header.h` 이런식인데 파일명을 변경하면 **안됨**
6. **Targets**의 **Build Settings**가서 **Objective-C Bridging Header**를 선택
7. `YourProject-Bridging-Header.h`에 아래 코드 추가

```objective-c
// CounterApp-Bridging-Header.h
#import "React/RCTBridgeModule.h"
```

## Objective-C to Swift
여기서부터는 objective-c와 주고 받아야 됨

아래 코드는 만들어진 swift 파일 초기화

```swift
// YourProject.swift

import Foundation

@objc(YourProject)
class YourProject: NSObject {
  @objc
  func count() -> [AnyHashable : Any]! {
    return ["count": 0]
  }
}
```

swift와 마찬가지로 새로운 **Objective-C File**을 만듬

그리고 `RCT_EXTERN_MODULE`를 사용해서 swift로 넘김

```objective-c
// YourProject.m
#import "React/RCTBridgeModule.h"
@interface RCT_EXTERN_MODULE(YourProject, NSObject)
RCT_EXTERN_METHOD(count)
@end
```

모듈명 바꾸려면 이렇게 호출

```objective-c
// YourProject.m
#import "React/RCTBridgeModule.h"
@interface RCT_EXTERN_REMAP_MODULE(RNYourProject, YourProject, NSObject)
RCT_EXTERN_METHOD(count)
@end
```

## Javascript
react에서 처리
```js
// App.js
import { NativeModules } from 'react-native'
console.log(NativeModules.YourProject.count())
```
