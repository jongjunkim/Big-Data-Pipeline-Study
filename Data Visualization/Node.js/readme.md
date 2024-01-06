
# Data Visualization

- Data visualization can help deliver data efficiently.
- It presents data to facilitate reaching conclusions.
- It affects an organization's decision-making process.

# Node.js

- Built on Chrome’s JavaScript runtime for easily building fast applications.
- Spring Boot requires more initial configuration and setup compared to Node.js.
- Node.js uses an event-driven, non-blocking I/O model, making it lightweight and efficient.

# HTTP

- Designed to enable communications between clients and servers.
- The client (browser) sends an HTTP request to the server, and the server returns a response to the client.

# MVC Pattern (Model-View-Controller)

- Model-view-controller 약자, 소프트웨어 디자인 패턴중 하나. 이 패턴은 소프트웨어를 세가지 주요 구성 요소로 나누어 관리함으로써 소프트웨어의 유지보수성과 확장성을 향상시키기위한 목적
- Divides software into three main components to enhance maintainability and scalability.
- Model (모델):
  - 데이터의 상태를 유지하고 데이터에 대한 조작, 처리, 유효성 검사 등의 작업을 수행
  - 사용자 인터페이스나 뷰와는 독립적으로 존재하며, 데이터의 변경에 대한 알림을 처리
- View (뷰):
  - 사용자의 인터페이스를 나타내며, 모델의 데이터를 시각적으로 표현
  - 모델의 데이터를 직접 수정하지 않고, 모델로부터 데이터를 읽어와서 표시
- Controller:
  - 사용자의 입력 및 이벤트에 응답하여 모델의 상태를 변경 업데이트
  - 모델과 뷰 간의 상호 작용을 관리하고, 사용자의 액션에 따라 어떤 로직을 실행할지 제어

# Synchronous vs. Asynchronous

- Synchronous:
  - 동기식은 순차적인 실행을 의미합니다. 하나의 작업이 끝나야 다음 작업이 시작됩니다
  - 일반적으로 동기식 코드는 간단하고 직관적이지만, 작업이 끝날 때까지 대기해야 하므로 시간이 오래 걸릴 수 있습니다.
- Asynchronous:
  - 비동기식은 작업이 순차적으로 실행되지 않고, 작업이 완료될 때까지 기다리지 않습니다
  - 비동기식 코드는 여러 작업을 동시에 수행할 수 있어서 대규모 애플리케이션에서 유용합니다.

# Event-driven

- 이벤트가 발생할 때 미리 지정해둔 작업을 수행

# NPM and Express

- NPM is an online repository for publishing open-source Node.js packages.
- Express is a Node.js web application framework.

# Event-driven Programming in Node.js

"Event-driven" is a crucial characteristic of Node.js, signifying its adoption of an event-driven and asynchronous programming model.

## Event-driven Architecture

In event-driven programming, a program responds to specific events. Events can include user input, completion of file loading, network requests, and other occurrences in the system. In Node.js, listeners are registered for these events, and when an event occurs, pre-registered callback functions execute to handle the event.

## Asynchronous I/O in Node.js

Node.js supports asynchronous I/O, allowing multiple tasks to be processed simultaneously. This concurrent handling of multiple requests helps enhance performance by preventing blocking.

## Single-threaded and Event Loop

Node.js operates on a single thread through an event loop, allowing it to asynchronously handle multiple tasks. This design efficiently responds to numerous user requests.

## Non-blocking I/O

Node.js는 입출력 작업이 완료될 때까지 대기하지 않고 다른 작업을 수행할 수 있도록 하는 비차단(non-blocking) 입출력 모델을 채택

## Advantages of Event-driven Architecture

- Asynchronous nature and performance: 이벤트 기반 아키텍처는 비동기적인 처리를 지원하며, 이는 여러 작업을 동시에 처리할 수 있게 하고, 대기 시간을 최소화하여 높은 성능을 제공 특히 네트워크 요청, 파일 I/O 등과 같은 비동기 작업에서 효과적
- Scalability(확장성): 이벤트 기반 시스템은 이벤트가 발생할 때마다 콜백 함수를 실행하므로, 여러 이벤트에 대한 감지 및 응답이 가능하며, 시스템이 더욱 확장 가능하게 됩니다.
## Drawbacks of Event-driven Architecture

- Callback Hell: 콜백 함수를 중첩해서 사용할 때 코드가 복잡해지고 가독성이 떨어질 수 있는 콜백 지옥 문제가 발생할 수 있습니다
- Debugging Challenges: 비동기적인 특성으로 인해 코드의 실행 순서가 예측하기 어려울 수 있고, 디버깅이 어려울 수 있습니다.

# 실습

- Node js 설치
  - ```ubuntu curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash – ```
- Express 설치
  - ```ubuntu sudo npm install –g express ```
  - express . -> app.js  bin  package.json  public  routes  views 생성
  - app.js 파일 가서 아래와 같이 써주면됨




