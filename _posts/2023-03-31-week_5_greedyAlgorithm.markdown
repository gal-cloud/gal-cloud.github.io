2023-03-31-week_4_greedyAlgorithm.markdown

Greedy Algorithm

import java.util.ArrayList;
import java.util.Scanner;
public class week_5_1 {

    ArrayList<Integer> coin = new ArrayList<>();

    public static void ChangeCoin(int changeW) {
        int[] coins = {500, 100, 50, 10, 1};   // coins를 배열로 선언
        int[] n = new int[coins.length];        // 각 동전의 개수를 coins와 같은 크기의 배열로 정리
        for (int i=0 ; i<coins.length ; i++) {   // coins 배열의 크기만큼 반복
            while (changeW >= coins[i]) {         // 거스름돈이 coins의 각 배열보다 작다면 반복
                changeW -= coins[i];                // 배열의 진행상황만큼 -=
                n[i] += 1;                          // 동전의 개수를 ++
            }
        }
        System.out.print("거스름돈은 ");
        for(int i=0 ; i<coins.length ; i++)
            System.out.printf("%d원 %d개 ", coins[i], n[i]);
    }
        /*
        int n500=0, n100=0, n50=0, n10=0, n1=0;

        if(changeW <=0 ){
            System.out.println("올바르지 못한 입력입니다.");
            return;
        }
        while(changeW >= 500 ){
            changeW = changeW-500;
            n500++;
        }
        while(changeW >= 100){
            changeW = changeW - 100;
            n100++;
        }
        while(changeW >= 50){
            changeW = changeW - 50;
            n50++;
        }
        while(changeW >= 10) {
            changeW = changeW - 10;
            n10++;
        }
        while(changeW >= 1){
            changeW = changeW - 1;
            n1++;
        }
        System.out.printf("거스름 돈은 500원 %d개, 100원 %d개, 50원 %d개, 10원 %d개, 1원 %d개 입니다", n500, n100, n50, n10, n1);
    }
    */

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.print("거스름 돈 입력 : ");
        int changeW = sc.nextInt();

        System.out.println(changeW);
        ChangeCoin(changeW);

    }
}