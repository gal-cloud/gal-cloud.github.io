2023-04-07-week_6_greedySchool.markdown

import java.util.*;

public class week_6_1 {
    
    public static void main(String[] args){
        HashSet<Integer> u = new HashSet<Integer>();
        for (int i=1 ; i<=10 ; i++){
            u.add(i);
        }// hashset u에 1부터 10까지 값 add
       /* MySet<Integer> s1 = new MySet<Integer>(1,2,3,8);
        MySet<Integer> s2 = new MySet<Integer>(1,2,3,4,8);
        MySet<Integer> s3 = new MySet<Integer>(1,2,3,4);
        MySet<Integer> s4 = new MySet<Integer>(2,3,4,5,7,8);
        MySet<Integer> s5 = new MySet<Integer>(4,5,6,7);
        MySet<Integer> s6 = new MySet<Integer>(5,6,7,9,10);
        MySet<Integer> s7 = new MySet<Integer>(4,5,6,7);
        MySet<Integer> s8 = new MySet<Integer>(1,2,4,8);
        MySet<Integer> s9 = new MySet<Integer>(6,9);
        MySet<Integer> s10 = new MySet<Integer>(6,10);*/

        ArrayList<MySet> f = new ArrayList<MySet>();
        f.add(new MySet<Integer>(1,2,3,8));
        f.add(new MySet<Integer>(1,2,3,4,8));
        f.add( new MySet<Integer>(1,2,3,4));
        f.add( new MySet<Integer>(2,3,4,5,7,8));
        f.add( new MySet<Integer>(4,5,6,7));
        f.add( new MySet<Integer>(5,6,7,9,10));
        f.add( new MySet<Integer>(4,5,6,7));
        f.add(new MySet<Integer>(1,2,4,8));
        f.add( new MySet<Integer>(6,9));
        f.add( new MySet<Integer>(6,10));
        System.out.println("초기입력값 : " +f); // myset class에 노드별 간선정보 입력후 출력


        Comparator<MySet> comp = new Comparator<MySet>(){
            @Override
            public int compare(MySet o1, MySet o2){
                return -(o1.size() - o2.size()); // siza가 더 큰걸 앞으로 가져옴
            }
        }; // 비교기준 메소드
        Collections.sort(f, comp); // comp기준으로 myset arraylist를 sort한다
        System.out.println("정렬후 : "+ f); // sort한 arraylist f를 출력

        ArrayList<MySet> c = new ArrayList<MySet>();
        while(!u.isEmpty()){
            MySet<Integer> tmp = func2(u, f);
            u.removeAll(tmp);
            c.add(tmp);
            f.remove(tmp);
        }; // 

        System.out.println(func(u, f.get(1)));
        System.out.println(func2(u, f));


        }

        public static int func(HashSet<Integer> u, MySet<Integer> s){ // hashset이랑 myset을 인자로 받음
            int n = 0;
            for (Integer i : u){
                if(s.contains(i)) n+=1;
             }
             return n;
        } // u에 들어있는 i를 꺼내온 후 s에 i가 있으면 n의 index를 1개씩 늘려감
        public static MySet<Integer> func2(HashSet<Integer> u, ArrayList<MySet> f){
            int n=0;
            int idx = 0;
            for(int i=0 ; i<f.size() ; i++){
                int tmp = func(u, f.get(i));        // s(i)가 가진 U 원소의 수
                if (tmp > n){
                    n = tmp;
                    idx = i;
                }
            }
            return f.get(idx);
        }

}
class MySet<T> extends HashSet<Integer> {
    public MySet(int... elements){
        for(Integer x : elements) add(x);
    }
}
