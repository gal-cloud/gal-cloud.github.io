2023-04-14-"week_6_assignment".markdown

컴퓨터 알고리즘 6주차 과제

1번 작업 스케쥴링 소스코드
```
import java.util.*;
public class assignment_1 {
    public static void main(String[] args){

        Scanner sc = new Scanner(System.in);
        ArrayList<Job> job = new ArrayList<Job>();

        int n = sc.nextInt();
        for(int i=0 ; i<n ; i++){
            int start = sc.nextInt();
            int end = sc.nextInt();
            job.add(new Job(start, end));
        } // 데이터 입력

        Comparator<Job> comp = new Comparator<Job>(){
            @Override
            public int compare(Job o1, Job o2){
                return o1.start - o2.start;
            }
        }; // 시작시간에 따라 오름차순 정렬

        Collections.sort(job, comp); // job을 시작시간으로 오름차순 정렬
        printMachine(job); // 정렬된 job 출력
        System.out.println();
        JobScheduling(job, n);
    }
    public static void printMachine(ArrayList<Job> job){
        System.out.print("정렬된 알고리즘 : ");
        for(Job x : job){
            System.out.printf("[%d, %d] ", x.start, x.end);
        }
    } // Machine을 한번에 print 출력하기 위한 메소드
    public static void JobScheduling(ArrayList<Job> job, int n){
        ArrayList<Job>[] machine = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            machine[i] = new ArrayList<>();
        } // 작업의 개수만큼 기계를 의미하는 배열 생성
        int machineNum = 0;
        while(!job.isEmpty()){ // job이 null이 될때까지 while 반복
            int complete=0;
            for (int i = 0; i < machineNum; i++) {
                if (job.get(0).start >= (machine[i].get(machine[i].size() - 1).end)) { // 기계의 종료시간보다 작업의 시작시간이 늦거나 같다면 true반환
                    machine[i].add(job.remove(0)); // 해당 기계에 작업 추가 & job에서 작업 삭제
                    complete++; // job에서 작업을 사용했다는 것을 확인하기 위한 변수
                    break; // for문의 반복을 끊어 greedy algorithm을 유지하기 위한 break
                } //
            }
            if(complete==1)continue; // 위에서 표시했듯 작업을 사용했기 때문에 continue로 밑의 코드가 실행되지 않도록 while문을 넘김
            machine[machineNum].add(job.remove(0)); // 기존 기계에 작업이 추가되지 않고 넘어왔으므로 비어있는 기계에 작업을 추가 & job에서 작업 삭제
            machineNum++; // 새로운 기계를 사용했으므로 다음 기계로 기계수를 1개 늘림
        }
        for(int i=0 ; i<machineNum ; i++){
            System.out.printf("machine %d번 : ", i);
            for(int j=0 ; j<machine[i].size() ; j++){
                System.out.printf("[%d, %d] - ", machine[i].get(j).start,machine[i].get(j).end);
            }
            System.out.println();
        }
    }
}
class Job extends HashSet<Integer>{
    int start, end;
    public Job(int start, int end){
        this.start = start;
        this.end = end;
    }
} // 시작시간과 종료시간의 정보를 갖는 Job 클래스
```
1번 result
```
7
7 8
3 7
1 5
5 9
0 2
6 8
1 6
정렬된 알고리즘 : [0, 2] [1, 5] [1, 6] [3, 7] [5, 9] [6, 8] [7, 8] 
machine 0번 : [0, 2] - [3, 7] - [7, 8] - 
machine 1번 : [1, 5] - [5, 9] - 
machine 2번 : [1, 6] - [6, 8] - 
```

2번 회의실 배정 (백준) 소스코드
```
import java.util.*;
public class assignment_2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayList<Conference> conferences = new ArrayList<Conference>();

        int N = sc.nextInt();
        for (int i = 0; i < N; i++) {
            int start = sc.nextInt();
            int end = sc.nextInt();
            conferences.add(new Conference(start, end));
        } // Input
        Comparator<Conference> comp = new Comparator<Conference>(){
            @Override
            public int compare(Conference o1, Conference o2){
                return o1.end - o2.end;
            }
        };                                      // ArrayList<Conference>를 종료시간에 따른 오름차순으로 정렬
        Collections.sort(conferences, comp);    // 종료시간의 오름차순으로 conferences 정렬
        System.out.println("정렬된 회의 :");
        for(int i=0 ; i<conferences.size() ; i++) System.out.printf("[%d %d] ", conferences.get(i).start, conferences.get(i).end); // 점검을 위해 conferences 출력
        System.out.println();
        conferenceSchedule(conferences);
    }
    public static void conferenceSchedule(ArrayList<Conference> conference){                        // Conference ArrayList를 인수로 받음
        ArrayList<Conference> conferenceRoom = new ArrayList<Conference>();                         // 문제에서 주어진 회의실을 ArrayList로 구현함
        while(!conference.isEmpty()){                                                               // conference가 null이 되는 순간까지 반복
            if (conferenceRoom.isEmpty()){                                                          // 회의실이 비어있다면 conference의 0번 인덱스를 회의실에 넣어줌
                conferenceRoom.add(conference.remove(0));                                     // 회의를 추가함과 동시에 conference에서 회의를 삭제한다
            } else if (conference.get(0).start >= conferenceRoom.get(conferenceRoom.size()-1).end){ // 회의의 시작시간이 회의실 마지막 회의의 종료시간보다 늦거나 같다면 회의 추가
                conferenceRoom.add(conference.remove(0));                                     // 회의를 추가함과 동시에 conference에서 회의를 삭제한다
            } else {                                                                                // conference의 회의가 회의실에 넣을 수 없는 시간대일때, conference의 회의를 삭제한다.
                conference.remove(0);
            }
        }
        System.out.println("회의실의 회의목록 출력");
        for(int i=0 ; i<conferenceRoom.size() ; i++) System.out.printf("[%d, %d] - ", conferenceRoom.get(i).start, conferenceRoom.get(i).end);
        System.out.print("\b\b\n");
        System.out.printf("최대로 사용할 수 있는 회의의 개수는 %d개이다.", conferenceRoom.size());
    }
}
class Conference{ // 시작시간과 종료시간을 인수로 가지는 Conference 클래스를 선언한다
    int start, end;
    public Conference(int start, int end){
        this.start = start;
        this.end = end;
    }
}
```
2번 result
```
11
1 4
3 5
0 6
5 7
3 8
5 9
6 10
8 11
8 12
2 13
12 14
정렬된 회의 :
[1 4] [3 5] [0 6] [5 7] [3 8] [5 9] [6 10] [8 11] [8 12] [2 13] [12 14] 
회의실의 회의목록 출력
[1, 4] - [5, 7] - [8, 11] - [12, 14] 
최대로 사용할 수 있는 회의의 개수는 4개이다.
```


