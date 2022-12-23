### Java 데이터 타입
- Java에서의 Data Type은 크게 Primitive Type (기본형), Reference Type (참조형) 두 타입이 있다.

### **Primitive Type** (원시 타입, 기본형)
- 8가지의 기본형 타입을 미리 정의하여 제공한다.
- byte, short, int, long, float, double, boolean, char
- 실제 값을 비교하기 때문에 (== 연산자 비교 O) 


### **Wrapper Class** (래퍼 클래스)
- Wrapper Class는 Primitive Type을 객체로 만든 것
- 객체로 만들었기 때문에 null 가능
- 객체의 주소값을 비교하기 때문에 (== 연산자 비교 X, equals() 메서드로 비교)

### **Primitive Type** vs **Wrapper Class**

- int, character 빼고 Primitive Type 맨 앞을 대문자로 바꿔주면 Wrapper Class

|  Primitive Type | Wrapper Class |
| --------------- | ------------- |
|      byte       |     Byte      |
|      short      |     Short     | 
|      int        |  **Integer**  | 
|      long       |     Long      |
|      float      |     Float     |
|      double     |     Double    |
|      boolean    |     Boolean   |
|      char       | **Character** |