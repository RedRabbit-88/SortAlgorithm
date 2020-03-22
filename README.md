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

## 3. 버블 정렬 (Bubble Sort)
### 개념
* 루프를 돌며 n번째와 n+1번째 요소를 비교해서 순서를 정렬하는 정렬
* 마치 Bubble과 같이 매 루프 수행 시마다 최대값이 가장 뒤로 정렬되는 구조
* 시간 복잡도
   * Best : O(n2)
   * Average : O(n2)
   * Worst : O(n2)

### 알고리즘
1. 첫번째 요소부터 루프 시작
2. 바로 뒤에 요소보다 값이 클 경우 서로 위치 변경. 마지막 요소까지 반복
3. 1~2를 반복. n회 반복 시마다 배열 length - n번까지만 비교
```
	private static void bubbleSort(int[] intArr) {
		for (int out = intArr.length - 1; out > 0; out--) {
			for (int in = 0; in < out; in++) {
				if (intArr[in] > intArr[in + 1]) {
					int temp = intArr[in];
					intArr[in] = intArr[in + 1];
					intArr[in + 1] = temp;
				}
			}
		}
	}
```

## 4. 퀵 정렬 (Quick Sort)
### 개념
* 분할 정복 알고리즘의 하나로 매우 빠른 속도를 자랑하지만, 불안정 정렬이다.
* 합병 정렬(Merge Sort)와 달리 퀵 정렬은 배열을 "불균등"하게 분할한다.
* 배열에 있는 하나의 요소를 골라 pivot이라 지정.
* pivot을 기준으로 왼쪽은 pivot보다 작은 값, 오른쪽은 pivot보다 큰 값을 정렬.
* 정렬이 완료되면 pivot을 기준으로 배열을 분할해서 동일 작업 수행
* 시간 복잡도
   * Best : O(nlogn)
   * Average : O(nlogn)
   * Worst : O(n2)

### 알고리즘
1. left/right의 중앙에 있는 값을 pivot으로 사용
2. left부터 우측으로 pivot과 비교하면서 pivot보다 "큰" 값을 찾음.
3. right부터 좌측으로 pivot과 비교하면서 pivot보다 "작은" 값을 찾음.
4. 2/3번에서 구한 값을 swap
5. 1~4를 반복
* 4번에서 값이 swap되었기 때문에 2번에서 찾은 pivot보다 "큰" 값은 pivot의 우측에, 3번에서 찾은 pivot보다 "작은" 값은 pivot의 좌측으로 이동함.
* 이후 계속해서 pivot 좌측에서 pivot보다 "큰" 값과 pivot 우측에서 pivot보다 "작은" 값을 찾아서 swap 작업 수행.
* 더 이상 pivot을 기준으로 정렬될 값이 없을 때까지 계속
```
	private static void quickSort(int[] intArr, int left, int right) {
		if (left < right) { // 더 이상 분할할 값이 없을 경우 종료
			// 분할된 배열로 정렬작업 수행
			int pivot = partition(intArr, left, right);
			
			quickSort(intArr, left, pivot - 1);  // 분할된 배열의 좌측부터 pivot 전까지로 분할
			quickSort(intArr, pivot + 1, right); // 분할된 배열의 pivot 다음부터 우측 끝까지로 분할
		}
	}
	
	private static int partition(int[] intArr, int left, int right) {
		int low = left;		// 좌측 끝값
		int high = right;	// 우측 끝값
		int pivot = intArr[(low + high) / 2]; // 중간값을 pivot으로 설정
		
		while (low < high) { // 정렬할 값들이 존재할 때
			// 좌측 끝부터 pivot까지 pivot보다 큰 값을 찾음
			while (low <= right && intArr[low] < pivot) {
				low++;
			}
			// 우측 끝부터 pivot까지 pivot보다 작은 값을 찾음
			while (high >= left && intArr[high] > pivot) {
				high--;
			}
			// pivot 기준으로 좌측에서 pivot보다 큰 값과 우측에서 pivot보다 작은 값이 존재할 경우
			// 두 값을 swap
			if (low < high) {
				int temp = intArr[high];
				intArr[high] = intArr[low];
				intArr[low] = temp;
			}
		}
		
		return low;
	}
```
