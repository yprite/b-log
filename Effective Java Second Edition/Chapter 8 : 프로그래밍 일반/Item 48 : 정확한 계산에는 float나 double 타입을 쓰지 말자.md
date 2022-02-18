
float와 double 타입은 과학 계산과 공학 계산을 목적으로 설계되었음  
이진 부동소수점 연산을 수행  
이진 부동소수점 연산은 넓은 범위의 수에 대해 정확한 근사치를 빨리 산출하기 위해 설계되었음  

**float나 double 타입은 돈 계산에는 특히 부적당하다**


예를 들어, 주머니에 1.03달러가 있는데 42센트를 썻다고 하면 남은 돈이 얼마인지 출력해보는 코드는 아래와 같음
```
System.out.println(1.03 - .42);
```
애석하게도 0.6100000000001이 출력됨

```
System.out.println(1.00 - 9  * .10);
```
이 코드의 실행결과는 0.999999999998

문제는 부동 소수점 타입을 사용했기 때문

돈과 같은 정확한 계산을 위해서는 BigDecimal, int, long 타입 중 하나를 사용해야 함

그러나 BigDecimal을 사용하면 두가지 단점이 있음  
1. 기본형 데이터 타입을 사용할 때보다 불편
2. 실행 속도가 더 느려짐

BigDecimal의 대안은 값의 크기가 제한되는 int나 long 타입을 사ㅇ하면서 소ㅜ점을 우리가 계산하고 유지
```
public static void main(String[] args) {
    int itemsBought = 0;
    int funds = 100;
    for (int price = 10; funds >= price; price += 10) {
        itemsBought++;
        funds -= price;
    }
    System.out.println(itemBought + " items bought.");
    System.out.println("Money left over : " + funds + " cents");
}
```

# 요약
- 근사치가 아닌 정확한 결과가 필요한 계산에서는 float나 double 타입을 사용하지 않음  
- 만일 시스템에서 소수점 계산과 유지를 해주길 원하고, 사용의 불편함과 기본형 데이터 타입을 사용하지 않는데 따른 비용을 개의치 않는다면, BigDecimal을 사용  
- BigDecimal을 사용하면 추가적인 장점을 갖음
- 반올림이 수반되는 연산을 할 떄는 언제든지 8가지 반올림 모드를 이용해서 반올림을 완벽하게 제어 할 수 있음
- 수의 크기가 십진수 9자리를 넘지 않는다면 int 타입
- 수의 크기가 십진수 18자리를 넘지 않으면 long 타입
- 수의 크기가 십진수 18자리를 초과하면 BigDecimal을 사용
