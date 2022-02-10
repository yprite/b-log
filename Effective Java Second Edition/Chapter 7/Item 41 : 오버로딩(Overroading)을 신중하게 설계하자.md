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
 
