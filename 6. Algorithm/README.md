# Algorithm

## Sorting 

<br>

<table border="1">
  <tr>
    <th>알고리즘</th>
    <th>최선</th>
    <th>평균</th>
    <th>최악</th>
  </tr>
  <tr>
    <td>합병 정렬</td>
    <td>O(NlogN)</td>
    <td>O(NlogN)</td>
    <td>O(NlogN)</td>
  </tr>
  <tr>
    <td>힙 정렬</td>
    <td>O(NlogN)</td>
    <td>O(NlogN)</td>
    <td>O(NlogN)</td>
  </tr>
  <tr>
    <td>퀵 정렬</td>
    <td>O(NlogN)</td>
    <td>O(NlogN)</td>
    <td>O(N^2)</td>
  </tr>
  <tr>
    <td>삽입 정렬</td>
    <td>O(N)</td>
    <td>O(N^2)</td>
    <td>O(N^2)</td>
  </tr>
   <tr>
    <td>셸 정렬</td>
    <td>O(N)</td>
    <td>O(N^1.5)</td>
    <td>O(N^2)</td>
  </tr>
  <tr>
    <td>버블 정렬</td>
    <td>O(N^2)</td>
    <td>O(N^2)</td>
    <td>O(N^2)</td>
  </tr>
  <tr>
    <td>선택 정렬</td>
    <td>O(N^2)</td>
    <td>O(N^2)</td>
    <td>O(N^2)</td>
  </tr>
</table>

<br>
<hr>

## Merge Sort(합병 정렬)

<br>

`시간 복잡도: O(NlogN)`

**분할 정복을 통한 구현**

<br>

![합병 정렬](https://user-images.githubusercontent.com/55429912/119265683-861eaf80-bc22-11eb-81c8-da9a890a187d.png)

```C++
#define MAX_SIZE 8

int res[MAX_SIZE];

void merge(int* arr, int left, int mid, int right) {
  
    int i = left, j = mid + 1, k = left;
    
    while(i <= mid && j <= right) {
        if(arr[i] <= arr[j]) {
          res[k++] = arr[i++];
        }
        else{
          res[k++] = arr[j++];
        }
    }
    if(i > mid){  // 왼쪽 배열이 먼저 다 채워질 경우
        for(int idx = j; idx <= right; idx++) {
          res[k++] = data[idx];
        }
    }
    else {        // 오른쪽 배열이 먼저 다 채워질 경우
        for(int idx = i; idx <= mid; idx++) {
          res[k++] = data[idx];
        }
    }

    for(int idx = left; idx <= right; idx++) {
        arr[idx] = res[idx];
    }
}

void mergeSort(int* arr, int left, int right) {
    if(left < right) {
      int mid = (left + right) / 2;
      
      mergeSort(arr, left, mid);
      mergeSort(arr, mid + 1, right);
      merge(arr, left, mid, right);
    }
}

```
장점: 안정 정렬(동일한 값에 대해 기존의 순서가 유지), 빠른 시간 복잡도 

단점: 정렬된 배열을 담을 임시 배열이 하나 더 필요하다(메모리 공간을 배열크기만큼 더 사용)

<br>
<hr>

## Heap Sort(힙 정렬)

<br>

`시간 복잡도: O(NlogN)`

**힙 구조를 통한 구현(내림차순: 최대 힙, 오름차순: 최소 힙)**

<br>

![힙 정렬](https://user-images.githubusercontent.com/55429912/119266564-435ed680-bc26-11eb-940c-c00f5a515e8e.png)

```C++

```

장점: 추가적인 메모리 필요X, 빠른 시간 복잡도 

단점: 불안정 정렬