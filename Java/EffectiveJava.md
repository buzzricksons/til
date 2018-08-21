# 규칙1 생성자 대신 정적 팩토리 메서드를 사용할 수 없는지 생각해 보라
정적 팩토리 메서드만 있는 클래스를 만들면 생기는 가장 큰 문제는, public이나 protected로 선언된 생성자가 없으므로 하위클래스를 만들 수 없다는 것이다.

## 정적 팩토리 메서드 이름
- valueOf: 단순하게 말하자면, 인자로 주어진 값과 같은 값을 갖는 객체를 반환한다는 뜻. 따라서 이런 정적 팩토리 메서드는 형변환(type-conversion)메서드 이다.
- of: valueOf를 더 간단하게 쓴 것이다.EnumSet덕분에 인기를 모은 이름이다.
- getInstance: 인자에 기술된 객체를 반환하지만 인자와 같은 값을 같지 않을 수도 있다. 싱글턴 패턴을 따를 경우, 이 메서드는 인자 없이 항상 같은 객체를 반환한다.
- newInstance: getInstance와 같지만, 반환될 객체의 클래스와 다른 클래스에 팩토리 메서드가 있을때 사용한다. Type은 팩토리 메서드가 반환할 객체의 자료형이다.
- getType: getInstance와 같지만, 반환될 객체의 클래스와 다른 클래스에 팩터리 메서드가 있을때 사용한다. Type은 팩토리 메서드가 반환할 객체의 자료형이다.
- newType: newInstance와 같지만, 반환될 객체의 클래스와 다른 클래스에 팩토리 메서드가 있을때 사용한다. Type은 팩토리 메서드가 반환할 객체의 자료형이다.

# 규칙2 생성자 인자가 많을 때는 Builder 패턴 적용을 고려하라
- 마지막 단계에서 아무런 인자없이 build 메서드를 호출하여 immutable객체를 만듦.
- 생성자와 비교했을 때 빌더 패턴이 갖는 장점: 빌더 객체는 여러개의 varargs인자를 받을 수 있다는 것이다. 생성자는 메서드와 마찬가지로 하나의 varargs만 인자로 가질 수 있다. 
하지만 빌더는 인자마다 별도의 설정 메서드를 사용하므로, 설정 메서드마다 하나씩, 필요한 만큼 많은 varargs인자를 사용할 수 있다.
- 빌더 패턴에도 단점은 있다. 객체를 생성하려면 우선 빌더 객체를 생성해야 한다. 실무에서 빌더 객체를 만드는 오버헤드가 문제가 될 소지는 없어 보이지만, 성능이 중요한 상황에선 그렇지 않을 수도 있다.
- 점층적 생성자 패턴보다 많은 코드를 요구하기 때문에 인자가 충분히 많은 상황(가령, 네개 이상)에서 이용해야 한다. 우선은 생성자와 정적 팩토리로 시작하되 인자 개수가 통제할 수 없을
정도로 많아지면 빌더 패턴을 적용.

# 규칙3 private 생성자나 enum 자료형은 싱글턴 패턴을 따르도록 설계하라
## JDK 1.5 이전

## JDK 1.5 이후