
# 기존코드
    시간복잡도 최대 O(N), 시간 초과 발생
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;

public class BOJ_11286_절댓값합구현하기 {
	
	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();
		
		int N = Integer.parseInt(br.readLine());
		
		// 값을 담을 List
		List<Long> list = new ArrayList<>();
		
		// N 번 반복
		for(int i = 0; i < N; i++) {
			
			// 인덱스를 담을 변수
			int index = 0;
			
			// X 갑 입력받음
			long X = (long) Integer.parseInt(br.readLine());
					
			if(X != 0) { // X가 0이 아니라면 리스트에 값 추가
				list.add(X);
			} else { // X가 0이라면 절대값이 가장 작은 값을 출력하고, 제거
				for(int s = 0; s < list.size(); s++) {
					
					// 만약 두 절대값이 같다면 더 작은 값을 저장
					if(Math.abs(list.get(index)) == Math.abs(list.get(s))) {
						index = list.get(index) > list.get(s) ? s : index;
						
					// 기존 값보다 더 작은 절대값이 있다면 index 변경	
					} else if(Math.abs(list.get(index)) > Math.abs(list.get(s))) {
						index = s;
					}			
				}
							
				// 배열이 비어있는데 절대값이 가장 작은 값을 출력하라고 한 경우
				if(list.size() == 0) {
					sb.append("0").append("\n");
				} else { // 배열이 비어있지 않고 값을 출력하라고 한 경우
					// 절대값이 가장 작은 값을 출력
					sb.append(list.get(index)).append("\n");
					// 배열에서 값 제거
					list.remove(index);					
				}
			}
		}
		
		System.out.println(sb);
	}
}
```

# 개선코드
    시간복잡도 O(logN)
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Comparator;
import java.util.PriorityQueue;

public class BOJ_11286_절댓값합구현하기 {

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();

		int N = Integer.parseInt(br.readLine());

		// 값을 담을 우선순위 큐
		PriorityQueue<Long> pq = new PriorityQueue<>( (Long o1, Long o2) -> {
				// 절대값을 기준으로 비교 o1 = o2 -> 0 반환, 같으면 o1 < o2는 0보다 작은값 반환, o1 > o2 0보다 큰 값 반환 
				int absoluteValue = Long.compare(Math.abs(o1), Math.abs(o2));
				return absoluteValue != 0 ? absoluteValue : Long.compare(o1, o2);
		});

		// N 번 반복
		for(int i = 0; i < N; i++) {

			// X에 값 입력
			long X = Long.parseLong(br.readLine());

			if(X != 0) { // X가 0이 아니라면 큐에 값 추가
				pq.add(X);

			} else { // X가 0이라면 절대값이 가장 작은 값을 출력하고, 제거

				// 큐가 비어있는데 절대값이 가장 작은 값을 출력하라고 한 경우 빌더에 0 저장
				if(pq.size() == 0) {
					sb.append("0").append("\n");
				} else { // 큐가 비어있지 않고 값을 출력하라고 한 경우
					// 절대값이 가장 작은 값을 빌더에 저장하고, 큐에서 제거
					sb.append(pq.poll()).append("\n");
				}
			}
		}

    // 빌더에 저장된 값 한 번에 출력		
		System.out.println(sb);
	}
}
```
