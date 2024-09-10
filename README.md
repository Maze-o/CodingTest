<h1>프로그래머스 코딩테스트</h1>

<hr>

<h3>체육복</h3>

```

import java.util.Arrays;
// sort함수를 쓸것이기 때문에 배열 라이브러리 import

class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        //잃어버린사람 answer , 입력값 n , 잃어버린사람 lost, 여벌 체육복 있는사람 reserve
        
        int answer = n - lost.length; // 잃어버리지 않은 사람 answer에 대입

        // 정렬 해주지 않으면 배열값 대입할때 뒤죽박죽임
        Arrays.sort(reserve); //여벌 체육복 있는 사람 배열 오름차순으로 정렬
        Arrays.sort(lost); // 잃어버린 사람 배열 오름차순으로 정렬 
        
        
        // 여벌을 챙겨온 사람이 도난당한 상황
        for (int i = 0; i < lost.length; i++) {
            for (int j = 0; j < reserve.length; j++) { 
                if (lost[i] == reserve[j]) { // 빌려준 사람이랑 잃어버린 사람의 배열이 같으면 본인에게 빌려준 것으로 간주하고
                    answer++; // 잃어버리지 않은 사람에 1 더해주고 (본인이 빌려주고 받았으니)
                    lost[i] = -1; // 배열을 하나 줄이기 위해 (1명이 빠졌으니) -1를 대입해
                    reserve[j] = -1; // reserve도 - 해주는 이유는 잃어버린 사람과 빌려준 사람이 같아 둘다 빼야함
                    break; // if문 탈출
                }
            }
        }
        
        // 여벌 체육복이 있는 사람이 빌려주는 상황
         for(int i = 0; i < lost.length; i++) { // length가 위에 본인을 제외한 상태로 시작
            for(int j = 0; j < reserve.length;j++) {
                //앞사람 대여                             뒷사람 대여
                if((lost[i]-1 == reserve[j]) || (lost[i]+1 == reserve[j])) { // or연산자로 앞이나 뒤사람중에 true가 되면 (여벌은 한벌이니)            
                    answer++; // 잃어버리지 않은사람 (빌려준 체육복을 받았으니) 더해줌              
                    reserve[j] = -1; // 빌려준 사람을 -1 
                    break; // if문 탈출
                }
            }
        }

        // 잃어버리지 않은사람 리턴        
        return answer;
        
        
    }
}

```
