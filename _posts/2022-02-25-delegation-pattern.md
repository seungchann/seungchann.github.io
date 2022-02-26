---
title: "[Design Patterns] Delegation Pattern"
excerpt: "Design Patterns - Delegation Pattern"
categories: 
  - Design Pattern
tags:
  - Design Pattern
  - iOS
modified_date_at: 2022-02-25T16:50:00
---
## Delegation 패턴이란?  
* object가 다른 "helper" object를 활용하는 패턴입니다.  
* 직접 object를 사용하는 대신에, "helper" object를 통해 데이터를 제공하거나 task를 실행합니다.  
* 다음 그림과 같이 세 가지 파트로 이루어져 있습니다.  
<br>
<center><img src="/assets/images/design_pattern/delegation_pattern/delegation_pattern_black.png"></center>

#### 1. `Delegate`를 필요로 하는 object (delegating object)  
* `delegate`는 대부분 weak property로 사용됩니다.  
* 왜냐하면 (`delegate` -> `delegate object` -> `delegate` -> ...) 와 같이 retain cycle을 피하기 위해서 입니다.  

#### 2. `Delegate protocol`  
* Delegate protocol에는 `delegate`를 사용하기 위해서 구현해야 하는 메서드들을 담고 있습니다.  

#### 3. `Delegate`  
* `Delegate protocol`을 준수하는 helper object 입니다.  

## 추가 설명  
* 구체적인(concrete) object 대신에 `delegate protocol`을 사용하면, 구현이 조금 더 유연(flexible)해질 수 있습니다.  
* 그렇게 된다면, 프로토콜을 준수하는 모든 object는 `delegate`로 사용될 수 있습니다.  

## 언제 delegate 패턴이 사용될까?  
* 거대한 class를 분리하려고 하는 상황이나, 일반적이고 재사용가능한 component를 만드려고 할 때 `delegate` 패턴을 사용합니다.  
* `Delegate relationship`은 Apple의 프레임워크, 특히 `UIKit`에서 익훅하게 볼 수 있습니다.  
* `DataSource-`나 `Delegate-` 이름을 가진 object들이 대부분 `delegation pattern`을 따르고 있습니다.  
* Apple 프레임워크에서는 왜 1개가 아니라 2개의 protocol을 사용할까요?   

#### 1. `DataSource`  
* Apple 프레임워크에서는 데이터를 제공하는 delegate 메서드들을 그룹화할 경우, `DataSource`라는 이름을 사용합니다.  
* 예를 들어 `UITableViewDataSource`는 `UITableViewCells`을 제공하는 역할을 합니다.  

#### 2. `Delegate`  
* Apple 프레임워크에서는 데이터나 이벤트를 받는 메서드들을 그룹화할 경우, `Delegate`라는 이름을 사용합니다.  
* 예를 들어 `UITableViewDelegate`는 특정 row가 선택될 때마다 알려줍니다.  
<br>
* `Datasource`와 `Delegate`를 같은 object에 set해주는 것이 일반적입니다.  
* 예를 들자면, `UITableView`를 소유하는 View Controller에 set하는 경우가 있습니다.  
* 하지만 반드시 같은 object에 set해 줄 필요는 없으며, 각각 다른 object에 set해서 사용했을 때 더 효율적인 경우도 있습니다.  

## Delegate 패턴을 사용할 때 주의해야 할 점  
* `Delegate`는 매우 유용하지만, 남용(overuse) 될 수도 있습니다.  
* Object에 너무 많은 `delegate`를 생성하지 않도록 조심해야 합니다.  
<br>
* Object가 여러 `delegate`를 필요로 한다면, 하나의 object가 너무 많은 일을 수행하고 있다는 지표입니다. (one catch-all class)  
* 이럴 때는 object의 여러 기능들을 use case에 따라 나누는 것을 고려해봐야 합니다.  
<br>
* (하나의 object에서 delegate의) 개수에 대한 기준이 확실하게 정해진 것은 없습니다.  
* 만약에 무슨일이 일어나는지를 이해하기 위해 여러 class들을 switching하고 있다면, 너무 많은 `delegate`를 사용하고 있다는 신호입니다.  
* 만약에 특정 `delegate`가 왜 중요한 역할을 하는지 이해하지 못한다면, 너무 적은 `delegate`를 사용하고 있다는 신호입니다.  
* 이럴 경우에는, 너무 기능을 세세하게 나누었다는 뜻입니다.  
<br>
* Retain cycle이 만들어지고 있는지 주의해야 합니다.  
* 대부분 `delegate property`는 `weak` 프로퍼티로 생성되어야 합니다.  
* 만약 object에 반드시 `delegate`를 set 해주어야 하는 상황이라면, 생성자의 input으로 `delegate`를 받는 방식을 고려해야 합니다.  
* 이러한 경우, 옵셔널 `?` 대신에 `!`을 사용하여 forced unwrapping이 필요합니다.  
* 결과적으로 object 생성 전에 `delegate`을 set해줄 수 있게 됩니다.  
<br>
* 만약 `strong`한 `delegate`를 사용하고 싶은 경우에는, `strategy` 패턴이 더 적합할 것입니다.  

## Key Points  
* `Delegation` 패턴은 **delegate를 필요로 하는 object**, **delegate protocol**, **delegate**로 나누어져 있습니다.  
* `Delegation` 패턴을 통해 거대한 class를 분리하거나, 일반적이고 재사용가능한 component를 만들 수 있습니다.  
* `Delegate`는 대부분 `weak` 프로퍼티로 사용됩니다.  

## References  
* Design Patterns by Tutorials (raywenderlich)  
* Github 예제 [link](https://github.com/seungchann/fundamental-design-pattern-example/tree/main) (commit: 43e58a3)  