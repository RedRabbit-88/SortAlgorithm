# SortAlgorithm

## 1. 삽입정렬 (Insertion Sort)
### 개념
* 자료 배열의 모든 요소를 앞에서부터 차례대로 정렬된 배열 요소와 비교하며 정렬
* 매 루프 수행 시 최소값을 찾아 루프 시작 위치에 "삽입"한다.
* 시간 복잡도
   * Best : O(n)
   * Average : O(n2)
   * Worst : O(n2)

### 알고리즘
1. 2번째 요소부터 루프 시작. 이를 정렬할 기준값으로 설정 (n)
2. n-1번재 요소부터 첫번쨰 요소까지 루프 돌며 기준값보다 큰 요소들은 하나씩 뒤로 이동
3. 기준값보다 작은 요소를 찾으면 해당 요소 바로 뒤로 기준값 삽입
4. 1~3을 마지막 요소까지 반복
```
	private static void insertionSort(int[] intArr) {
		int out, in, key = 0;
		
		for (out = 1; out < intArr.length; out++) { // 2번째 요소부터 시작
			key = intArr[out]; // 현재 요소를 키값으로 설정
			// 첫 번째 요소까지 확인하면서 키값보다 큰 값은 한 칸씩 뒤로 이동.
			// 키값보다 작은 값을 만났을 때 중지
			for (in = out - 1; in >= 0 && key < intArr[in]; in--) {
				intArr[in + 1] = intArr[in];
			}
			// 키값보다 작은 값 바로 뒤에 키값을 삽입
			intArr[in + 1] = key;
		}
	}
```

## 2. 선택 정렬 (Selection Sort)
### 개념
* 루프를 돌며 최소값을 "선택"해서 지정된 자리에 삽입하는 정렬
* 매 루프 수행 시마다 배열에서 n번째 작은 값을 n번째에 입력하는 구조
* 시간 복잡도
   * Best : O(n2)
   * Average : O(n2)
   * Worst : O(n2)

### 알고리즘
* 첫번째 요소부터 루프 시작 (n)
* n+1번째 요소부터 마지막 요소까지 루프 돌며 최소값 확인
* 마지막 요소까지 확인 후 최소값을 n번째 요소와 swap
* 1~3을 반복
```
	private static void selectionSort(int[] intArr) {
		for (int out = 0; out < intArr.length - 1; out++) {
			int min = out;
			for (int in = out + 1; in < intArr.length; in++) {
				if (intArr[in] < intArr[min]) {
					min = in;
				}
			}
			if (out != min) {
				int temp = intArr[out];
				intArr[out] = intArr[min];
				intArr[min] = temp;
			}
		}
	}
```
