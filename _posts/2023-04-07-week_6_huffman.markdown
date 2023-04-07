2023-04-07-week_6_huffman.markdown

import java.util.*;

public class week_6_3 {
    public static void main(String[] args) {
       /* Node a = new Node('a', 450);
        Node t = new Node('t', 90);
        Node g = new Node('g', 120);
        Node c = new Node('c', 270);*/

        PriorityQueue<Node> queue = new PriorityQueue<Node>();
        queue.add(new Node('a', 450));
        queue.add(new Node('t', 90));
        queue.add(new Node('g', 120));
        queue.add(new Node('c', 270));

        while(queue.size() >= 2){
            Node x = queue.remove();
            Node y = queue.remove();
            Node z = new Node(' ', x.freq + y.freq);
            z.add(x);
            z.add(y);
            queue.add(z);
        }

        Node root = queue.remove();
        traverse(root);

    }

    public static void traverse(Node root){
        traverse(root, 0, "");
    }

    public static void traverse(Node root, int nTap, String code){
        for(int i=0 ; i<nTap  ; i++) System.out.print("\t");
        root.code = code;
        System.out.println(root);
        int k=0;
        for (Node x : root) {
            traverse(x,nTap+1, String.format("%s", x.code +k));
            k+=1;
        }
    }

}

class Node extends TreeSet<Node> implements Comparable<Node>{
    char alphabet;
    int freq;
    String code = "";
    public Node(char alpha, int freq){
        this.alphabet = alpha;
        this.freq = freq;
    }
    @Override
    public int compareTo(Node o){
        return this.freq - o.freq;
    }
    @Override
    public String toString(){
        return String.format("%c%d[%s]", alphabet, freq, code);
    }
}