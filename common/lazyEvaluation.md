# What is LazyEvaluation?

> In programming language theory, lazy evaluation, or call-by-need,[1] is an evaluation strategy which delays the evaluation of an expression until its value is needed
> (https://en.wikipedia.org/wiki/Lazy_evaluation)

LazyEvaluation이란, 말 그대로, 표현(expression)이 실제로 사용되기 전까지 실행을 미루는 것을 의미한다. 이는 eager evaluation와는 정반대의 의미이며, 주로 함수형 언어에서 사용되는 개념이다.
LazyEvaluation을 통하여 무한한 데이터 스트림을 처리하거나, 불필요한 연산을 줄일 수 있으며, 경우에 따라선 메모이제이션을 통하여 연산의 횟수를 줄일 수도 있다.

```

final List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
 
System.out.println(
    list.stream()
        .filter(i -> {
            System.out.println("i < 6");
            return i<6;
        })
        .filter(i -> {
            System.out.println("i%2 == 0");
            return i%2==0;
        })
        .map(i -> {
            System.out.println("i = i*10");
            return i*10;
        })
        .collect(Collectors.toList())
);

```

```
i < 6
i%2 == 0
i < 6
i%2 == 0
i = i*10
i < 6
i%2 == 0
i < 6
i%2 == 0
i = i*10
i < 6
i%2 == 0
i < 6
i < 6
i < 6
i < 6
i < 6
[20, 40]
```
(https://dororongju.tistory.com/137)

위 코드에서 i가 6보다 큰 경우, 첫 번째 필터 함수에서 걸러진 이후에는 그 다음 필터와 맵 함수를 거치지 않는데,
이는 LazyEvalutation을 통하여 불필요한 함수의 연산을 줄일 수 있다는 것을 알 수 있다. 위 코드의 경우 코드가 단순하여 문제가 되지 않으나,
만약 실행 시간이 긴 함수라면 LazyEvalutaion을 통하여 많은 자원을 절약할 수 있다.

```

total = 0
for i in range(10000000): <!-- 이미 이곳에서 길이가 10000000인 배열을 생성해버리기 때문에 메모리 사용량이 그만큼 증가한다. -->
    total += i
print total

```

그러나 위 코드에서 range 부분을 lazyEvaluation을 사용하는 함수로 변경할 경우, 값이 필요할 때마다 만들기 때문에 메모리 사용량이 줄어든다.
(https://stackoverflow.com/questions/265392/why-is-lazy-evaluation-useful?rq=1)

