
# BackPressure란?

> Resistance or force opposing the desired flow of data through software.

 소프트웨어의 목적은 입력 데이터를 받아서, 원하는 결과로 변경하는 것이다. 이때, 그 결과는 JSON 형식의 API일 수도 있고,
 웹페이지를 위한 HTML, 혹은 모니터에 투사되는 픽셀일 수도 있다.

 BackPressure란, 그 입력을 결과로 바꾸는 과정에서 저항하는 것이다. 대부분의 경우, 
 저항(resistance)란 연산 속도-입력이 들어오는 속도만큼 그 처리가 느린 문제-이며, 이것이 가장 쉬운 비유일 것이다.

 물론, 다른 형태의 backpressure 또한 발생할 수 있다. 예를 들어, 당신의 어플리케이션이 유저의 행동(action)을 기다리고 있다고 해보자.

>By the way, you might eventually hear someone use the word “backpressure” to actually mean something has the ability to control or handle backpressure.
>For example, if someone says: “I made this new library with built-in backpressure…” they probably mean it somehow helps you manage backpressure,
>not that it actually intrinsically is the cause of it.
>
>Backpressure is not “desirable” except when it’s inescapable and you want to protect something else from receiving it.

그러나 아직 backpressure가 정확히 무엇을 의미하는지 아직까지는 애매한 부분이 있다.
다음의 예시를 보도록 하자.

## Examples of Backpressure

>I Love Lucy: Chocolate Factory
>Let’s start with an analogy. In the 50s television show “I Love Lucy” there’s an episode in which Lucy is working at a candy packaging plant.
>Her job is to take candy from a conveyor belt and wrap each of them in paper. Easy enough, except she quickly finds the conveyor’s speed is faster than she can handle.
>Hilarity ensues.This is a perfect example of backpressure. She actually tries two different ways of dealing with it: setting some aside to get to later (buffering), and eventually she starts eating and hiding them in her hat (dropping).
>However, in the case of a chocolate factory, neither of these backpressure strategies are viable.
>Instead, she needed them to slow down the conveyor; in other words, she needs to be able to control the producer’s speed. We’ll talk more about strategies in a bit!


# Backpressure Strategies

 너의 컴퓨팅 자원을 scale up 하는 것 외의, 이러한 back pressure를 다룰 수 있는 전략은 크게
 세 가지 옵션으로 점철될 수 있다.

 1. Producer를 조절한다.
 3. 들어오는 데이터를 buffering한다.
 4. 일부 데이터를 Drop한다.
 5. backpressure를 무시한다. 

  # 1. Producer를 조절한다.

   가장 좋은 옵션일 수 있지만, 이를 구현하기 위하여 코드의 복잡성이 추가된다. 
   또한 사용자의 클릭과 같은 조절하지 못하는 경우도 있다.

  # 2. 들어오는 데이터를 Buffering한다.

   좋은 방법이지만, 추가적인 코드의 추가가 필요하고, 무한한(unbounded) 경우 oom의 위험이 있다.

  # 3. Droping

   시스템이 완전히 fail over하는 것보다는 적당히 데이터를 drop하는 것이 더 유리하다.

   

(https://medium.com/@jayphelps/backpressure-explained-the-flow-of-data-through-software-2350b3e77ce7)




