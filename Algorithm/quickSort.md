# 퀵 정렬  

## 소개  
대표적인 '분할 정복' 알고리즘으로 평균 속도가 O(N * logN)  

2 ^ 10 = 1,000  
2 ^ 20 = 1,000,000  
log2N -> N 이 1,000,000 일 때? 20 밖에 안되는 작은 숫자.  

O(N^)에 비해 굉장히 빠른 속도  
   
## 아이디어  
**_ 특정한 값을 기준으로 큰 숫자와 작은 숫자를 나누면 어떨까?_
   나누다 : 두 집합으로 나눈다.
   기준값(PIVOT)을 기준으로 두 그룹으로 나눈다.  
     
 ## 예시  
 3 7 8 1 5 9 6 10 2 4  
 일반적으로 가장 앞의 값을 기준값(PIVOT)으로 둔다.  
 예시에서도 가장 앞에 있는 3을 PIVOT 값으로 정했다.  
 
 왼쪽에서 오른쪽으로 이동하고, 오른쪽에서 왼쪽으로 이동한다.  
 
 왼쪽에서 오른쪽으로 이동할 때, PIVOT값 3 보다 큰 값을 선택  
 오른쪽에서 왼쪽으로 이동할 때, PIVOT값 3 보다 작은 값을 선택 한다.  
 
즉, 7과 2를 하나씩 선택한다. 이 때, 큰 값과 작은 값의 위치를 바꿔준다. -> 3 2 8 1 5 9 6 10 7 4  
왼쪽에서 3보다 큰 것 찾으면 8, 오른쪽에서 3보다 작은 걸 찾으면 1 - > 3 2 1 8 5 9 6 10 7 4  
왼쪽에서 3보다 큰 것 찾으면 8, 오른쪽에서 3보다 작은 걸 찾으면 1. 근데 여기에서 8과 1 이 엇갈림. 
즉, 작은 값 1의 인덱스가 큰 값 8의 인덱스보다 더 작은 경우 엇갈렸다 표현이 되며, 이런 상황에는 왼쪽에서 탐색!  
선택한 작은 값(여기서는 1)과 pivot을 비교하여 더 작은 값인 1을 pivot과 자리를 바꾼다. -> 1 2 3 8 5 9 6 10 7 4  
  
    
    
    
이 때, pivot 3의 왼쪽에는 3 보다 작은 값, 오른쪽에는 3 보다 큰 값이 위치되어 있다. 이렇게 분할이 이루어져 pivot값 3보다 큰 수의 집합, 작은 수의 집합으로 나뉘어진다.  
이제 여기에서 왼쪽 집합과 오른쪽 집합을 기준으로 반복하여 위 과정을 반복해 준다.  
  
왼쪽 집합에서는 가장 앞에 있는 값 1 이 pivot
오른쪽 집합에서는 가장 앞에 있는 값 8 이 pivot 값  

왼쪽 그룹의 pivot 1 같은 경우, 왼쪽에서 오른쪽으로 가며 pivot값 1 보다 큰 값인 2를 선택. 오른쪽에서 왼쪽으로 가며 pivot값 보다 작은 값을 찾는데, 없다.  이 경우에는, 자기 자신을 선택함.  
이 상태에서 엇갈렸기 때문에, 1과 자기자신 1을 바꾸기 때문에 1인 정렬이 된 것!  위 과정을 반복하면, 2가 pivot 값이 되고 결국 2도 자기 자신과 바꿔 정렬이 됨!
-> 1 2 3 8 5 9 6 10 7 4  

오른쪽 그룹에서 왼쪽에서 오른쪽으로 이동할 때, PIVOT값 8보다 큰 값 9 을 선택  
오른쪽에서 왼쪽으로 이동할 때, PIVOT값 3 보다 작은 값 4을 선택 한다. 엇갈리지 않았기 때문에 서로 자리를 바꿔줌 -> 1 2 3 8 5 4 6 10 7 9  
  
왼쪽에서 오른쪽으로 이동할 때, PIVOT값 8보다 큰 값 10 을 선택  
오른쪽에서 왼쪽으로 이동할 때, PIVOT값 3 보다 작은 값 7을 선택. 엇갈리지 않았기 때문에 서로 자리를 바꿔줌 - > 1 2 3 8 5 4 6 7 10 9  

왼쪽에서 오른쪽으로 이동할 때, PIVOT값 8보다 큰 값 10 을 선택  
오른쪽에서 왼쪽으로 이동할 때, PIVOT값 3 보다 작은 값 7을 선택. 엇갈리기 때문에 왼쪽에 있는 값과 pivot 8과 자리를 바꿔줌 -> 1 2 3 7 5 4 6 8 10 9  

이 때, 또 8을 기준으로 왼쪽에는 8 보다 작은 값, 오른 쪽에는 8 보다 큰 값이 모인 집합으로 분할 된다.  
  
그렇다면 왼쪽 그룹에서 pivot 값 7 로 잡고 위 과정을 반복해준다.  
이렇게 반복 반복 하다보면, 1 2 3 4 5 6 7 8 9 10 정렬이 이루어 진다.   
  
  
## 시간복잡도  
1 2 3 4 5 6 7 8 9 10을 정렬한다고 했을 때, 
O(N^2) 시간 복잡도를 가진다면, N ^ 2 = 10 * 10 = 100 번의 연산이 일어난다.  
  
그런데, 이것을 반으로 쪼개어  
1 2 3 4 5  -> 5 * 5 = 25 회 연산
6 7 8 9 10  -> 5 * 5 = 25 회 연산  
이 둘의 연산횟수는 총 50 회 이다.  

이러한 원리로 분할 정복 알고리즘인 퀵 정렬이 빠른 이유이다.
그렇게 때문에, 대용량 데이터를 정렬할 때, 퀵 정렬이 선택정렬이나 버블정렬 보다 훨씬 빠른 이유이다. 

평균 시간 복잡도는 O(N * logN) 이지만, 최악의 시간 복잡도는 O(N ^ 2) 이다. PIVOT값을 설정하는 경우에 따라 다르다.  
이미 정렬이 되어 있는 경우를 예시로 들자.  
1 2 3 4 5 6 7 8 9 10  
1 에서 시작해서 2 부터 10 까지 왼쪽에서 오른쪽으로 이동하며 작은 값을 찾고, 오른쪽에서 왼쪽으로 큰 값을 찾는다. -> 1 2 3 4 5 6 7 8 9 10 로, 1 하나만 정렬된다.
2 에서 시작해서 3부터 10 까지 왼쪽에서 오른쪽으로 이동하며 작은 값, 큰 값을 찾아 1 2 3 4 5 6 7 8 9 10 로 2 하나만 정렬이 된다.

일반적으로 가장 빠르게 정렬이 이루어 지려면 중간에 있는 값을 기준으로 왼쪽, 오른쪽 그룹의 연산이 이루어져야 하는데,  
이렇게 되면, 연산이 10, 9, 8, 7, 6, .... 번으로 O(N^2)의 시간복잡도를 가지게 되는 것이다.

그래서 항상 N log N을 보장하지는 않는다. 그래도 대부분 경우 빠르기 때문에 많은 사랑을 받고 있다. 데이터의 특징에 따라 정렬을 선택해서 사용하면 된다.
  
  
## C언어로 퀵정렬 오름차순 구현   
```C
#include <stdio.h>  

int number = 10;
int data[10] = {1, 10 , 5, 8, 7, 6, 4, 3, 2, 9}

// start는 특정 부분집합의 첫 번째 값, end는 마지막 값
void quickSort(int *data, int start, int end){
  // 원소가 1개인 경우
  if (start >= end) {
    return;
  }
  
  int key = start; // 첫번째 원소
  
  // i 왼쪽 부터 하나씩 큰 값을 찾을 때의 인덱스. 기본적으로 키값의 오른쪽에 위치함. 그리고 오른쪽으로 점점 이동하며 탐색하며 큰 값을 찾아야 하기 때문에 start 에 + i 값을 준다.
  int i = start + i; 
  //오른쪽에서 왼쪽으로 출발 할 때, 오른쪽의 출발지점이 된다.
  int j = end; 
  
  int temp; // 위치 바꾸는 임시변수
  
  while( i <= j ) { // 엇갈릴 때 까지 반복. 왼쪽부터 출발한 것이 오른쪽부터 출발한 값보다 작거나 같을 때 까지만 반복
    while(data[i] <= data[key]){ // 키 값 보다 큰 값을 만날 때 까지 오른쪽으로 이동
      // 기본 적으로 항상 퀵 정렬은 큰 값과 작은 값을 바꾸며, 바꾼 후에는 왼쪽에 있는 값과 pivot 값을 바꾸는 것. 
      // 단순히 큰 값을 찾는 위치와 작은 값을 찾는 위치를 바꾸면 내림차순정렬을 할 수 있다.
      // data[i] >= data[key] 내림차순 정렬 
      i++;
    }
    while(data[j] >= data[key] && j > start){ 
    // data[j] <= data[key] && j > start 내림차순 정렬 시  
    // 키 값보다 작은 값을 만날 때 까지 왼쪽으로 이동 && 1 10 5 8 7 6 4 3 2 9 에서 1보다 작은 값을 고른다고 할 때, 없다. 
    // -1 .... 검색하면 안되개 때문에
    // 최대한 커봤자 start인 10 까지만 탐색하도록 범위를 정해 준 것
    // 엇갈렸을 때 교체를 하는데, 왼쪽에 있는 값과 pivot 값을 교체 해 주기 때문에 왼쪽으로만 넘어가지 않도록 해주면 되기 때문에 오른쪽에는 범위를 지정해주지 않음    
      j--;
    }
    
    if(i > j){ //현재 엇갈린 상태면 키 값과 교체하도록 한다.
      temp = data[j];
      data[j] = data[i];
      data[key] = temp;
    } else { // 엇갈리지 않은 상태라면 서로 교체하도록 한다.
      temp = data[j];
      data[j] = data[i];
      data[i] = temp;   
    }
  }
  
  // 서로 엇갈려 밖으로 빠져 나왔을 떄
  // 그 키 값을 기준으로 왼쪽(pivot보다 작은 값 집합)과 오른쪽(pivot보다 큰 값 집합)에서 각각 다시 큌 정렬을 수행
  quickSort(data, start, j - 1);
  quickSort(data. j + 1, end);
}

```