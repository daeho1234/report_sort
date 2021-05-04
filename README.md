# 정렬구현

---
– 목표 : 쉘정렬, 버블정렬, 선택정렬, 삽입정렬의 구현

​

##  버블정렬구현
​ 
* 이웃하는 숫자를 비교해 작은 수를 앞으로 이동시키는 과정을 반복한다.
```
public static void bubble_sort(int list[], int n) {
        int i, j, temp;
        for (i = n - 1; i > 0; i--) {
            for (j = 0; j < i; j++)
                if (list[j] > list[j + 1]) {
                    temp = list[j];
                    list[j] = list[j + 1];
                    list[j + 1] = temp;
                }
        }
        for (j = 0; j < n; j++)
            System.out.print(list[j] + " ");
    }
```
​  
1. bubble_sort를 다음과 같이 구현했습니다.(n : 사이즈)
2. for문을 이용해 반복하여 비교하고 비교된 내용 list[j]가 list[j+1]보다 크다면 서로 SWAP(temp를이용)되도록 하였습니다.

### 버블정렬결과

* 역순
1) 메인함수(리스트의 갯수는 30개입니다.)
![image](https://user-images.githubusercontent.com/80096249/116971506-a24ec100-acf4-11eb-943f-e0faccb27ca7.png)

2)결과
![image](https://user-images.githubusercontent.com/80096249/116971577-bd213580-acf4-11eb-8ffa-2a5ed6f7d989.png)

경과시간 : 6

* 정렬된 리스트(일부만 혼합)
1) 리스트
![image](https://user-images.githubusercontent.com/80096249/116972813-8ea45a00-acf6-11eb-83b4-e96622b24c28.png)

2)결과
![image](https://user-images.githubusercontent.com/80096249/116972889-a976ce80-acf6-11eb-81be-959d6d67a009.png)

경과시간 : 6 (시간의 차이가 없다)

## 삽입정렬의 구현
​ 
* 배열을 정렬된 부분과 정렬 안 된 부분으로 나누고, 정렬 안 된 부분의 원소를 적절한 위치에 삽입하여 정렬되도록 하는 과정을 반복한다.
```
public static void insertion_sort(int a[],int SIZE)
    {
        int i, j, key;
        for (i = 1; i < SIZE; i++)
        {
            key = a[i];
            for (j = i - 1; j >= 0 && a[j] > key; j--)
                a[j + 1] = a[j];
            a[j + 1] = key;
        }
        for (int l = 0; l < SIZE; l++)
            System.out.print(a[l] + " ");
    }
```
​ 
1. 정렬되지 않은 a[i]를 for문을 통해 정렬된 부분으로 만든다.

### 삽입정렬


---

​    

## 다익스트라 알고리즘 동작 과정

​    

![이미지](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcofnIo%2FbtqEuY3ZsSW%2FTnQX9kZ9RpyYtvElsrkMz1%2Fimg.gif)

​    

---

​    

## Shortest Path(G,v)   

​    

> + 입력: 가중치 그래프 G=(V,E), (V)=n, (E)=edge
>
> + 출력: 출발점 v로부터 (n-1)개의 점까지 각각 최단 거리를 저장한 배열 distance
>
> ---
>
> ​    
>
> 1. 배열 distance를 ∞로 초기화시킨다. 단, distance[v]=0으로 초기화한다.    
> 2. while (v로부터의 최단 거리가 확정되지 않은 점이 있으면)     
> 3. 현재까지 v로부터 최단 거리가 확정되지 않은 각 점 u에 대해서 최소의 distance[u]의 값을 가진 점 min_pos을 선택하고, 출발점 v로부터 점 min_pos까지의 최단 거리 distance[min_pos]을 확정한다.    
> 4. v로부터 현재보다 짧은 거리로 점 min_pos을 통해 우회 가능한 각 점 w에 대해서 distance[w]를 갱신한다.     
> 5. return distance

---

​    

## 시간 복잡도

​    

### while-루프가 (n-1)번 반복되고, 1회 반복될 때

> – 최소의 distance[u]를 가진 점 min_pos을 찾는데 O(n) 시간이 걸린다.
>
> – min_pos에 연결된 점의 수가 최대 (n-1)개이므로, 각 distance[w]를 갱신하는데 걸리는 시간은 O(n)이다.
>
> ![수식](https://user-images.githubusercontent.com/80369791/113504812-8a5d1380-9575-11eb-8523-7cd908f519db.gif)    

---

​    

## 소스코드


​    

### 시작 정점 방문 표시

```
distance[v] = 0;
visit[v] = true;
```

​    

### distance 초기값 저장

```
 for(int i = 0; i<g.n; i++) {
            if(!visit[i] && g.weight[v][i] !=0)
            {
                distance[i] = g.weight[v][i];
            }
        }
```

​    

### 모든 정점을 방문 하면서 최단 경로 찾기

```
for(int j = 0; j<g.n-1; j++){
            int min = Integer.MAX_VALUE;
            int min_pos = -1;

            //방문하지 않은 정점 중에서 최단 거리의 정점 고르기
            for(int i = 0; i<g.n; i++){
                if(distance[i] < min && !visit[i]){
                    min = distance[i]; // 최단 거리
                    min_pos = i; // 최단 거리의 인덱스(정점)
                }
            }

            visit[min_pos] = true; // 선택된 정점은 방문 표시해줌
            for(int i = 0; i<g.n; i++){
                if(!visit[i] && g.weight[min_pos][i]!=0) // 방문하지 않은 정점일 때만
                    if(distance[min_pos] + g.weight[min_pos][i] < distance[i]) // 선택된 정점을 통한 거리(distance 값)가 원래 거리보다 짧으면
                        distance[i] = distance[min_pos] + g.weight[min_pos][i]; // 인접 정점의 distance 값 업데이트
            }
        }
```

​    

### 최단 경로의 거리 출력

```
for(int i = 0; i<g.n; i++) {
            System.out.print(distance[i]+" ");
        }
```

​    

### Graph

```
private static class Graph {
        int n; // 정점의 개수
        int[][] weight; // 가중치
        public Graph(int n){
            this.n = n;
            weight = new int[n][n];
        }
        public void value(int i, int j, int w){
            weight[i][j] = w;
            weight[j][i] = w;
        }
    }
```

​    

### Main

```
public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        System.out.print("정점의 개수 : ");
        int n = scanner.nextInt();
        Graph g = new Graph(n);
        int edge = random.nextInt(5) + n;

        int num = 0;
        for(int i = 0; i<edge; i++) {
            int x = num;
            if(num>n-1){
                x = random.nextInt(n);
            }
            int y = random.nextInt(n);
            if(x == y){
                while(x==y){
                    y = random.nextInt(n);
                }
            }
            int z = random.nextInt(20) + 1;
            System.out.println(x+" "+y+" "+z);
            g.value(x,y,z);
            num++;
        }

        System.out.print("시작 정점 : ");
        int v = scanner.nextInt();
        dijkstra(g, v);
    }
```

​    

## 코드 설명

: 정점의 개수를 입력하면 그래프와 가중치를 랜덤으로 생성된다.    

시작 정점을 입력하면 최단 거리를 dijkstra함수를 통해 구한다.    

+ 입력 : 정점의 개수, 시작 정점    

- 출력 : 그래프, 최단 경로의 거리    

![4](https://user-images.githubusercontent.com/80369791/113506551-81be0a80-9580-11eb-914a-820578429d1b.png)![5](https://user-images.githubusercontent.com/80369791/113506555-82ef3780-9580-11eb-98b9-a71b38a44dd9.png)

---

​    

​    

## 실행시간 측정

- 실행 전 시간과 실행 후 시간의 차이

```java
long beforeTime = System.currentTimeMillis();
        dijkstra(g, v);
        System.out.println();
        long afterTime = System.currentTimeMillis();
        long secDiffTime = (afterTime - beforeTime);
        System.out.println("시간차이 : "+secDiffTime);
```

---


## 정점의 수에 따른 실행시간

​    

+ 정점의 개수를 10개 씩 늘릴 경우

  | 개수 | 10   | 20   | 30   | 40   | 50   | 60   | 70   | 80   | 90   | 100  |
  | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
  | 시간 | 5    | 6    | 7    | 7    | 8    | 9    | 9    | 11   | 12   | 15   |


![3](https://user-images.githubusercontent.com/80369791/113508652-2eea5000-958c-11eb-9185-31621dc8bbd6.png) 

+ 정점의 개수를 10의 n승 만큼 늘릴 경우

  | 개수 | 10   | 100  | 1000 | 10000 |
  | ---- | ---- | ---- | ---- | ----- |
  | 시간 | 5    | 10   | 48   | 1026  |

![2](https://user-images.githubusercontent.com/80369791/113506160-23902800-957e-11eb-8489-bdba6cdf68ba.png) 

+ 이론적으로 실행 시켰을 경우에 나오는 그래프

  ![6](https://user-images.githubusercontent.com/80369791/113508681-52ad9600-958c-11eb-9dcc-b5dc854ead87.png)    

  ​    

---

## 결론

다익스트라 (Dijkstra)의 최단 경로 알고리즘은 출발점으로부터 최단 거리가 확정되지 않은 점들 중에서 출발점으로부터 가장 가까운 점을 추가하고, 그 점의 최단 거리를 확정한다.     

시간복잡도는 O(n2)로 정점의 수가 늘어날수록 실행시간이 길어졌다.
