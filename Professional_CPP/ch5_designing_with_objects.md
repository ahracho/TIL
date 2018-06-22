# Profession C++ (by Marc Gregoire)

#### 블록체인 코어 개발 스터디 5주차 (5/4)


# Chapter 5 : Designing with Objects

## WHAT’S IN THIS CHAPTER?
- OOP가 무엇인지 알아본다.
- 서로 다른 객체들의 관계를 어떻게 정의하는지 알아본다.
- 추상화가 무엇이고 왜 중요한지 알아본다.

---

# The Object-Oriented Philosophy
OOP적으로 사고한다는 것은 이 프로그램은 무엇을 프로그램이지? 하고 Procedural로 생각하는 것이 아니라, 현실 세계의 무엇을 모델링하고 있는지를 생각하는 것이다. OOP는 task에 따라서 프로그램을 나누지 않고, 물리적인 객체로 나눠서 생각한다. 

## Classes
클래스는 종을 나타내는 것이고, 하나의 객체는 클래스의 인스턴스이다. An object is an instance of a class - a particular item with characteristics that distinguish it from other instances of the same class.

## Components
Component는 클래스와 같지만 좀 더 작고 구체적인 단위이다. 비행기가 하나의 클래스가 될 수도 있지만, 상황에 따라서는 비행기 안의 부품들이 하나의 클래스로 만들어져야 할 때도 있다. 

## Properties
속성은 객체들이 서로 다르게 해주는 요소이다. 오렌지라는 클래스(오렌지라는 추상적인 개념)에서 우리 눈 앞에 있는 실제 오렌지가 파생되는지 각각의 오렌지마다 당도도 다르고, 산도도 다를 것이다. 여기서 당도와 산도가 오렌지의 속성이 되는 것이다. 

객체의 속성 뿐만 아니라 클래스의 속성도 있는데, 객체의 속성이 객체마다 다른 것에 비해, 클래스의 속성은 클래스에서 나온 모든 객체들에게 동일하게 적용된다.  

## Behaviors
속성과 마찬가지로 각 객체 또는 클래스가 어떤 동작을 할 수 있는지 정의할 수도 있다. 

# Object Relationships
## The Has-A Relationship
객체 간의 관계가 Has-A로 정의된다면, component일 경우가 많다. 예를 들어, 윈도우 창에 Save 버튼이 있는 UI를 생각해보자. 윈도우 창과 버튼은 각각 다른 클래스에서 나온 객체이지만 서로 연결되어 있다. 이럴 때 버튼이 윈도우 안에 있기 때문에 Window has a button이라고 표현할 수 있다. 

## The Is-A Relationship (Inheritance)
Is-A 관계는 OOP의 핵심 개념이다. 상속의 개념은 여러 클래스가 상하 관계로 정리될 수 있는 것을 의미한다. 예를 들어 UI에서 버튼에도 체크 버튼, 라디오 버튼 등 여러 종류가 있다. 버튼을 간단히 클릭할 수 있고, 어떤 행동을 하는 클래스라고 하면 체크 버튼도 버튼의 기본 속성과 행동을 모두 가지면서 자기만의 가질 수 있는 속성과 행동을 추가할 수 있다. 

여러 클래스가 비슷한 속성과 행동을 가지고 있다면 그들을 묶여서 base class를 만들 수 있을지 고민해 보아야한다. 

### Inheritance Techniques
#### Adding Functionality and Properties
부모 클래스의 속성과 행동에 자식 클래스만 가질 수 있는 속성과 행동을 더할 수 있다.
#### Replacing Functionality and Properties 
자식 클래스는 부모 클래스로부터 물려받은 행동을 자신의 것으로 대체하거나 override 할 수 있다. 만약에 자식 클래스가 부모 클래스의 모든 행동을 새로 정의하였다면 상속하는 것이 바람직한 경우가 아니었음을 뜻한다. 속성을 override 할 수도 있지만 하지 않는 것이 좋다. 부모 클래스의 속성이 다른 이름으로 자식 클래스에 새롭게 정의되어 있을 수도 있고, 부모 클래스의 속성이 특별한 의미를 담고 있는 경우라면 override하는 것이 올바르지 않을 수 있기 때문이다. 

# Abstraction
## Interface vs. Implementation
추상화의 핵심은 인터페이스와 구현을 분리하는 것이다. OOP에서 클래스 인터페이스란 모두가 사용할 수 있도록 공개된 속성과 행동들을 의미한다. 좋은 인터페이스는 Public behavior만 담고 있다. property/variable은 절대 밖으로 드러나서는 안되고 getter/setter를 통해 공개되어야 한다. 

## Deciding on an Exposed Interface
Public은 어떤 코드든 접근할 수 있다는 의미, Protected는 자식 클래스만 접근할 수 있다는 의미, Private은 자식 클래스도 접근할 수 없다는 의미이다. 어떤 걸 Public으로 둘지에 대한 고민을 해야한다. 
