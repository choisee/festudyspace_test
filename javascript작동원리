0. 들어가기
 - 자바스크립트의 특징
  = 단일 스레드 기반의 언어, 이러한 구동환경은 단일 호출 스택(call stack)을 사용함
  = 단일 스레드인데 여러 일을 어떻게 처리하는걸까? 어떻게 동시성(concurrency)를 지원하는걸까? -> 정답은 이벤트 루프 !!
   ex. 웹브라우저는 애니메이션 효과를 보여주면서 마우스 입력을 받아서 처리하고, Node.js 기반의 웹서버는 동시에 여러개의 HTTP요청을 처리
  = 실제 자바스크립트가 구동되는 환경(브라우저, Node.js등)에서는 주로 여러개의 스레드가 사용됨, 이러한 구동 환경이 단일 호출 스택을 사용하는 자바 스크립트 엔진과 상호 연동하기 위해 사용하는 장치가 바로 '이벤트 루프'
  * 단하나의 호출스택(call stack)을 사용 = 자바스트립트 함수가 실행되는 방식 = run to completion = 하나의 함수가 실행되면 이 함수의 실행이 끝날때까지는 다른 어떤 작업도 중간에 끼어들지 못한다는 의미
   (This differs from C, for instance, where if a function runs in a thread, it may be stopped at any point by the runtime system to run some other code in another thread.)

1. 웹엔진의 분류
 - javascript engine
  = javascript로 작성한 코드를 해석하고 실행하는 인터프리터
  * 인터프린터 vs 컨파일러  
   - interpreter의 경우 변환된 바이트 코드를 한줄씩 읽어나가며 동작을 수행
   - JITC의 경우 바이트 코드를 기반으로 전체를 native code로 컴파일하여 동작을 수행
 - rendering engine (layout engine)
  = HTML과 CSS로 작성된 마크업 코드를 웹페이지에 랜더링
 - V8과 같은 자바스크립트 엔진은 단일호출스택(Call Stack)을 사용 (비동기 요청 및 동시성에 대한 처리는 자바스크립트 엔진을 구동하는 환경인 브라우저나 Node.js가 담당)

2. javascript engine의 3가지 영역
 - call stack, task queue(event queue), heap
 - event loop
  = task queue에 들어가는 task 관리
  
3. 3가지 영역 상세
 - 자바스크립트에서 비동기로 호출되는 함수들은 call stack에 쌓이지 않고 task queue에 enqueue된다.
 ex.
 setTimeout(function(){
   console.log('1');
 },0); // 0ms
 console.log('2');
 
 위의 코드를 실행한 결과는 
 //1
 //2
 일것 같지만 setTimeout은 task queue에 쌓여서
 //2
 //1
 의 결과가 도출된다.
* 따라서 자바스크립트의 타이머는 정확한 타이밍을 보장해주지 않는다

 - 형태
  -----------------
  | S | H         |
  |   |           |
  |   |           |
  |   |           |
  |   |           |
  |   |           |
  |----------------
  | Q             |
  -----------------
S : Call stack = 요청이 들어오면 해당 요청을 순타적으로 스택에 담아서 처리, 메소드 실행시 call stack에 새로운 프레임이 생성 및 push되고 메소드의 실행이 끝나면 해당 프레임은 pop된다
(As always, calling a function creates a new stack frame for that function's use.)
H : Heap = 동적 생성된 객체 저장소
Q : Event queue = 비동기 함수가 적재되는곳 ( event loop이 돌다가 push된 항목 발견하면 pop해서 수행)

 - event loop
 while (queue.waitForMessage()) {
  queue.processNextMessage();
 }
 event queue에서 어떻게 event의 존재여부를 체크하는가 = 위의 코드참고 (처리해야할 이벤트(=태스크)를 파악하여 처리/작업을 수행한다)

4. 서로 다른 runtime간 통신
 - web worker나 cross-origin iframe은 각자의 스택, 힙, 메세지큐가 있다
  두개의 분리된 런타임은 postMessage를 통해서만 메세지 전달 가능



[참고]
https://trustyoo86.github.io/node.js/2017/11/17/javascript-v8-change-history.html
http://asfirstalways.tistory.com/362
https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop
https://github.com/nhnent/fe.javascript/wiki/June-13-June-17,-2016
https://vimeo.com/96425312
https://johnresig.com/blog/how-javascript-timers-work/