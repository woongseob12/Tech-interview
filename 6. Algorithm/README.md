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
void partition(int l, int r) {
	if (l < r) {						    // 최소 단위로 분할 할 수 있다면
		int mid = (l + r) / 2;		        // 중간값 구하기
		partition(l, mid);			        // 왼쪽
		partition(mid + 1, r);		        // 오른쪽
		merge(l, r);					    // 합치기
	}
}

void merge(int l, int r) {
	int mid = (l + r) / 2;
	int i = l, j = mid + 1, k = l;
	while (i <= mid && j <= r) {		    // 왼쪽값이 다 채워지거나, 오른쪽 값이 다 채워질 때 까지
		if (arr[i] <= arr[j]) {		        // 왼쪽 값이 더 작다면
			res[k++] = arr[i++];		    // 왼쪽 값을 넣어주고
		}
		else {  						    // 오른쪽 값이 더 작다면
			res[k++] = arr[j++];		    // 오른쪽 값을 넣어주고
		}
	}

	int temp = i > mid ? j : i;	    	    // 못채워 넣은 곳은 어딘지
	while (k <= r) {
		res[k++] = arr[temp++];	        	// 못채워 넣은 곳 채워 넣기
	}

	for (int idx = l; idx <= r; idx++) {	// 복사해주기
		arr[idx] = res[idx];
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
void quickSort(int l, int r) {
	if (l >= r) return;											// 최소 단위일 경우 처리하지 않고 반환
	int pivot = l, start = l + 1, end = r;						// 가장 왼쪽 값을 피벗으로 설정
	while (start <= end) {										// 시작포인터와 끝포인터가 교차하지 않을때 까지 반복
		while (start <= r && arr[pivot] >= arr[start]) start++;	// 유효한 범위이면서 피봇보다 작거나 같은 값으로 제대로 정렬되있다면
		while (end > l && arr[pivot] <= arr[end]) end--;		// 유효한 범위이면서 피봇보다 크거나 같은 값으로 제대로 정렬되있다면
		if (start > end) {										// 두 포인터가 교차 되었다면
			swap(arr[pivot], arr[end]);							// 피봇과 끝값을 교체
		}
		else {													// 큰 값과 작은 값이 정렬되어 있지 않은 상태라면
			swap(arr[start], arr[end]);							// 큰 값과 작은 값이 올바른 위치로 가도록 교체
		}
	}

	quickSort(l, end - 1);										// 피봇 제외한 왼쪽
	quickSort(end + 1, r);										// 피봇을 제외한 오른쪽
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
void insertionSort() {
	int len = sizeof(arr) / sizeof(arr[0]), i, j;
	for (i = 1; i < len; i++) {			    // 두번째 부터 비교 시작
		int key = arr[i];
		for (j = i - 1; j >= 0; j--) {	    // 앞의 원소들과 비교
			if (arr[j] <= key) break;		// 앞이 값이 더 작다면 탐색 중단(오름차순 기준)
			arr[j + 1] = arr[j];			// 값 1칸씩 밀어주기
		}
		arr[j + 1] = key;					// 들어갈 공간을 찾아서 삽입
	}
}
```

장점: 최선의 경우(이미 정렬되어 있는 경우) O(N), 안정 정렬

단점: 최악의 경우 O(N^2)

<br>
<hr>

## Bubble Sort(버블 정렬)

<br>

`시간 복잡도: O(N^2)`

<br>

![버블 정렬](https://user-images.githubusercontent.com/55429912/119269868-d0a92780-bc34-11eb-9418-705c0fdf02bf.png)

```C++
void bubbleSort() {
	int len = sizeof(arr) / sizeof(arr[0]);
	for (int i = len - 1; i > 0; i--) {		    // 끝부터 채워 나가기
		for (int j = 0; j < i; j++) {			// 채워진 부분을 제외하고 앞부분 진행하기
			if (arr[j] > arr[j + 1]) {		    // 앞의 값이 더 클 경우 교체(오름차순)
				swap(arr[j], arr[j + 1]);
			}
		}
	}
}
```

장점: 구현 용이, 코드가 직관적

단점: O(N^2)의 시간복잡도

<br>
<hr>

## Selection Sort(선택 정렬)

<br>

`시간 복잡도: O(N^2)`

<br>

![선택 정렬](https://user-images.githubusercontent.com/55429912/119270338-2aaaec80-bc37-11eb-9c10-9b35b28737f9.png)

```C++
void selectionSort() {
	int len = sizeof(arr) / sizeof(arr[0]);
	for (int i = 0; i < len - 1; i++) {		    // 순회
		int min = i;							// 최소값 설정
		for (int j = i + 1; j < len; j++) {
			if (arr[min] > arr[j]) {			// 최소값 갱신
				min = j;
			}
		}
		if (min != i) {
			swap(arr[min], arr[i]);			    // 최소값 교체
		}
	}
}
```

장점: 정렬을 위한 비교 횟수는 많으나 교환 횟수가 적어 역순 정렬에 효과적

단점: 정렬을 위한 비교횟수가 많아서 이미 정렬된 상태에서 소수의 자료가 추가되면 재정렬시 최악의 처리속도

<br>
<hr>

## Binary Search(이진 탐색)

<br>

`시간 복잡도: O(logN)`

**반복 또는 재귀로 구현**

<br>

![이진 탐색](https://user-images.githubusercontent.com/55429912/119336229-5de98c00-bcc8-11eb-9621-8caa78cf2ca9.png)

```C++
#define MAX_SIZE 7
int val = 6;
int arr[MAX_SIZE] = {9, 7, 6, 4, 3, 2, 1};

int BinarySearch() {
    int s = 0, e = MAX_SIZE - 1;

    while(s <= e) {
        int mid = (s + e) / 2;

        if(arr[mid] == val) {
            return mid;
        }
        else if(arr[mid] < val) {
            e = mid - 1;
        }
        else{
            s = mid + 1;
        }
    }
    return -1;
}
```

장점: 빠른 시간복잡도 O(logN)

단점: 배열이 이미 정렬되어 있어야함

<br>
<hr>

## DFS(깊이 우선 탐색)

<br>

`시간 복잡도: 인접 행렬: O(V^2), 인접 리스트: O(V + E)`

`V는 노드, E는 간선`

**스택 or 재귀를 통해 구현**

![DFS](https://user-images.githubusercontent.com/55429912/119339590-4ca27e80-bccc-11eb-91ac-75c3452161c3.png)

```C++
void dfs(int curr) {
    visit[curr] = true;

    for(int i = 0; i < graph[curr].size(); i++) {
        int next = graph[curr][i];
        if(!visit[next]){
            dfs(next);
        }
    }
}
```

장점: 현 경로상의 노드들만 기억하면 되므로 저장 공간의 수요가 비교적 적음

단점: 얻어지는 해가 최단 경로가 된다는 보장이 없다.

<br>
<hr>

## BFS(너비 우선 탐색)

<br>

`시간 복잡도: 인접 행렬: O(V^2), 인접 리스트: O(V + E)`

`V는 노드, E는 간선`

**큐를 통해 구현**

![BFS](https://user-images.githubusercontent.com/55429912/119339896-ba4eaa80-bccc-11eb-8deb-2f524851051f.png)

```C++
void bfs(int node) {
    queue<int> q;
    q.push(node);
    visit[node] = true;

    while(!q.empty()) {
        int curr = q.front();
        q.pop();

        for(int i = 0; i < graph[curr].size(); i++){
            int next = graph[curr][i];
            if(!visit[next]) {
                visit[next] = true;
                q.push(next);
            }
        }
    }
}
```

장점: 답이 여러개인 경우에도 최단 경로임을 보장

단점: 큐를 이용하여 다음 탐색 노드를 저장하기 때문에 노드의 수가 많을수록 불필요한 노드까지 저장

<br>
<hr>

## Dijkstra(다익스트라)

<br>

**최단 경로 알고리즘**

기본 로직: 첫 정점을 기준으로 연결되어 있는 정점들을 추가해가며, 최단 거리를 갱신하는 것

모든 노드를 각각 비교하는 선형탐색의 경우 시간복잡도는 `O(V^2)`

힙구조로 구현시 시간 복잡도는 `O((V + E)logV)`

V는 노드, E는 간선

- 각 노드마다 미방문 노드중 출발점~ 현재까지 계산된 최단거리를 가지는 노드를 찾는데 `O(VlogV)`의 시간이 필요
  - 모든 노드 O(V)에 대해 힙에서 최소값을 추출O(logV)
- 각 노드마다 이웃한 노드의 최단거리를 갱신하는데 `O(ElogV)`의 시간이 필요
  - 각 노드마다 모든 이웃을 확인하는 것은 모든 Edge를 확인하는 것과 같고 O(E), 매번 힙에서 최단거리를 갱신해야 하기 때문에 O(logV)

**우선순위큐를 이용하여 구현**

![Dijkstra](https://user-images.githubusercontent.com/55429912/119345274-a0649600-bcd3-11eb-9f1b-d689d592c8ba.png)

```C++
void dijkstra(int start) {
    for(int i = 1; i <= N; i++) {
        d[i] = INF;
    }
    d[start] = 0;
    priority_queue<pair<int, int>, vector<pair<int,int>>, greater<>> pq;
    pq.push({d[start], start});

    while(!pq.empty()) {
        int cost = pq.top().first;
        int curr = pq.top().second;
        pq.pop();

        if(cost > d[curr]) { continue; }

        for(int i = 0; i < graph[curr].size(); i++) {
            int next = graph[curr][i].first;
            if (d[next] > d[curr] + graph[curr][i].second) {
                d[next] = d[curr] + graph[curr][i].second;
                pq.push({d[next], next});
            }
        }
    }
}
```

장점: 인터넷 라우팅에서 사용되는 OSPF(Open Shortest Path First)방식의 프로토콜과 같이 현실에서 최단 경로를 찾기 적합한 알고리즘

단점: 음의 가중치 간선이 있으면 사용 불가

<br>
<hr>

## Bellman-Ford(벨만-포드)

<br>

**최단 경로 알고리즘**

`시간 복잡도: O(VE)`

`V는 노드, E는 간선`

`V - 1 번 인접한 모든 간선(E)들을 검사하는 과정`

다익스트라를 개선한 최단 경로 알고리즘, 다익스트라의 경우 음의 싸이클이 있다면 무한 뺑뺑이
(음수 가중치의 간선이 있다고 무조건 무한 뺑뺑이를 돌진 않음, 음의 싸이클이 있을 경우에만 -∞로 발산)

**거리 값을 갱신하는 과정을 V - 1번으로 제한하여 음의 싸이클 유무 판별!**

1. 시작 정점 결정
2. 시작 정점부터 다른 정점까지의 거리 값 무한대로 초기화(시작 정점은 0)
3. 현재 정점의 인접 정점들을 탐색하며, 기존의 거리값보다 더 짧은 거리값이 있을 경우 갱신
4. 3번 과정을 V - 1번 반복
5. 계속해서 갱신이 되는 경우 음수 사이클이 존재하는 것

왜 V - 1번 일까?
`최단 경로를 구하는 알고리즘에서 특정 정점을 2번 지날 수 없음`

```C++
// 음의 싸이클이 존재하는지 판별해주는 Bellman() 함수
bool bellman() {
    for (int i = 1; i <= N; i++) {
        d[i] = INF;
    }
    d[1] = 0;

    bool update = false;
    // 4번을 수행하기 위한 for문
    for(int loop = 0; loop < N - 1; loop++) {
        update = false;
        for(int curr = 1; curr <= N; curr++) {
            for(int adj = 0; adj < graph[curr].size(); adj++) {
                int next = graph[curr][adj].first;
                int cost = graph[curr][adj].second;
                if(d[curr] != INF && d[next] > d[curr] + cost) {
                    update = true;
                    d[next] > d[curr] + cost;
                }
            }
        }
        // 전체 노드에서 아무것도 갱신이 안됐다면 굳이 V - 1번까지 돌 필요도 없음
        if (!update) { return update; }
    }
    return update;
}
```

장점: 음의 가중치 간선이 있어도 사용 가능

단점: 다익스트라에 비해 큰 시간복잡도(O(VE) > O((V + E)logV))

출처 https://soobarkbar.tistory.com/75

<br>
<hr>

## KMP(Knuth, Morris, Prett)

<br>

**문자열 검색 알고리즘**

`시간 복잡도: O(N + M)`

<br>
1. 접두사(prefix)와 접미사(suffix)가 같은 가장 긴 문자열 길이를 저장하는 배열(pi) 생성

ex) 문자열 "ABAABAB"

<table border="1" style="text-align: center">
    <tr>
        <th>idx</th>
        <th>생성된 부분 문자열</th>
        <th>접두사</th>
        <th>중간 문자열</th>
        <th>접미사</th>
        <th>pi[idx]</th>
    </tr>
    <tr>
        <td>0</td>
        <td>A</td>
        <td>-</td>
        <td>A</td>
        <td>-</td>
        <td>0</td>
    </tr>
    <tr>
        <td>1</td>
        <td>AB</td>
        <td>-</td>
        <td>AB</td>
        <td>-</td>
        <td>0</td>
    </tr>
    <tr>
        <td>2</td>
        <td>ABA</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>1</td>
    </tr>
    <tr>
        <td>3</td>
        <td>ABAA</td>
        <td>A</td>
        <td>BA</td>
        <td>A</td>
        <td>1</td>
    </tr>
    <tr>
        <td>4</td>
        <td>ABAAB</td>
        <td>AB</td>
        <td>A</td>
        <td>AB</td>
        <td>2</td>
    </tr>
    <tr>
        <td>5</td>
        <td>ABAABA</td>
        <td>ABA</td>
        <td>-</td>
        <td>ABA</td>
        <td>3</td>
    </tr>
    <tr>
        <td>6</td>
        <td>ABAABAB</td>
        <td>AB</td>
        <td>AAB</td>
        <td>AB</td>
        <td>2</td>
    </tr>
</table>

<br>
2. pi배열을 이용하여 기존 문자열과 비교

ex) 문자열 S1에 "ABAABACABAABAB"에 문자열 S2가 "ABAABAB"이 있는가

    s1[6] != s2[6]

<table /border="1">
    <tr>
        <td>인덱스</td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>13</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td style="color: red">C</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
    </tr>
        <tr>
        <td>S2</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td style="color: red">B</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>

<br>

    s2의 부분문자열 "ABAABA"의 pi[5] = 3    // 3칸 이동

<table /border="1">
    <tr>
        <td>인덱스</td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>13</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td style="color: green">A</td>
        <td style="color: green">B</td>
        <td style="color: green">A</td>
        <td>C</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
    </tr>
        <tr>
        <td>S2</td>
        <td></td>
        <td></td>
        <td></td>
        <td style="color: green">A</td>
        <td style="color: green">B</td>
        <td style="color: green">A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>

<br>

    s1[6] != s2[4]

<table /border="1">
    <tr>
        <td>인덱스</td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>13</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td style="color: red">C</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
    </tr>
        <tr>
        <td>S2</td>
        <td></td>
        <td></td>
        <td></td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td style="color: red">A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>

<br>

    s2의 부분문자열 "ABA"의 pi[2] = 1    // 1칸 이동

<table /border="1">
    <tr>
        <td>인덱스</td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>13</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td style="color: green">A</td>
        <td>C</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
    </tr>
        <tr>
        <td>S2</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td style="color: green">A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
        <td></td>
        <td></td>
    </tr>
</table>

<br>

    s1[6] != s2[2]

<table /border="1">
    <tr>
        <td>인덱스</td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>13</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td style="color: red">C</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
    </tr>
        <tr>
        <td>S2</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>A</td>
        <td style="color: red">B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
        <td></td>
        <td></td>
    </tr>
</table>

<br>

    s1[6] != s2[0]  // 겹치는 것이 없어서 1칸만 이동

<table /border="1">
    <tr>
        <td>인덱스</td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>13</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td style="color: red">C</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
    </tr>
        <tr>
        <td>S2</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td style="color: red">A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>B</td>
        <td></td>
    </tr>
</table>

<br>

    s1문자열안에 s2문자열 포함

<table /border="1">
    <tr>
        <td>인덱스</td>
        <td>0</td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
        <td>9</td>
        <td>10</td>
        <td>11</td>
        <td>12</td>
        <td>13</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>A</td>
        <td>B</td>
        <td>A</td>
        <td>C</td>
        <td style="color: yellow">A</td>
        <td style="color: yellow">B</td>
        <td style="color: yellow">A</td>
        <td style="color: yellow">A</td>
        <td style="color: yellow">B</td>
        <td style="color: yellow">A</td>
        <td style="color: yellow">B</td>
    </tr>
        <tr>
        <td>S2</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td style="color: yellow">A</td>
        <td style="color: yellow">B</td>
        <td style="color: yellow">A</td>
        <td style="color: yellow">A</td>
        <td style="color: yellow">B</td>
        <td style="color: yellow">A</td>
        <td style="color: yellow">B</td>
    </tr>
</table>
