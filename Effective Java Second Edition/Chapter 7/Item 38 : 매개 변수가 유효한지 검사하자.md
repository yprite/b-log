대부분의 메소드와 생성자는 자신들의 매개 변수로 전달될 수 있는 값에 제한을 둠

모든 제약은 명확하게 문서화해야 하며, 메소드 몸체 코드의 맨 앞에서 검사하도록 해야 함
에러가 발생한 후 가능한 빨리 검출해야 한다는 일반적 원칙의 특별한 경우
사전 검사에 실패하면 에러의 검출이 불확실하게 되고, 에러가 생긴 소스코드를 찾기가 어려워짐


Public 메소드의 경우는 Javadoc의 @throws 태그를 사용해서 매개 변수 값의 제약을 위반했을 때 발생되는 예외를 문서화 한다.

일반적으로 IllegalArgumentException, IndexOutOfBoundsException, NullPointerException 예외

```
  /**
     * Returns a BigInteger whose value is {@code (this mod m}).  This method
     * differs from {@code remainder} in that it always returns a
     * <i>non-negative</i> BigInteger.
     *
     * @param  m the modulus.
     * @return {@code this mod m}
     * @throws ArithmeticException {@code m} ≤ 0
     * @see    #remainder
     */
    public BigInteger mod(BigInteger m) {
        if (m.signum <= 0)
            throw new ArithmeticException("BigInteger: modulus not positive");

        BigInteger result = this.remainder(m);
        return (result.signum >= 0 ? result : result.add(m));
    }
```


외부에 공개하지 않고 패키지나 클래스 내부에서 사용하는 메소드의 경우에는 해당 패키지나 클래스의 저자인 우리가 메소드 호출 상황을 제어할 수 있음

따라서 유효한 매개 변수 값만이 전달되는지를 확인할 수  있고 또한 반드시 확인해야 함

public이 아닌 메소드에서는 assertion을 사용해서 매개변수를 검사
```
private static void sort(long a[], int offset, int length) {
    assert a != null;
    assert offset >= 0 && offset <= a.length;
    assert length >= 0 && length <= a.length - offset;
    //계산 수행 ...
}
```


본질적으로, Assertion은 클라이언트가 어떻게 사용하는 지와는 관계없이 지정한 조겅이 true일 것


일반적인 유효성 검사와 단언문이 다른 점

실패하면 AssertionError를 던집니다.
런타임에 아무런 효과도, 아무런 성능 저하도 없습니다(단, java를 실행할 때 명령줄에서 -ea 혹은 --enableassertions 플래그를 설정하면 런타임에 영향을 줍니다).


메소드나 생성자를 작성할 때마다 매개 변수에 어떤 제약을 둘 것인지 심사 숙고해야 한다.
그리고 그런 제약을 문서화하고 메소드 몸체의 맨 앞에서 명시적인 검사를 하도록 해야 한다.
또 그렇게 습관 들이는 것이 좋다.
