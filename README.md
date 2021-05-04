# 정렬구현

---
– 목표 : 쉘정렬, 버블정렬, 선택정렬, 삽입정렬의 구현


##  버블정렬구현

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
![image](https://user-images.githubusercontent.com/80096249/116982153-6a02af00-ad03-11eb-805e-61669472a1d3.png)

2)결과

![image](https://user-images.githubusercontent.com/80096249/116972889-a976ce80-acf6-11eb-81be-959d6d67a009.png)

경과시간 : 6 (시간의 차이가 없다)

## 삽입정렬구현

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

1. 정렬되지 않은 a[i]를 for문을 거쳐 정렬된 부분으로 만든다.

### 삽입정렬결과

* 역순
1) 메인함수(리스트의 갯수는 1000개입니다.)
![image](https://user-images.githubusercontent.com/80096249/117010724-08a10700-ad28-11eb-9f6b-ab627e7cafe3.png)

2) 결과

![image](https://user-images.githubusercontent.com/80096249/117010805-24a4a880-ad28-11eb-9ff7-d193d7cba043.png)

경과시간 : 14 (뒷부분도 모두 정상 정렬되었습니다.)

* 정렬된 리스트(일부만 혼합)

1) 리스트

![image](https://user-images.githubusercontent.com/80096249/117011160-8402b880-ad28-11eb-9ca8-491aedce40f5.png)

2)결과

![image](https://user-images.githubusercontent.com/80096249/117011085-6fbebb80-ad28-11eb-8bbf-05466c064167.png)

경과시간 : 14 (뒷부분도 모두 정상 정렬되었습니다.)

##  선택정렬구현

* 입력 배열 전체에서 최소값을 선택하여 배열의 0번 원소와 자리를 바꾸고, 다음엔 0번 원소를 제외한 나머지 원소에서 최솟값을 선택하여, 배열의 1번 원소와 자리를 바꾼다.

```
 public static void selection_sort(int a[],int SIZE)
    {
        int least, temp;
        for (int i = 0; i < SIZE - 1; i++)
        {
            least = i;
            for (int j = i + 1; j < SIZE; j++)
                if (a[j] < a[least])
                    least = j;
            temp = a[i];
            a[i] = a[least];
            a[least] = temp;
        }
        for (int j = 0; j < 15; j++)
            System.out.print(a[j] + " ");
        System.out.println("");
    }
```

1. least를 이용해 최솟값을 얻어 자리를 바꾼다.

### 선택정렬결과

* 역순
1) 메인함수(리스트의 갯수는 1000개입니다.)
![image](https://user-images.githubusercontent.com/80096249/116982106-5bb49300-ad03-11eb-8e46-d6709078f6d8.png)

2)결과

![image](https://user-images.githubusercontent.com/80096249/116981745-e779ef80-ad02-11eb-9496-a81429b0c4c9.png)

경과시간 : 18 (뒤도 모두 정상정렬되었습니다)

* 정렬된 리스트(일부만 혼합)

1) 리스트

![image](https://user-images.githubusercontent.com/80096249/116982122-60794700-ad03-11eb-9233-a22a014f8dc8.png)

2)결과

![image](https://user-images.githubusercontent.com/80096249/117010308-a34d1600-ad27-11eb-9677-bc69b723e021.png)

경과시간 : 18 (시간의 차이가 없다) (뒤도 모두 정상정렬되었습니다)

##  쉘정렬구현

* 버블정렬과 삽입정렬을 모두 이용해 단점을 보완한 정렬
```
public static void inc_insertion_sort(int[] list, int first, int last, int gap)
    {
        int i, j, key;
        for (i = first + gap; i <= last; i = i + gap)
        {
            key = list[i];
            for (j = i - gap; j >= first && list[j] > key;j=j-gap)
                list[j + gap] = list[j];
            list[j + gap] = key;
        }
    }

    public static void Shell_sort(int[] list, int n)
    {
        int i,gap;
        for (gap = n / 2; gap > 0; gap = gap / 2)
        {
            if (gap % 2 == 0)
                gap++;
            for (i = 0; i < gap; i++)
                inc_insertion_sort(list, i, n - 1, gap);
        }
    }
```
1.삽입정렬과 버블정렬을 모두이용해 구현

### 쉘정렬결과

* 역순
1) 메인함수(리스트의 갯수는 30개입니다.)
![image](https://user-images.githubusercontent.com/80096249/116980930-d54b8180-ad01-11eb-8d47-7dd7144f6b6b.png)

2)결과

![image](https://user-images.githubusercontent.com/80096249/116980960-de3c5300-ad01-11eb-95d9-6a860d2113f5.png)

경과시간 : 6

* 정렬된 리스트(일부만 혼합)
1) 리스트
![image](https://user-images.githubusercontent.com/80096249/116972813-8ea45a00-acf6-11eb-83b4-e96622b24c28.png)

2)결과

![image](https://user-images.githubusercontent.com/80096249/116972889-a976ce80-acf6-11eb-81be-959d6d67a009.png)

경과시간 : 6 (시간의 차이가 없다)



## 결론

다익스트라 (Dijkstra)의 최단 경로 알고리즘은 출발점으로부터 최단 거리가 확정되지 않은 점들 중에서 출발점으로부터 가장 가까운 점을 추가하고, 그 점의 최단 거리를 확정한다.     

시간복잡도는 O(n2)로 정점의 수가 늘어날수록 실행시간이 길어졌다.
