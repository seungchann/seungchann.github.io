---
title: "[Design Patterns] Strategy Pattern"
excerpt: "Design Patterns - Strategy Pattern"
categories: 
  - Design Pattern
tags:
  - Design Pattern
  - iOS
modified_date_at: 2022-04-11T00:25:00
---
## Strategy 패턴이란?  
* `Strategy` 패턴은 런타임에서 set되거나 switch될 수 있는, interchangeable한 object들의 family를 정의합니다.  
* 다음 그림과 같이 세 가지 파트로 이루어져 있습니다.  
<br>
<center><img src="/assets/images/design_pattern/strategy_pattern/strategy_pattern_black.png"></center>

#### 1. `strategy`를 사용하는 object  
* 대부분의 ios 앱 개발에서 strategy 패턴이 사용될 경우, view controller가 이러한 object입니다.  
* 하지만, interchangeable behavior가 필요하다면 모든 종류의 object들이 (기술적으로는) 이러한 object가 될 수 있습니다.
#### 2. `strategy protocol`  
* `Strategy protocol`은 모든 `strategy`가 반드시 구현해야 할 메서드들을 정의하고 있습니다.  
#### 3. `strategies`  
* `Strategy`란 `strategy 프로토콜`을 준수하는 object 입니다.  

## 언제 strategy 패턴이 사용될까?  
* 두 가지 이상의 `interchangeable`한 behavior를 사용해야 할 때, `strategy` 패턴을 사용합니다.  
* `Strategy` 패턴은 `Delegate` 패턴과 비슷합니다.  
  * 둘 다 유연성(flexibility)를 높이기 위해서, protocol 기반으로 사용됩니다.  
  * 결과적으로, `strategy protocol`을 구현한 모든 object들은 런타임에서 `strategy`로 사용될 수 있습니다.  
* 단 `delegation`과는 다르게, `strategy` 패턴은 object들의 family를 사용합니다.  
* `Delegate`는 런타임에서 fix되어 있습니다.  
  * 예를 들어 `UITableView`의 `dataSouce`와 `delegate`들은 Interface Builder에 set되어 있기 때문에, 런타임 중에 바뀌는 경우는 드문 경우입니다.  
* 하지만, `strategy`는 런타임 중에도 쉽게 interchangeable할 수 있도록 되어 있습니다.  

## Strategy 패턴을 사용할 때 주의해야 할 점  
* `Strategy` 패턴을 남용(overuse)하지 않도록 주의해야 합니다.  
* 특히 behavior가 바뀌지 않는 경우에는, 바로 view controller나 object context 안쪽에 넣어줘도 좋습니다.  
* 이 패턴의 trick은 behavior를 꺼내 써야할 때를 알고있다는 것입니다.  
  * behavior가 필요한 곳만 정해준다면, 천천히 (behavior를) 해도 괜찮습니다.  

## Key Points  
* `Strategy` 패턴은 런타임에서 set되거나 switch될 수 있는, interchangeable한 object들의 family를 정의합니다.  
* `Strategy` 패턴은 **strategy를 사용하는 object**, **strategy protocol**, **strategy**로 나누어져 있습니다.  
* `Strategy` 패턴은 `delegation` 패턴과 비슷합니다.  
  * 두 패턴 모두 유연함을 위해 protocol을 사용합니다.  
  * `strategy`는 런타임에서도 switch될 수 있지만, `delegation`은 fix됩니다.  

## References  
* Design Patterns by Tutorials (raywenderlich)  
* Github 예제 [link](https://github.com/seungchann/fundamental-design-pattern-example/tree/main) (commit: 847f9e4)  