---
title: "[Design Patterns] Model-View-Controller Pattern"
excerpt: "Design Patterns - Model-View-Controller Pattern"
categories: 
  - Design Pattern
tags:
  - Design Pattern
  - iOS
modified_date_at: 2022-02-18T17:08:00
---
## MVC 패턴이란?  
* Model-View-Controller (MVC) 패턴은 세 가지 타입의 object로 나누어져 있습니다.  
* 세 가지 object는 다음 그림과 같이 결합되어 있습니다.  
<br>
<center><img src="/assets/images/design_pattern/mvc_pattern/MVC_pattern_black.png"></center>

#### 1. Model
* `Model`은 앱의 데이터를 포함하고 있습니다.  
* 대부분 `struct`나 간단한 `class`로 구성되어 있습니다.  

#### 2. View  
* `View`에서는 스크린에서의 시각적 요소나 컨트롤들을 표시합니다.  
* 대부분 `UIView`의 하위 클래스로 구성되어 있습니다.  

#### 3. Controller  
* `Controller`는 `model`과 `view` 사이에서 조정(coordinate)하는 역할을 합니다.  
* 대부분 `UIViewController`의 하위 클래스로 구성되어 있습니다.  

## 추가 설명  
* MVC 패턴은 iOS 프로그래밍에서 익숙하게 볼 수 있습니다.  
* Apple이 `UIKit`에서 채택한 디자인 패턴이기 때문입니다.  
<br>
* `Controller`는 하나 이상의 `model` 혹은 `view`를 포함할 수 있습니다.  
<br>
* `Controller`에서는 `model`과 `view`에 대해 `strong property`를 소유할 수 있습니다.  
* 즉, `controller`에서 직접 접근이 가능합니다.  
<br>
* 반대로, `model`과 `view`에서는 (그들이) 속해있는 `controller`에 직접 접근할 수 없습니다. (`strong reference`를 포함할 수 없습니다.)  
* 이렇게 되면 `retain cycle`이 발생할 수 있습니다.  
<br>
* `Model`에서는 `property observing`를 통해서 `controller`와 소통(communicate)합니다.  
* `View`에서는 `IBAction`을 통해서 `controller`와 소통(communicate)합니다.  
<br>
* 결과적으로, `model`과 `view`들은 `controller`들 사이에서 재사용됩니다.  
* `Controller`들은 각각의 task에 따라 logic이 구분되어 있기 때문에 재사용되기 어렵습니다. (MVC에서는 재사용하지 않습니다.)  
<br>

```
주의: View에서는 delegate를 통해서 (그들이) 속해있는 controller의 weak reference를 사용할 수도 있습니다. 
예를 들어, UITableView는 delegate나 dataSource reference를 통해 view controller의 weak reference를 포함하고 있을 수도 있습니다.
하지만, 테이블 뷰는 그 reference들이 (속해있는) controller를 가리키고 있는 것인지 알지 못합니다.
```

## 언제 MVC 패턴이 사용될까?  
* iOS 앱을 처음 만들 때 `starting point`로 MVC 패턴을 사용하면 좋습니다.  
* MVC 패턴이 아닌 추가적인 패턴들이 필요하다고 느껴질 때, 앱에 다른 패턴을 사용하면 됩니다.  

## MVC 패턴을 사용할 때 주의해야 할 점  
* MVC 패턴에도 한계가 존재합니다.  
* 모든 `object`들이 `model`, `view`, `controller`에 딱 맞게 구분되지는 않습니다.  
* 결과적으로, <u>MVC 패턴만</u> 사용한 앱은 `controller`에 너무 많은 logic들이 포함되게 됩니다.  
* 즉, View Controller가 복잡해지고, 거대해지게 됩니다.  
* 이러한 현상을 방지하기 위해서 다른 디자인 패턴도 함께 활용해줘야 합니다.  

## Key Points  
* MVC 패턴은 **model**, **view**, **controller**로 나누어져 있습니다.  
* MVC 패턴은 **model**과 **view**를 **controller**에서 재사용할 수 있습니다.  
  * 단, **controller**는 각각의 logic이 구체적으로 정해져 있으므로, <u>재사용하지 않습니다</u>.  
* **controller**는 **model**과 **view** 사이에서 조정(coordinate)하는 역할을 합니다.  
  * **model**의 데이터 값을 **view**에 띄워주고, **view**의 `IBAction` 콜을 처리합니다.  
* MVC 패턴으로 iOS 앱을 시작하는 것은 좋지만, 한계도 있습니다.  
  * 모든 object들이 **model**, **view**, **controller**로 깔끔하게 나누어 떨어지지는 않습니다.  
  * 따라서, MVC 패턴과 다른 패턴들을 함께 활용하는 것을 권장합니다.  

## References  
* Design Patterns by Tutorials (raywenderlich)  
* Github 예제 [link](https://github.com/seungchann/fundamental-design-pattern-example/tree/main) (commit: 79ec05e)  