# DesignPattern_Study_Prototype

# Notion Link
https://five-cosmos-fb9.notion.site/Prototype-3c106cc1f9e84b7e8f76ec6c368d43ea

### 원형(Prototype) 패턴

원형이 되는(prototypical) 인스턴스를 사용하여 생성할 객체의 종류를 명시하고,

이렇게 만드는 견본을 복사해서 새로운 객체를 생성하는 패턴.

**빌더나, 팩토리 패턴과는 다른 형태의 패턴!**

어떻게 보면 Copy 타입이지, 어떻게 프로토 타입이냐? 라고 할 수 있다ㅡ.

- *“오브젝트가 copy가 되기 전 까지의 상태 를 프로토타입으로 가지고 있어라”* 라는 것
- 미완성된 프로토타입 오브젝트를 이용하여(Clone) 원하는 최종 오브젝트를 만들어낸다.
- **`중간 단계의 오브젝트를 프로토타입 오브젝트로 만들고`**
- **`이를 DeepCopy 하여 최종 오브젝트를 만들어 나가는 것이라 볼 수 있다.`**

**특징**

1. 추상 클래스 패턴과는 반대로 클라이언트 응용 프로그램 코드 내에서 객체 창조자(Creator)를 서브 클래스(Sub Class) 하는 것을 피할 수 있게 해준다.
2. 새로운 객체는 일반적인 방법(예를 들어, new를 이용한다거나)으로 객체를 생성(create) 하는 고유의 비용이 주어진 응용 프로그램 상황에 있어서 불가피하게 매우 클 때, 이 비용을 감내하지 않을 수 있게 해준다.

<aside>
💡 즉, 객체를 복사하여 생성하는 방식이므로 다수의 객체를 생성해야 할 경우 
객체 생성의 비용을 효과적으로 감소시킬 수 있다.

프로토타입이 존재하고 복제만 해서 객체를 생성하게 되므로 서브 클래스의 수를 줄일 수 있다.

</aside>

**고양이(Cat) 클래스를 이용해 Kitty, Nabi 오브젝트를 만드려고 할 때** 

- 가장 기본적인 방법으로는 Cat 클래스를 선언하고 그 속성 값들을 원하는 값으로 매핑해줄 수 있을 것이다.
    - 비효율적이야..!

```java
Cat kitty = new Cat();
kitty.setName("Kitty");
kitty.setEyeColor("White");
kitty.setTailColor("White");
kitty.setBodyColor("White");

Cat nabi = new Cat();
kitty.setName("Nabi");
kitty.setEyeColor("White");
kitty.setTailColor("White");
kitty.setBodyColor("White");
```

![image](https://user-images.githubusercontent.com/18654358/156861418-1e054952-a804-4119-bc06-f3c775f10139.png)

- 위 방법은 비효율적인 측면이 있다.

**동일한 고양이 클래스를 사용한다면? 복제를 이용하여 조금 더 쉽게 만들어 낼 수 있지 않을까?!**

- 동일한 고양이를 반환하는 Clone 메소드가 Cat 클래스에 존재한다면
- 최초 생성한 Kitty 고양이를 이용해 clone(deepcopy)를 이용하여 nabi 를 만들어 낼 수 있다.

```java
Cat kitty = new Cat();
kitty.setName("Kitty");
kitty.setEyeColor("White");
kitty.setTailColor("White");
kitty.setBodyColor("White");

Cat nabi = kitty.clone();
kitty.setName("Nabi");
```

![image](https://user-images.githubusercontent.com/18654358/156861433-b6ac4f23-afab-417f-a39b-c52e0d7dfe0d.png)

**조금 더 디자인패턴에서 얘기하는 원형(프로토타입)패턴에 맞게 개발해볼 수 있다.**

고양이 클래스를 베이스 클래스로 만들고 검은 고양이, 하얀 고양이 클래스를 만들어 볼 수 있다.

- ***`여기서 검은 고양이와 하얀 고양이는 미완성된 프로토타입 객체이다. (중간단계 오브젝트)`***
- **`이 객체를 이용해 원하는 클래스를 만들어 내는 것!`**

```java
abstract class Cat{
	String name;
	String eyeColor;
	String bodyColor;
	String tailColor;

	public Cat clone(){
		return // deepCopy;
	}
}

class BlackCat extends Cat{
	public BlackCat(){
		super();
		super.bodyColor = "Black";
	}
}

class WhiteCat extends Cat{
	public WhiteCat(){
		super();
		super.bodyColor = "White";
	}
}

BlackCat bc = new BalckCat();
bc.eyeColor = "pink";
bc.tailColor = "green";

Kitty kitty = bc.clone();
kitty.eyeColor = "white";
kitty.name = "kitty";
```

![image](https://user-images.githubusercontent.com/18654358/156861446-2c292e4b-8f29-445e-bea0-037088e7dcf4.png)

### 활용성

원형 패턴은 제품의 생성, 복합, 표현 방법에 독립적인 제품을 만들고자 할 때 사용된다.

- 인스턴스화할 클래스를 런타임에 지정할 때 (이를테면, 동적 로딩)
- 제품 클래스 계통과 병렬적으로 만드는 팩토리 클래스를 피하고 싶을 때
- 클래스의 인스턴스들이 서로 다른 상태 조합 중에 어느 하나일 때 원형 패턴을 사용한다.

<aside>
💡 미리 원형으로 초기화해 두고, 나중에 이를 복재해서 사용하는 것이 매번 필요한 상태 조합의 값들을 수동적으로 초기화하는 것보다 더 편리할 수 있다.

</aside>

### 구조

![image](https://user-images.githubusercontent.com/18654358/156861455-5bf557c6-664a-427d-b776-14dcb396f9e9.png)

### 참여자

**Prototype**

- 자신을 복제하는데 필요한 인터페이스를 정의

**ConcreatePrototype**

- 자신을 복제하는 연산을 구현

**Client**

- 원형에 자기 자신의 복제를 요청하여 새로운 객체를 생성

---

---

### Effective Java. clone 재정의는 주의해서 진행하라

**Cloneable Interface**

<aside>
💡 cloneable : 복제해도 되는 클래스임을 명시하는 용도의 믹스인 인터페이스

</aside>

<aside>
💡 믹스인
- 클래스가 자신의 “본래 타입”에 추가하여 구현할 수 있는 타입
- 선택 가능한 기능을 제공하며, 그 기능을 제공받고자 하는 클래스에서 선언한다.

</aside>

clone 메서드가 선언된 곳이 Cloneable이 아닌 Object이고 그마저도 protected 이다.

즉, Cloneable을 구현한 것만으로 clone 메서드를 호출할 수 없다.

**Cloneable**

- Object의 protected 메서드인 clone의 동작 방식을 결정한다.
- 상위 클래스(Object)에 정의된 protected 메서드의 동작방식을 변경한 것

<aside>
💡 clone 호출 + Cloneable 구현 O : 객체의 필드들을 하나하나 복사한 객체 반환
clone 호출 + Cloneable 구현 X : CloneNotSupportedException

</aside>

**clone 메서드의 일반 규약**

클론 객체와 원본객체의 Identification 값은 다르다.

<aside>
💡 x.clone() ≠ x

</aside>

<aside>
💡 x.clone().getClass() == x.getClass()

</aside>

클론 객체와 원본 객체의 logical equation은 같으며 클론 객체와 원본 객체의 클래스가 같다.

<aside>
💡 x.clone().equals(x)

</aside>

<aside>
💡 x.clone().getClass() == x.getClass()

</aside>

**clone 메서드의 사용**

**상속에서의 주의점**

생성자 연쇄(constructor chaining)과 비슷하다.

- 상속으로 부모 클래스의 default 생성자를 계속 호출한다.
- 마찬가지로 clone 에서도 상속으로 연쇄해서 객체를 생성해야 한다.

clone 메서드가 super.clone 이 아닌 생성자를 호출해 얻은 인스턴스를 반환해도 컴파일러는 불평하지 않을 것이다.

clone을 재정의한 클래스가 final이면 하위 클래스가 없으니 관례를 무시해도 안전하다.

**상위 클래스를 제대로 상속했을 때 Cloneable 구현**

super.clone을 호출한다. (클래스에 정의한 모든 필드가 원본과 같다.)

**`불변 클래스에서 굳이 clone 메서드를 제공하지 않는게 좋다. (기존의 super.clone 으로 해결)`**

```java
@Override
public PhoneNumber clone(){
	try{
		return (PhoneNumber) super.clone();
	}catch(CloneNotSupportedException e){
		throw new AssertionError();
	}
}
```

- Object의 clone은 Object를 반환하지만 PhoneNumber에서는 PhoneNumber를 반환토록 했다.
- 재정의한 메서드의 반환 타입은 상위 클래스 메서드가 반환하는 타입(Object)의 하위 타입(PhoneNumber)일 수 있다.
    - 자바의 공변 변환 타이핑(Convariant return typing) 지원 덕분
    - 공변 변환 타이핑 : T`가 T의 subType이면, C<T`>는 C<T>의 SubType 이다.
    

**가변 객체에서 사용할 경우**

```java
public class Stack{
	private Object[] elements;
	private int size;
}

@Override 
public Stack clone(){
	try{
		Stack result = (Stack) super.clone();
		result.elements = elements.clone();
		return result;
	}catch(CloneNotSupportedException e){
		throw new AssertionError();
	}
}
```

- 위와 같이 복사를 하지 않는다면 복사한 객체는 elements의 참조값을 가지고 있어
- **`원본 객체를 수정하면 복사객체도 수정되는 현상이 일어날 수 있다.`**

**clone 메서드는 사실상 생성자와 같은 효과를 낸다.**

- clone은 원본 객체에 아무런 해를 끼치지 않는 동시에 복제된 객체의 불변식을 보장해야 한다.

**배열의 복제**

- 배열의 clone 메서드를 사용하자
- 배열은 clone 기능을 제대로 사용하는 유일한 예이다.

**HashTable에서의 복제 (복잡한 가변 객체의 복제)**

- 해시테이블 내부
    - 버킷들의 배열 + 각 버킷을 key / value 쌍을 담는 연결리스트의 첫번째 엔트리 참조
1. 배열 복제 → 버킷 배열을 복제하나, 버킷 배열안에 있는 연결리스트들은 모두 원본과 같다.
2. 각 버킷을 구성하는 연결 리스트를 복사해야 한다.
3. 연결리스트를 복제할 때 재귀적으로 호출하는 방식을 사용한다.
    1. 스택 프레임을 소비함으로 스택오버플로가 발생할 가능성이 있다.
4. 재귀 호출 대신 반복자를 써서 순회한다.
5. 원본 객체의 상태를 다시 생성하는 고수준 메서드를 호출한다. put(key, value)
    1. 저수준 API 보다 속도가 느리다.
    2. Cloneable 아키텍처의 기초적인 필드 단위 객체 복사를 우회한다.

**Clone의 상속에서 주의점**

1. Cloneable 구현 여부를 하위 클래스에서 선택하도록 해준다.
2. clone을 동작하지 않게 구현해놓고 하위 클래스에서 재정의 못하게 한다.

```java
@Override
protected final Object clone() throws CloneNotSupportedException{
	throw new CloneNotSupportedException();
}
```
