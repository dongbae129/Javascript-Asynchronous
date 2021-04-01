-목차-

1. javascript 동작원리

2. javascript 런타임

3. 비동기




1. Javascript 동작원리

   javascript는 대표적으로 v8이라는 엔진을 이용하며 주요 구성 요소는 call stack, memory heap이 존재한다.
  
   javasciprt는 싱글 스레드와 논-블로킹 언어이다.
  
  
   싱글스레드는 하나의 memory heap, 하나의 call stack을 가지고 있다.
  
   memory heap : 메모리 할당이 일어나는 곳
   call stack : 코드 실행에 따라 호출 스택이 쌓이는 곳
   
   하나의 call stack을 가지고 있다는 의미가 무엇이냐면 한번에 한가지의 일밖에 수행할수 없다는 뜻이다.
  
   call stack에는 실행될 함수가 순서적으로 쌓이게 된다. 그리고 이렇게 쌓인 함수는 제일 위에 올려진 함수가 실행완료가 돼야 밑에 있는 함수가 실행이 된다.
  
   또한, call stack에서 stack의 크기가 존재하며 해당 크기를 초과하면(실행하는 함수가 많다) stack overflow(말 그대로 stack이 넘쳤다)오류가 발생한다.
  
  
   블로킹이란 말그래도 막는것, 즉 콜스택이 멈춘상태를 말한다(보통 하나의 함수를 실행함에 있어 처리 시간이 오래걸려 다음 함수 실행까지 지연된 상태).
  
  
2. Javascript 런타임

    런타임이란, 특정 언어로 만든 프로그램들을 실행할 수 있는 환경을 뜻한다.
    
    그러면 javascript 런타임이란 javascript로 만든 프로그램을 실행할 수 있는 환경을 의미한다
    
    ![runtime](https://user-images.githubusercontent.com/36911316/113258960-8f1c9000-9307-11eb-8090-88965f1b738d.png)
    
    

    Web API는 브라우저와 함께 제공된다. 웹 API는 HTTP 전송, setTimeout , DOM Event 등과 같은 다양한 작업을 수행할 수 있다.
    
    Web API를 사용하여 백그라운드에서 비동기적으로 작업을 처리할 수 있고 , 이러한 작업이 끝나면
    자바스크립트 엔진에게 해당 작업이 끝났음을 알려주어 계속해서 작업을 수행해 나갈 수 있게 된다.
    
    Web API에서는 해당 작업을 자체적으로 처리한 뒤 콜백 큐(Callback Queue) 로 전달한다.
    이렇게 콜백 큐로 들어온 작업들은 콜 스택이 비어있을 경우에만 콜 스택으로 이동하게 되는데
    이 때 이벤트 루프(Event Loop) 가 콜 스택이 비어있는지 주기적으로 확인하고 콜백 큐에 있는 작업들을 이동시키는 역할을 한다
    
    
    
3. 비동기
    
    
    
    
    
