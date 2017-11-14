---
layout: post
title:  "[Problem Solving] getting started"
subtitle:   "[Problem Solving] getting started"
categories: book
tags: problem_solving
---



## 0.1 최대와 최소

``` c
int min(int x, int y){
  if(x < y)
    return x;
  return y;
}

int max(int x, int y){
  if(x > y)
    return x;
  return y;
}
```

위의 함수를 매크로(macro) 함수로 작성하면,

```c
#define max(x, y)((x)>(y)?(x):(y))
#define min(x, y)((x)<(y)?(x):(y))
```

매크로 함수는 보통 함수와는 다르게 컴파일을 하기 전에 코드 자체를 바꿈

* max(3, 2)는 ((3)>(2)?(3):(2)) 로 바뀌어 컴파일 됨 

매크로 함수를 사용하면 함수를 호출하는 시간(매우 짧음)이 없다는 점이 좋음

근데, 찾아내기 힘든 버그가 생길 수 도 있음 
