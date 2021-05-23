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

**힙(완전 이진트리 형태의 자료구조) 구조를 통한 구현(내림차순: 최대 힙, 오름차순: 최소 힙)**

<br>

![힙 정렬](https://user-images.githubusercontent.com/55429912/119266564-435ed680-bc26-11eb-940c-c00f5a515e8e.png)

```C++
void heapify(int* arr, int len, int i) {
    int parent = i;
    int leftChild = i * 2 + 1;  
    int rightChild = i * 2 + 2;
    
    // 왼쪽 자식 노드와 부모 노드를 비교하여 큰 값을 부모 노드로 올린다.
    if (l < n && arr[p] < arr[l]) p = l;

    // 오른쪽 자식 노드와 부모 노드를 비교하여 큰 값을 부모 노드로 올린다.
    if (r < n && arr[p] < arr[r]) p = r;

    // 부모 노드를 가리키는 p 값이 바뀌면 위치를 교환하고
    // heapify()를 호출하여 과정을 반복한다.
    if (i != p) {
        swap(arr, p, i);
        heapify(arr, len, parent);
    }
}

void heapSort(int* arr) {
    int len = arr.length();

    // heap 초기화
    for(int i = (len / 2) - 1; i >= 0; i--){
        heapify(arr, len, i);
    }
    for(int i = len - 1; i > 0; i--) {
        swap(arr, 0, i);  
        heapify(arr, i, 0);
    }
}
```

장점: 추가적인 메모리 필요X, 빠른 시간 복잡도 

단점: 불안정 정렬

<br>
<hr>

## Quick Sort(퀵 정렬)

<br>

`시간 복잡도: 평균: O(NlogN), 최악: O(N^2)`

**분할 정복을 통한 구현(합병 정렬과 달리 퀵 정렬은 비균등하게 분할)**

1. pivot을 선정
  
2. pivot을 기준으로 pivot보다 작은 요소들은 모두 pivot의 왼쪽, 큰 요소들은 오른쪽으로 이동

3. pivot을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬

4. 부분 리스트들이 더이상 분할이 불가능할 때까지 반복

<br>

![퀵 정렬](https://user-images.githubusercontent.com/55429912/119268416-d18a8b00-bc2d-11eb-8c34-bceab99f6b6c.png)

```C++
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

void quickSort(int left, int right) {
    if(left >= right) return;
    int pivot = left, start = left + 1, end = right;

    while(start <= end) {
        while(arr[pivot] >= arr[start] && start <= right) start++;
        while(arr[pivot] <= arr[end] && end > left) end--;
        if(s > e) {
            swap(arr[pivot], arr[end]);
        }
        else {
            swap(arr[start], arr[end]);
        }
    }

    quickSort(left, end - 1);
    quickSort(end + 1, right);
}
```

장점: 추가적인 메모리 필요X, 빠른 시간 복잡도(다른 O(NlogN)의 시간 복잡도를 가지는 정렬 알고리즘에 보다 빠름)

단점: 최악의 경우(이미 정렬 되어있는 경우, 리스트가 계속 불균형하게 나누어지는 경우) 시간 복잡도는 O(N^2), 불안정 정렬

<br>
<hr>

## Insertion Sort(삽입 정렬)

<br>

`시간 복잡도: 최선: O(N), 평균: O(N^2), 최악: O(N^2)`

<br>

![삽입 정렬](https://user-images.githubusercontent.com/55429912/119269333-229c7e00-bc32-11eb-927b-242e29978717.png)

```C++
#define MAX_SIZE 5
int arr[MAX_SIZE] = {8, 5, 6, 2, 4};

void insertionSort() {
    for(int i = 1; i < MAX_SIZE; i++) {
        int key = arr[i], j;

        for(j = i - 1; j >= 0; j--) {
            if(key >= arr[j]) break;
            arr[j + 1] = arr[j]; 
        }
        arr[j + 1] = key;
    }
}
```

장점: 최선의 경우(이미 정렬되어 있는 경우) O(N), 안정 정렬

단점: 최악의 경우 O(N^2)

<br>
<hr>

## Shell Sort(셸 정렬)

<br>

<br>
<hr>

## Bubble Sort(버블 정렬)

<br>

<br>
<hr>

## Selection Sort(선택 정렬)

<br>