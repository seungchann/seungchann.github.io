---
title: "[Design Patterns] Singleton Pattern"
excerpt: "Design Patterns - Singleton Pattern"
categories: 
  - Design Pattern
tags:
  - Design Pattern
  - iOS
modified_date_at: 2022-04-12T21:00:00
---
## Singleton 패턴이란?  
* `Singleton` 패턴은 하나의 클래스에서 **단일 instance**를 사용하도록 제한합니다.  
* 이 패턴은 iOS 앱 개발에서 매우 자주 사용됩니다.  
* `Singleton plus` 패턴도 흔히 사용됩니다.  
  * `Singleton plus` 패턴에서는 다른 instance들이 생성되는 것을 허용하는 **shared singleton instance**를 제공합니다.  
<br>
<center><img src="/assets/images/design_pattern/singleton_pattern/singleton_pattern_black.png"></center>

## 언제 strategy 패턴이 사용될까?  
* 하나의 클래스에서 여러 개의 instance를 사용해서 문제가 생길 경우, **singleton** 패턴을 사용합니다.  
* **shared instance**가 대부분 유용하게 사용되지만, **custom instance** 생성도 필요한 경우에는 **singleton plus** 패턴을 사용합니다.  
  * 예시로는, 파일 시스템 접근을 담당하는 `FileManager`가 있습니다.  
  * `singleton`인 "default" 인스턴스도 있고, 본인만의 인스턴스를 만들 수도 있습니다.  
  * 만약 background 스레드에서 사용하고 있다면, 본인만의 인스턴스를 만들어 사용할 것입니다.  

## Strategy 패턴을 사용할 때 주의해야 할 점  
* `Singleton` 패턴을 남용(overuse)하지 않도록 주의해야 합니다.  
* 만약 `singleton` 패턴을 사용하고 싶은 상황이 생겼다면, 먼저 다른 방법으로 목표를 달성할 수 있는지 고려해봐야 합니다.  
* 예를 들어, 단순하게 하나의 view controller에서 다른 view controller로 정보를 옮길 때에는 `singleton`이 적절하지 않습니다.  
  * 대신에, `initializer`나 `property`를 통해 model을 넘기는 것을 고려해봐야 합니다.  
* 정말로 `singleton` 패턴을 사용해야 겠다고 결정했다면, `singleton`패턴과 `singleton plus` 패턴 중에 어느 것이 더 적합한지를 따져봐야 합니다.  
  * 하나 이상의 instance가 존재한다면 문제가 발생할까?  
  * 커스텀 instance를 만들 수 있다면 유용하게 사용될까?  
* `Singleton`에서 공통적으로 문제가 되는 부분은 `testing`입니다.  
  * 만약에 state가 `singleton`과 같이 전역 변수에 저장되어 있다면, 테스트의 순서가 중요해집니다.  
  * `mock`하기도 힘들어집니다.  
* `Singleton`이 전혀 어울리지 않는 곳에 사용해서 `code smell`이 나지 않도록 주의해야 합니다.  
  * 만약에 여러 custom instance가 필요한 곳이라면, regular object가 더 적합할 것입니다.  

## Key Points  
* `Singleton` 패턴은 하나의 클래스에서 **단일 instance**를 사용하도록 제한합니다.  
* `Singleton plus` 패턴에서는 **"default" shared instance**도 제공하며, 다른 instance들을 생성하는 것도 허용됩니다.  
* 이 패턴을 남용하지 않도록 주의해야 합니다.  
  * `Singleton`을 만들기 전에, 다른 방법으로 문제를 해결할 수 있는지 고려해봐야 합니다.  
  * `Singleton`이 최선의 방법이라면, 되도록 `singleton plus` 패턴을 활용하는 것이 좋습니다.  

## References  
* Design Patterns by Tutorials (raywenderlich)  
* Github 예제 [link](https://github.com/seungchann/fundamental-design-pattern-example/tree/main) (commit: 15dbb2b)  