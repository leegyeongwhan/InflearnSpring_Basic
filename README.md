# 스프링 핵심원리 기본편

### 0섹션 1섹션

   - 예전 스프링은 빌드를 하고 tommcat 설치 설정들 설정 해야 하는 어려움이 무척 많았다. 스프링부트는 이러한 어려움을 해결해주는 껍데기라고 생각하자. 즉 라이브러리 호환 버전 설정들을 대부분 해준다.
  
  - 스프링 생태계 , 스프리 서큐리티 스프링 데이터 스프링 프레임워크 스프링 부트 등등 을 스프링이라 부르자
   
   - 객체 지향과 스프링

       - 역할(인터페이스) 구현(클래스,객체) 를 구분 하자 객체 지향의 원칙 중 다형성이 꽃이다 인터페이스 들과 구현체 클래스 겍체들 과의 협력 관계에 집중하고 원칙들을 따져가며 설계하자 이것이 좋은 개발자의 설계이다.
      - 다형성의 본질은 클라이언트를 변경하지 않고 서버의 구현 기능을 유연하게 변경 하는 것이다.
   - solid원칙 과 다형성
   
       - 역할(인터페이스가) 을 변경하면 클라이언트,서버 모두에 변경이 일어난다 ex) 자동차 → 비행기 개발자는 인터페이스를 안정적으로 잘 설계해야 한다 스프링은 이런 다형성을 극대화 시켜준다.
       - ocp ,dop 운전자는 자동차 역할만 알아야지 k5,k3 자동차의 구조는 알 필요가 없다. 즉 운전자 클라이언트는 역할에(인터페이스)에 의존해야 한다 → (추상화에만 의존해라 구체화에 의존하지 마라.)
           하지만 우리는  현실적으로 다형성 만으로는 클라이언트 코드의 변경을 막을 수가 없다 이것은 spring의 탄생을 야기한다.

### 2섹션 객체 지향원리 적용


   - 우리는 인터페이스(역할) 구현(클래스로) 지금까지 구분을 지었다 하지만 결국 자바코드만 으로는 클라이언트 코드의 변경을 막을 수없었다 ex) 새로운 할인정책이 들어왔을때 주문 서비스가 인터페이스 뿐만 아니라 new class명 으로 구체적인(할인정책)도 읜존하게된다. 이것은 즉 앞서 말한 solid 원칙  중 dip원칙 위반이다.

   - 해결책
      이것은 즉 클라이언트(주문 서비스)가 너무 많은 일을한다. 우리는 이것을  관심사의 분리를 해야한다. ex) 공연으로 치면 배우가 배우 초빙,공연,섭외까지 다하고있다.
     
   -  우리는 구체적인 구현만 하는 공연 계획자가 필요하다. Appconfig는 공연계획자이다. 구체적인 구현체들은 이친구가 한다. 즉 appconfig 를통해 구현하고 클라이언트 코드는 바꿀     필요가 업어진다 ex) 할인정책을 클라이언트 코드변경 없이 바꿀수있다.

   - 제어의역전
      이렇게 되면 역할은 다른 구현체들의 정보를 모르게된다 appconfig가 실행 권한을 가지기 때문에 이런 역할과 구현체를 나누고 appconfig를 통한 ,의존성 주입을 통한설계를 통   하면 정적인 클래스,인터페이스 관계를 안바꾸고 동저인 것만 변경 가능하다. 그리고 우리는 이제 앞으로 더욱이 발전해 스프링 컨테이너를 통해 이역할을 할 것이다.
      
      
### 스프링 컨테이너와 빈

   - 순수 자바 코드가 아닌 이제 스프링 컨테이너에 자바 빈들을 의존 관계(di)를 주입 시켜 사용한다.      ApplicationContext + Beanfactory 를 보통 스프링 컨테이너라 한다.
   
   - ApplicationContext는 Beanfactory의 기능을 상속받는다. -> 빈의 관리 기능 + 편리한 부가 기능 제공   이밖에도 여러 편리학 어플리케이션 이벤트, 환경 변수등 관련된 기능들을 상속받고있다.
   
   - 특히 예전 스프링을 사용할때 xml파이리반으로 빈들을 등록하여 스프링 컨테이너 처럼썼는데 ApplicationContext는 여기서 유연함을 보인다 xml 기반으로 바꾸기만 하면 똑같이 사용 가능하다.
   
   - 이 처러 스프링이 다양한 형식을 지원하는건 스프링 컨테이너가 -> BeanDefinition 의 역할에만 의존하기때문 즉 스프링의 다양한 정보를 BeanDefinition 으로 추상화 해서 사용한다.

 - 우리는 지금까지 AppConfig를 통한 스프링 컨테이너(에너테이션을 사용하여) 사용과 xml을 통한 사용의 차이를 봤다 우리가 만든 순수 자바 DI 컨테이너 Appconfig는  고객이 요청할때마다 객체를 새로 생성 해야했다. -> 이것은 심각한 메모리 낭비를 발생 할 수 이다. ->해결책 객체를 1개만 생성하고 공유하자.
  -> 우리는 이것을 싱글톤 패턴이라 부른다. -> 그렇지만 싱글톤 패턴도 문제가 있다! 이것은 스프링컨테이너가 다 해결해준다. 다음 시간엔 이것을 배워보자.

### 싱글톤 컨테이너


   - 싱글톤 패턴
   
     -  순수 DI 컨테이너 의 새로 객체를 생성 하는 문제를 해결 할 수 있다.
     -  객체 인스턴스를 2개 이상 생성하지 못하도록 막아야한다.
     -  우리는 private 생성자를 사용해 외부에서 new사용을 막아보았다.
     -  주의! 공유필드는 항상 조심하자 필드를 공유하지말ㄹ고 1.지역변수,2.파라미터를 쓰자
 
 - 싱글톤 컨테이너
     싱글톤 패턴의 여러 문제들을 해결해준다 실습을 하면서 컨테이너에 등록된 객체들이 한번만 호출 되는지 확인하였고  이것은 @Configuration 와 깊은 연관이있다. 바이트코드를    조작하여 CGLIB라이브러리를 사용하여  진정 스프링 컨테이너가 싱글톤 패턴을 보장한다는 사실을 알 수 있었다.
