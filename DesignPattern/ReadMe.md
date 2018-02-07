# 안드로이드 디자인 패턴

## 1. SOLID 법칙
##### 1) S(SRP) 단일 책임 원칙
> + 정의 :<br>
한 클래스는 하나의 책임만 가져야 한다.<br>
즉 작성된 클래스는 하나의 기능만 가지며 클레스가 제공하는 모든 서비스는 그 하나의 책임을 수행하는데 집중되어야 한다는 원칙이다.<br>
어떤 변화에 의해 클래스를 변경해야 하는 이유는 오직 하나뿐이어야 함을 의미한다.<br>
SRP원리를 적용하면 책임 영역이 확실해지기 떄문에 다른 책임의 변경으로부터 연쇄작용에서 자유로울 수 있다.<br>
원리는 간단하지만 실제로 적용시키기에는 많은 노력과 시간이 필요할 것 같다. <br>
> + 적용방법 :<br>
리펙토링에서 대부분의 위험상황에 대한 해결방법은 직/간접적으로 SRP원리와 관련이 있으며, 이는 곧 책임을 최대한 최상의 상태로 분배한다는 뜻이다.
> + 적용이슈 :<br>
클래스는 자신의 이름이 나타내는 일을 해야한다.<br>

##### 2) O(OCP) 개방-폐쇄 원칙
> + 정의 :<br>
소프트웨어 요소(컴포넌트, 클래스, 모듈, 함수)는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.<br>
이것은 변경을 위한 비용은 가능한 줄이고 확장을 위한 비용은 가능한 극대화 해야 한다는 의미로, 요구사항의 변경이나 추가사항이 발생하더라도, 기존 구성요소는 수정이 일어나지 말아야 하며, 기존 구성요소를 쉽게 확장해서 재사용할 수 있어야 한다는 뜻이다.<br>
> + 적용방법 :<br>
변경(확장)될 것과 변하지 않을 것을 엄격히 구분한다.<br>
이 두 모듈이 만나는 지점에 인터페이스를 정의한다.<br>
구현에 의존하기보다 정의한 인터페이스에 의존하도록 한다.<br>
> + 적용이슈 : <br>
확장되는 것과 변경되지 않는 모듈을 분리하는 과정에서 크기 조절에 실패하면 오히려 관계가 더 복잡해 질 수 있다. <br>
인터페이스는 가능하면 변경되어서는 안된다.<br>


##### 3) L(LSP) 리스코프 치환 원칙
> + 정의 : <br>

> + 적용방법 : <br>
> + 적용이슈 : <br>

##### 4) I(ISP) 인터페이스 분리 원칙
> + 정의 : <br>
> + 적용방법 : <br>
> + 적용이슈 : <br>

##### 5) D()
> + 정의 : <br>
> + 적용방법 : <br>
> + 적용이슈 : <br>

#### 종류
+ Singletone

#### 참조
+ [NEXTREE](http://www.nextree.co.kr/p6960/)