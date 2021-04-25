-목차-

* javascript 동작원리
* javascript 런타임
* 비동기


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
    
    위에서 알아봤듯이 비동기는 코드의 실행을 멈추지 않고 다음 코드를 실행시킨다.
    
    비동기 방식으론 대표적으로 callback 함수, Promise, async 을 이용한 3가지가 있다.
    
    * 비동기 함수에 파라미터로 받은 callback 함수를 사용하여 비동기로 받은 데이터를 이어서 사용할수있다.
      문제점으로는 callback hell이라는 콜백지옥인데, 이는 콜백함수 내부에 또 콜백함수가 계속 들어가는 현상으로 기능상으로는 문제가 없지만
      가독성과 앞으로 로직변경에 힘들수 있나는점이 있다.
    
    * Promise는 비동기 처리에 사용되는 객체이다. 

````
function getData() {
        
           return new Promise(function(resolve, reject) {
           
             //서버작업 {
                  resolve();
               }
           });
           
         }
         
         getData().then((response)=>{
         
            console.log(response);
            }
         ).catch(function(err) {
         
           console.log(err); // Error: Request is failed
         });
````
Promise에서 함수를 하나 실행하는데 해당 함수는 resolve, reject라는 두개의 파라미터를 가지고 있다.
       
서버작업을 하고 성공했을경우 resolve를 실패했을때는 reject를 실행시키며 resolve는 then()에, reject는 catch() 연결된다.
       
이렇게 Promise를 이용하여 서버와 비동기 통신을 하는 라이브러리인 axios가 존재한다
       
axios.get().then().catch();
promise를 사용하기 때문에 동일하게 get이 성공하면 then을 실패하면 catch를 실행한다.       
    * async/await은 promise를 이용한 비동기 처리이다.
    
//서버통신은 비동기처리로 작성되었다.
      
````      
      async function test(){
      
         try{
         
            const test1 = await 서버통신;
         }
         catch{
         
            에러 발생시 작성할 코드
          }
          }
````
          
   async는 해당 기법을 적용시킬 함수에 위치시킨다.
       
await은 비동기처리 앞에 위치시킨다.(await을 적용시키면 예를들어 서버통신을 하여 반환한 값이 들어온 후에 test1에 할당한다.)
       
만약 await을 적용시키지 않으면 서버통신이 비동기 처리이기 때문에 test1에는 undefined가 할당된다.
       
예외처리는 promise와 비슷하게 .catch()가 아닌 try/catch 문으로 적용시키면 된다.
       
         
         
    
    
