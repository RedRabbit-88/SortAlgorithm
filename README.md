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
	private static void insertionSort(int[] list) {
		int key, tgt, seek = 0;
		
		for (tgt = 1; tgt < list.length; tgt++) { // 2번째 요소부터 시작
			key = list[tgt]; // 현재 요소를 키값으로 설정
			
			// 첫 번째 요소까지 확인하면서 키값보다 큰 값은 한 칸씩 뒤로 이동.
			// 키값보다 작은 값을 만났을 때 중지
			for (seek = tgt - 1; seek >= 0 && list[seek] > key; seek--) {
				list[seek + 1] = list[seek];
			}
			// 키값보다 작은 값 위치에 키값을 삽입
			list[seek + 1] = key;
			
			printList(list);
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
	private static void selectionSort(int[] list) {
		for (int i = 0; i < list.length; i++) { // 요소의 개수만큼 루프
			int key = i; // n번째 위치를 저장
			
			// n번째 위치부터 끝까지 가장 작은 값의 위치를 찾기
			for (int j = i; j < list.length; j++) {
				if (list[j] < list[key]) {
					key = j; // 키값보다 작은 값을 찾을 때마다 키값 교체
				}
			}
			// 키값에 변경이 있었을 경우에만 swap 실행
			if (i != key) {
				int tmp = list[i];
				list[i] = list[key];
				list[key] = tmp;
			}
			printList(list);
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
	private static void bubbleSort(int[] list) {
		for (int i = list.length - 1; i > 0; i--) { // 배열 마지막에서부터 시작
			// 배열의 첫번째 요소부터 n, n+1번째 요소를 비교하며 n번째 요소가 더 클 경우 swap
			for (int j = 0; j < i; j++) {
				if (list[j] > list[j + 1]) {
					int temp = list[j + 1];
					list[j + 1] = list[j];
					list[j] = temp;
				}
			}
			printList(list);
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
1. left/right사이 임의의 값을 pivot으로 사용
2. left부터 우측으로 pivot과 비교하면서 pivot보다 "큰" 값을 찾음.
3. right부터 좌측으로 pivot과 비교하면서 pivot보다 "작은" 값을 찾음.
4. 2/3번에서 구한 값을 swap
5. 1~4를 반복
* 4번에서 값이 swap되었기 때문에 2번에서 찾은 pivot보다 "큰" 값은 pivot의 우측에, 3번에서 찾은 pivot보다 "작은" 값은 pivot의 좌측으로 이동함.
* 이후 계속해서 pivot 좌측에서 pivot보다 "큰" 값과 pivot 우측에서 pivot보다 "작은" 값을 찾아서 swap 작업 수행.
* 더 이상 pivot을 기준으로 정렬될 값이 없을 때까지 계속
```
	private static void quickSort(int[] list, int left, int right) {
		if (left >= right)
			return;

		int pivot = list[left]; // 가장 왼쪽의 요소를 pivot으로 사용
		int low = left + 1; // pivot 다음 요소부터 pivot 보다 큰 값 검색
		int high = right; // 가장 오른쪽부터 pivot 보다 작은 값 검색
		
		while (low <= high) { // low, high가 교차하기 전까지 반복 (모든 요소 검색)
			while (low <= right && list[low] <= pivot) { // 왼쪽부터 pivot보다 큰 값을 찾는다 
				low++;
			}
			while (high >= left + 1 && list[high] >= pivot) { // 오른쪽부터 pivot보다 작은 값을 찾는다
				high--;
			}
			if (low <= high) { // low/high가 아직 교차하지 않았으면 Swap
				int tmp = list[high];
				list[high] = list[low];
				list[low] = tmp;
			} else { 
				// low/high 값이 교차했다면 (모든 요소 검색이 끝났다면)
				// 마지막 high 값은 가장 왼쪽값인 pivot과 교환. pivot값은 가운데가 된다
				list[left] = list[high];
				list[high] = pivot;
			}
		}
		printList(list);
		
		quickSort(list, left, high - 1);
		quickSort(list, high + 1, right);
	}
```

## 5. 합병 정렬 (Merge Sort)
### 개념
* 분할 정복 알고리즘의 하나로 매우 빠른 속도를 자랑하며 안정 정렬이다
* 배열의 길이가 0 또는 1이면 이미 정렬된 걸로 가정
* 그렇지 않은 경우에는 배열을 절반으로 잘라 2개로 분할한다.
* 각각 분할된 배열을 재귀함수를 이용하여 합병하며 정렬한다.
* 시간 복잡도
   * Best : O(nlogn)
   * Average : O(nlogn)
   * Worst : O(n2)

### 알고리즘
1. 분할된 배열의 중간값을 산출
2. 왼쪽부터 중간값, 중간값+1부터 오른쪽으로 배열을 나누는 재귀함수 호출
3. 1~2를 반복. 더 이상 분할할 수 없을 경우 합병 과정을 재귀함수로 수행
4. 중간값을 기준으로 왼쪽과 오른쪽 요소들을 하나씩 비교해가며 임시 배열에 입력
5. 합병 함수에서 정렬할 수 있는 모든 값이 임시 배열에 정렬된 후 원래 배열에 입력
```
	/**
	 * Merge Sort 구현
	 * 1. 분할된 배열의 중간값을 산출
	 * 2. 왼쪽부터 중간값, 중간값+1부터 오른쪽으로 배열을 나눠서 mergeSort 호출 (재귀)
	 * 3. 1~2를 반복. 더 이상 분할할 수 없을 경우 종료
	 * 
	 * @param intArr
	 * @param left
	 * @param right
	 */
	private static void mergeSort(int[] intArr, int left, int right) {
		// left가 right보다 작으면 분할 작업 수행
		// left = right가 되는 순간 중지 = 더 이상 쪼개질 수 없을 때까지
		if (left < right) {
			int mid = (left + right) / 2; // 분할을 위한 중간값 계산
			mergeSort(intArr, left, mid); // 왼쪽부터 중간값까지 분할
			mergeSort(intArr, mid + 1, right); // 중간값+1부터 오른쪽까지 분할
			merge(intArr, left, mid, right); // 정렬 및 merge 작업 수행
		}
	}
	
	/**
	 * mergeSort에서 호출되는 merge 함수
	 * 1. merge함수는 더 이상 배열을 분할할 수 없을 때부터 작동하기 시작
	 * 2. mergeSort(2, 2) 와 같이 left/right가 동일할 경우에는 아무런 동작을 안 함
	 * 3. mergeSort(2, 3) 와 같이 left/right가 다를 경우 동작
	 * 4. 중간값을 기준으로 왼쪽과 오른쪽 요소들을 하나씩 비교해가며 임시 배열에 입력
	 * 5. 해당 merge 함수에서 정렬할 수 있는 모든 값이 임시 배열에 정렬된 후 원래 배열에 입력
	 * 
	 * Ex1 mergeSort(0, 1)에서 merge(0, 0, 1)가 호출됨
	 *     1) 중간값은 0번째 요소로 가정
	 *     2) 왼쪽 요소 시작은 0번째 부터
	 *     3) 오른쪽 요소 시작은 중간값+1인 1번째 부터
	 *     > 즉 0번째와 1번째를 비교해서 더 작은 값을 먼저 임시 배열에 입력
	 * 
	 * Ex2 mergeSort(0, 2)에서 merge(0, 1, 2)가 호출됨
	 *     1) 중간값은 1번째 요소로 가정
	 *     2) 왼쪽 요소 시작은 0번째 부터
	 *     3) 오른쪽 요소 시작은 중간값+1인 2번째 부터
	 *     > 즉 0번째와 2번째를 비교해서 더 작은 값을 먼저 임시 배열에 입력
	 *     > 해당 함수는 Ex1의 merge(0, 0, 1)이 호출된 후에 호출되므로 이미 0/1번째는 정렬이 완료된 후 호출
	 * 
	 * [호출 순서]
	 * mergeSort(0, 8)			// 17 - merge(0, 4, 8) : 0~8번 정렬
	 *   mergeSort(0, 4)			// 15 - merge(0, 2, 4) : 0~4번 정렬
	 *     mergeSort(0, 2)				// 11 - merge(0, 1, 2) : 0~2번 정렬
	 *       mergeSort(0, 1) 				// 9 - merge(0, 0, 1) : 0~1번 정렬
	 *         mergeSort(0, 0)					// 1 - merge(0, 0, 0) : 아무런 동작 안 함
	 *         mergeSort(1, 1)					// 2 - merge(1, 1, 1) : 아무런 동작 안 함
	 *       mergeSort(2, 2) 				// 10 - merge(2, 2, 2) : 아무런 동작 안 함
	 *     mergeSort(3, 4)				// 12 - merge(3, 3, 4) : 3~4번 정렬
	 *       mergeSort(3, 3)					// 3 - merge(3, 3, 3) : 아무런 동작 안 함
	 *       mergeSort(4, 4)					// 4 - merge(4, 4, 4) : 아무런 동작 안 함
	 *   mergeSort(5, 8)			// 16 - merge(5, 6, 8) : 5~8번 정렬
	 *     mergeSort(5, 6)				// 13 - merge(5, 5, 6) : 5~6번 정렬
	 *       mergeSort(5, 5)					// 5 - merge(0, 0, 0) : 아무런 동작 안 함
	 *       mergeSort(6, 6)					// 6 - merge(0, 0, 0) : 아무런 동작 안 함
	 *     mergeSort(7, 8)				// 14 - merge(7, 7, 8) : 7~8번 정렬
	 *       mergeSort(7, 7)					// 7 - merge(7, 7, 7) : 아무런 동작 안 함
	 *       mergeSort(8, 8)					// 8 - merge(8, 8, 8) : 아무런 동작 안 함
	 * 
	 * @param intArr
	 * @param left
	 * @param mid
	 * @param right
	 * @return
	 */
	private static void merge(int[] intArr, int left, int mid, int right) {
		// 요소를 정렬해서 담아둘 임시 배열
		int[] temp = new int[intArr.length];
		
		int tmpIdx = left;	// 임시 배열에 요소를 입력하는 초기 위치
		int l = left;		// 왼쪽 기준값
		int r = mid + 1;	// 오른쪽 기준값
		
		// 왼쪽 기준값이 중간값에 도달하거나 중간값이 오른쪽 끝 값에 도달할 때까지 반복
		while (l <= mid && r <= right) {
			if (intArr[l] <= intArr[r]) { // 왼쪽/오른쪽 값을 비교
				temp[tmpIdx++] = intArr[l++]; // 왼쪽값이 작을 경우 임시 배열에 왼쪽값 입력
			} else {
				temp[tmpIdx++] = intArr[r++]; // 오른쪽값이 작을 경우 임시 배열에 오른쪽값 입력
			}
		}
		
		// 만약 중간값 기준 오른쪽 요소들이 전부 임시 배열에 들어간 경우
		// 남아 있는 왼쪽 요소들을 임시 배열에 입력
		while (l <= mid) {
			temp[tmpIdx++] = intArr[l++];
		}
		
		// 만약 중간값 기준 왼쪽 요소들이 전부 임시 배열에 들어간 경우
		// 남아 있는 오른쪽 요소들을 임시 배열에 입력
		while (r <= right) {
			temp[tmpIdx++] = intArr[r++];
		}
		
		// 임시배열에 저장된 값들을 원래 배열에 입력
		for (int i = left; i <= right; i++) {
			intArr[i] = temp[i]; 
		}
	}
```
