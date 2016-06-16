package swtest;

import java.util.LinkedList;
import java.util.Scanner;


public class PavementRecovery {
	
	static final int SPLIT = 1000;
	static int N;	
	static int[][] input = new int [102][102];
	static int[][] minTime = new int [102][102];

	static LinkedList <Integer> arr = new LinkedList<Integer>(); 

	static int rowGo []  = {1, -1,  0,  0}; 
	static int colGo [] =  {0,  0,  1, -1};

	
	public static void main(String args[]) throws Exception {
		
		long startTime = System.currentTimeMillis();
		
		int Answer = 0;
//		System.setIn(new FileInputStream(PavementRecovery.class.getResource("").getPath() + "AlienSite_sample_input.txt"));
//		System.setIn(new FileInputStream("AlienSite_sample_input.txt"));
		Scanner sc = new Scanner(System.in);
		 

		/*
		* 테스트 케이스의 수를 입력 받습니다.
		*/
		int T = sc.nextInt();

		/*
		* T 개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
		*/
		for(int test_case = 1; test_case <= T; ++test_case) {
			// 도로수
			N = sc.nextInt();
			
			for(int i=1; i<=N; i++){
				String str = sc.next();
				for(int j=1; j<=N; j++){
					input[i][j] = str.charAt(j-1)-'0';
					minTime[i][j] =999;
				}
			}
			
			
			//초기값만 0으로 
			minTime[1][1] =0;
			
			//초기 출발점 세팅
			arr.addLast(1*SPLIT + 1);
			
			int addedTime = 0; 
			int minValue = 999;
			int rowParentAdded = 0;
			int colParentAdded = 0;
		
			while (!arr.isEmpty()){
				
				int tempPos = arr.removeFirst();
				
				//현재경로의 인접위치 Queueing
							
				for (int i = 0 ; i<4; i++){					
					
					if (minTime[tempPos/SPLIT +rowGo[i]][tempPos%SPLIT +colGo[i]] > minTime[tempPos/SPLIT][tempPos%SPLIT] 
							+ input[tempPos/SPLIT+rowGo[i]][tempPos%SPLIT+colGo[i]]){
						
						minTime[tempPos/SPLIT +rowGo[i]][tempPos%SPLIT +colGo[i]] = minTime[tempPos/SPLIT][tempPos%SPLIT] 
								+ input[tempPos/SPLIT+rowGo[i]][tempPos%SPLIT+colGo[i]];
						
						arr.add((tempPos/SPLIT+rowGo[i])*1000 + tempPos%SPLIT+colGo[i]);					
						
					}
					
				}
				
			
			Answer = minTime[N][N];
			System.out.println(Answer);
			
		}
		
		System.out.println("\nElapsed Time : " + ((double)(System.currentTimeMillis() - startTime)/1000));
	}
		
	
			
			
}
