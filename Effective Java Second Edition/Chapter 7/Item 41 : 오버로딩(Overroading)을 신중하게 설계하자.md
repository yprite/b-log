```
public class CollectionClassifier {
  public static Strig Classify(Set<?> s) {
    return "Set";
  }
  public static Strig Classify(List<?> s) {
    return "List";
  }
  public static Strig Classify(Collection<?> s) {
    return "Unknown Collection";
  }
  public static void main(String[] args) {
    Collection<?>[] collections = {
      new HashSet<String>(),
      new ArrayList<BigInteger>(),
      new HashMap<String, String>().values()
    };

    for(Collection<?> c: collections) {
      System.our.println(classify(c));
    }
  }
}
```
 이 프로그램 실행 결과는 Unknown Collectino이 세번을 출력  
 Classify 메소드가 오버로딩되어서, 호출된 메소드가 컴파일 시점에 결정되기 때문  
 오버로딩된 메소드의 선택은 정적(Static)인 반면, 오버라이딩(Overriding)된 메소드의 선택은 동적  
 오버로딩의 혼란스런 사용을 피해야 함
 
 안전하면서 보수적인 정책이라면, 같은 수의 매개 변수르 갖느 두개의 오버로딩 메소드를 절대 사용하지 않는다는 거
 
 ObjectOutputStream 클래스를 생각해보면 write 메소드를 갖고 있으며, 오버로디 하기보다는 메소드 시그니처를 다르게 하고 있음
 - writeBoolean(boolean)
 - writeInt(int)
 - writeLong(long)
 
 1.5 배포판 이전에느, 모드 기본형들이 모든 참조 타입과 근복적으로 다르 취급되었지마, 1.5 배포판 이후에는 오토박싱이 추가되어 더 이상 그렇지 않음
 
 요약하면, 메소를 오버로딩 할 수 있다고 해 반드시 그렇게 하라는 것은 아님
 같은 개수의 매개변수를 갖는 메소드 시그니처르 사용해서 메소드를 오버로디 하는 것은 가급적 삼가야 함
 생성자가 오버로딩 되는 경우에느 그런 충고를 따르지 못할 수 있음
