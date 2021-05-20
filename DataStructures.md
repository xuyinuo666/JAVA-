# 线性结构



# 环形数组队列

```java
public class CircleArr {
    public static void main(String[] args) {
        clirclearrtest clirclearrtest = new clirclearrtest(5);
        try {
            clirclearrtest.add(6);
            clirclearrtest.add(6);
            clirclearrtest.add(6);
            clirclearrtest.add(6);
            clirclearrtest.add(6);

        } catch (Exception e) {
            e.printStackTrace();
        }
        clirclearrtest.datas();
        clirclearrtest.show();


    }
}


class clirclearrtest {
    private int front;
    private int rear;
    private int maxsize;
    private int[] arr;

    public clirclearrtest(int maxsize) {
        this.front = 0;
        this.rear = 0;
        this.maxsize = ++maxsize; //默认需要牺牲一个位置
        arr = new int[this.maxsize];
    }

    public boolean isEmp() {
        return front == rear;
    }

    public boolean isFull() {
        return (rear+1) % (maxsize) == front; //判断数组满了的情况 rear 在 front 的后面一个位置就是满了,但是要取余,rear可能会超过front.
    }

    public void show() {
        for (int i = front; i < front + datas(); i++) { //从front开始遍历
            System.out.println(arr[i % maxsize]);
        }
        System.out.println("有效个数"+datas());
    }

    public int datas() {
        return (maxsize - front + rear) % maxsize; //取出有效个数
    }

    public void add(int x) {
        if (isFull()) {
            throw new RuntimeException("满了~~");
        }
        arr[rear] = x;
        rear = (rear + 1) % maxsize; //将rear指针后移,也要取余,不然超过maxsize
    }

    public int select(int x) {
        return arr[x];
    }

    public void delete() {
        front = (front + 1) % maxsize; //将 front指针后移
    }
}

```



# LinkedList



数据1中的属性有个person,指向下一个的person,所以person类中就有个person属性.当这个属性为空时,就到了结尾

```java
public class LinkedListTest {
    public static void main(String[] args) {
        heroMethod heroMethod = new heroMethod();

        hero o3 = new hero("lwj", 32);
        hero o33 = new hero("lwj", 44);
        hero o5 = new hero("lwj3", 2);
        hero o51 = new hero("lwj3", 1);
        hero o41 = new hero("l334", 5);
        hero o42 = new hero("l334", 53);
        hero o4 = new hero("l334", 3);

        heroMethod.addhero(o3);
        heroMethod.addhero(o33);
        heroMethod.addhero(o4);
        heroMethod.addhero(o41);
        heroMethod.addhero(o42);
        heroMethod.addhero(o5);
        heroMethod.addhero(o51);
        heroMethod.show();
    }

}

class heroMethod {
    private hero herohead = new hero("", 0);
    hero helper1=herohead;
    void addhero(hero hero) {
        hero helper = herohead;
        while (true) {
            if (helper.getNext() == null) {
                break;
            } else if (helper.getNext().getId() > hero.getId()) {
                break;
            }
            helper = helper.getNext();
        }
        hero.setNext(helper.getNext());
        helper.setNext(hero);
    }

    void show() {
        helper1 = herohead;
        boolean flag = true;
        while (flag) {
            if (helper1.getNext() == null) break;
            System.out.println(helper1.getNext());
            helper1 = helper1.getNext();
        }
    }
}

class hero {
    private String name;
    private int id;
    private hero next;

    public hero() {
    }

    public hero(String name, int id) {
        this.name = name;
        this.id = id;
    }

    @Override
    public String toString() {
        return "hero{" +
                "name='" + name + '\'' +
                ", id=" + id +
                "" +
                '}';
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public hero getNext() {
        return next;
    }

    public void setNext(hero next) {
        this.next = next;
    }
}

```

# CircleLinkedList

```java
class CircleLinkedList {

    //创建头指针
    private person first = null;
    //定义一个辅助指针
    person temp = null;

    void addperson(int nums) {
        for (int i = 1; i <= nums; i++) {
            person p = new person(i);
            if (i == 1) {
                first = p;
                temp = first;
            } else {
                temp.nextPer = p;
                temp = p;
                temp.nextPer = first;
            }
        }
    }

    void show() {
        temp=first;
        while (true) {
            System.out.println(temp.getNo());
            temp = temp.nextPer;
            if (temp==first)
                break;
        }
    }
    class person {

        private int no;
        public person nextPer;

        public person(int no) {

            this.no = no;

        }


        public void setNo(int no) {
            this.no = no;
        }


        public int getNo() {
            return no;
        }


        public person getNextPer() {
            return nextPer;
        }

        public void setNextPer(person nextPer) {
            this.nextPer = nextPer;
        }

        @Override
        public String toString() {
            return "person{" +
                    ", no=" + no +
                    '}';
        }
    }
}

class test {
    public static void main(String[] args) {
        CircleLinkedList circleLinkedList = new CircleLinkedList();
        circleLinkedList.addperson(25);
        circleLinkedList.show();
    }
}


```

# 递归

```
public class migong {
    public static void main(String[] args) {
        mogongMethod m = new mogongMethod();
        int[][] m1=new int[10][10];
        for (int i = 0; i < 8; i++) {
            m1[3][i]=1;
        }
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 10; j++) {
                m1[0][j]=1;
                m1[9][j]=1;
                m1[i][0]=1;
                m1[i][9]=1;
            }
        }
        m.go(m1,1,1);
    }
}
class mogongMethod {
    public mogongMethod() {

    }
    boolean go(int[][] map, int x, int y) {
        if (map[1][8] == 2) {
            for (int i = 0; i < 10; i++) {
                for (int j = 0; j < 10; j++) {
                    System.out.print(map[i][j]+" ");
                }
                System.out.println();
            }
            return true;
        } else {
            if (map[x][y] == 0) {
                map[x][y] = 2;
                if (go(map, x + 1, y)) {
                    return true;
                } else if (go(map, x, y + 1)) {
                    return true;
                } else if (go(map, x - 1, y)) {
                    return true;
                } else if (go(map, x, y - 1)) {
                    return true;
                } else {
                    map[x][y]=3;
                    return false;
                }
            }else return false;


        }
    }

}

```

# 二分查找

```
package find;

public class DubbleFind {
    public static void main(String[] args) {
        int[] ints = new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9};
        DubbleMethod dubbleMethod = new DubbleMethod(ints, 5);
        int i = dubbleMethod.find(0, ints.length - 1);
        System.out.println(i);
    }
}

class DubbleMethod {
    private int[] x;
    private int find;
    private int mid;
    private int index = -1;
    private int start;
    private int end;

    public DubbleMethod(int[] x, int find) {
        this.x = x;
        this.find = find;
        this.mid = x.length / 2;
    }

    int find(int start, int end) {
        if (start > end) {
            return index;
        }
        if (x[mid] == find) {
            index = mid;
            return index;
        } else if (x[mid] > find) {
            end = mid - 1;
            mid = (end + start) / 2;
            return find(start, end);
        } else {
            start = mid + 1;
            mid = (end + start) / 2;
            return find(start, end);
        }
    }

}
```

# 斐波那契数列

```
package SuanFa;

public class FeiBo {
    public static void main(String[] args) {
        FeiBoMethod feiBoMethod = new FeiBoMethod();
        System.out.println(feiBoMethod.add(7));

    }
}
class FeiBoMethod{
    int add(int x){
        if (x==1||x==2){
            return 1;
        }else{
            return add(x-1)+add(x-2);
        }
    }
}
```

# 汉诺塔

```
package SuanFa;

public class HanNuo {
    public static void main(String[] args) {
        HanMethod hanMethod = new HanMethod();
        hanMethod.move(2,'a','b','c');
    }
}
class HanMethod{
    void move(int x,char from,char in,char to){
        if (x==1){
            System.out.println("将第1个从"+from+"移动到"+to);
        }
        else {
            move(x-1,from,to,in);
            System.out.println("将第"+x+"个从"+from+"移动到"+to);
            move(x-1,in,from,to);
        }

    }
}

```

# 排序算法

==插入排序==

遍历数组，遇到比前一个数小时，记录这个数，互换位置，然后向前遍历，直到比前位置数大，比后位置数小为止。

==快速==

选定第一个数为基准，记录这个数，最左索引i ，最右索引j ，先从j向前遍历 ，遍历到比基准数小的数将这个数赋给i ，此时i向右遍历，直到这个数比基准数大，将i赋给j，循环操作，当i=j时停止，再将i之前的 和之后的再次执行操作。

==选择==

当数组第二个数像后遍历，遇到比前一个数小互换位置，再向前比较，直到合适的位置。

==归并==

将数组递归执行二分，两个两个比较，一个数组中的分别有一个索引，索引指向小的数放入数组，将索引向后，两个数组合并成一个，再参与下次排序



## 冒泡排序

```
package PaiXu;

public class MaoPao {
    public static void main(String[] args) {
        int[] ints = {3, 4, 56, 6, 7, 7, 2, 234, 5};
        MaoPaoMethod maoPaoMethod = new MaoPaoMethod(ints);
        maoPaoMethod.go();
    }
}
class MaoPaoMethod{
    private int[] x;

    public MaoPaoMethod(int[] x) {
        this.x = x;
    }
    void go(){
        for (int i = 0; i < x.length - 1; i++) {
            for (int j = 0; j < x.length - i - 1; j++) {
                if (x[j]>x[j+1]){
                    int temp=x[j];
                    x[j]=x[j+1];
                    x[j+1]=temp;
                }
            }
        }
        for (int i = 0; i < x.length; i++) {
            System.out.println(x[i]);
        }
    }
}
```

## 快速排序

```
package PaiXu;

public class KuaiSu {
    public static void main(String[] args) {
        KuaiSuMethod kuaiSuMethod = new KuaiSuMethod();
        int [] x={2,5,1,6,4,44,56,5,7,43,22,32};
        kuaiSuMethod.go(x,0,x.length-1);
        for (int i = 0; i < x.length; i++) {
            System.out.println(x[i]);
        }
    }
}

class KuaiSuMethod {
    void go(int[] x,int start ,int end) {
        if (start < end) {
            int stard = x[start];
            int low = start;
            int high = end;
            while (low < high) {
                while (low < high && x[high] >= stard) {
                    high--;
                }
                x[low] = x[high];

                while (low < high && x[low] <= stard) {
                    low++;
                }
                x[high] = x[low];


            }
            x[low] = stard;
            go(x, start, low);
            go(x, low + 1, end);
        }
    }
}
```

## 插入排序

==每一个元素都向后比较

```
package PaiXu;

import java.util.Arrays;

public class InsertPaiXu {
    public static void main(String[] args) {
        InserMethod inserMethod = new InserMethod();
        int [] x={4,5,2,33,4,5,44,54,31,40,5,1,6,7,8,4};
        inserMethod.paixu(x);

    }
}

class InserMethod {

    void paixu(int[] x) {
        for (int i = 1; i < x.length ; i++) {
            if (x[i] < x[i - 1]) {
                int temp = x[i];
                int j;
                for (j = i - 1; j >= 0 && temp < x[j]; j--) {
                        x[j+1] = x[j];
                }
                x[j+1]=temp;
            }
        }
        System.out.println(Arrays.toString(x));
    }
}
```

## 希尔排序

```
package PaiXu;

import java.util.Arrays;

public class Share {
    public static void main(String[] args) {
        int[] x = {5, 3, 6, 8, 2, 9, 4, 7, 5, 2, 1};
        ShareMethod shareMethod = new ShareMethod();
        shareMethod.paixu(x);
        System.out.println(Arrays.toString(x));
    }
}

class ShareMethod {
    void paixu(int[] x) {
        //定义步长
        for (int i = x.length / 2; i >= 1; i = i / 2) {
            //遍历所有的元素,从i开始
            for (int l = i; l < x.length; l++) {
                //将i之前的也遍历
                for (int j = l-i; j >= 0; j -= i) {
                    if (x[j] > x[j + i]) {
                        int temp = x[j + 1];
                        x[j + 1] = x[j];
                        x[j] = temp;
                    }
                }
            }
        }
    }
}
```

## 选择排序

```
package PaiXu;

import java.util.Arrays;

public class XuanZe {
    public static void main(String[] args) {
        int[] x = {5, 3, 6, 8, 2, 9, 4, 7, 5, 2, 1,66,44,55,21,767,4543,23,5,7};
        XuanZeMethod xuanZeMethod = new XuanZeMethod();
        xuanZeMethod.go(x);
        System.out.println(Arrays.toString(x));
    }
}
class XuanZeMethod{
    void go(int [] x){
        for (int i = 0; i < x.length - 2; i++) {
            for (int j = i+1; j < x.length; j++) {
                if (x[i]>x[j]){
                    int temp=x[j];
                    x[j]=x[i];
                    x[i]=temp;
                }
            }
        }

    }
}

```

## 归并排序

```
package PaiXu;

import java.util.Arrays;

public class GuiBing {
    public static void main(String[] args) {
        int[] x = {6, 5, 4, 3, 2, 1};
        GuiBingMethod guiBingMethod = new GuiBingMethod();
//        guiBingMethod.Fen(x, 0, x.length - 1);
        guiBingMethod.Fen(x, 0, x.length - 1);
        System.out.println(Arrays.toString(x));
    }
}


class GuiBingMethod {
    void Fen(int[] x, int start, int end) {
        int mid = (end + start) / 2;
//        System.out.println(mid);
        if (start < end) {
            Fen(x, start, mid);
            Fen(x, mid + 1, end);
            go(x, start, mid, end);
        }
    }

    //将整个数组传入进来,但是指针的位置不同,就像传入多个数组
    void go(int[] x, int start, int mid, int end) {
        int i = start;
        int ii = mid + 1;////第二个数组的起始位置
        int iii = 0;
        int[] temp = new int[end - start + 1];
        while (i <= mid && ii <= end) {

            if (x[i] <= x[ii]) {
                temp[iii] = x[i];
                i++;
            } else {
                temp[iii] = x[ii];
                ii++;
            }
            iii++;
        }

        while (i <= mid) {
            temp[iii] = x[i];
            i++;
            iii++;
        }
        while (ii <= end) {
            temp[iii] = x[ii];
            ii++;
            iii++;
        }

        for (int j = 0; j < temp.length; j++) {
            x[j + start] = temp[j];
        }
    }
}

```

## 基数排序

# Hash表

```
class HashTab {
    public static void main(String[] args) {
        LinkedArr linkedArr = new LinkedArr(10);
        Emp emp = new Emp();
        Emp emp2 = new Emp();
        emp.setName("xgw");
        emp.setId(1);
        emp2.setName("lwj");
        emp2.setId(11);
        linkedArr.add(emp);
        linkedArr.add(emp2);
        linkedArr.show(1);
    }
}

class LinkedArr {
    private int size;
    private EmpLinked[] empLinked;

    public LinkedArr(int size) {
        this.size = size;
        empLinked = new EmpLinked[size];
        for (int i = 0; i < size; i++) {
            empLinked[i] = new EmpLinked();
        }
    }

    void add(Emp emp) {
        empLinked[emp.getId() % 10].add(emp);
    }
    

    void show(int id) {
        for (int i = 0; i < size - 1; i++) {
            empLinked[i].show();
        }
    }
}

class EmpLinked {
    Emp head;
    Emp help;

    void add(Emp emp) {
        if (head == null) {
            head = emp;
            return;
        } else {
            help = head;
            while (help.getNext() != null) {
                help = help.getNext();
            }
            help.setNext(emp);
        }
    }

    void show() {
        help = head;
        while (help != null) {
            System.out.print(help.getName());
            help = help.getNext();
        }
    }
}

class Emp {
    private int id;
    private String name;
    private Emp next;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Emp getNext() {
        return next;
    }

    public void setNext(Emp next) {
        this.next = next;
    }

    @Override
    public String toString() {
        return "Emp{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", next=" + next +
                '}';
    }
}
```

# 树

1. 根节点：第一个节点
2. 子节点：上面有节点，下面有节点的节点
3. 双亲节点：下面有节点的节点
4. 路径：连接
5. 节点的度：有几个子节点
6. 节点的权：节点的值
7. 叶子节点：上面有节点的节点
8. 子树：树中的树
9. 层：树层

## 二叉树

==任何一个节点的子节点数量都不超过2，左右节点不能颠倒。视为不同的树==

### 满二叉树

所有的叶子节点都在最后一层，节点总数=2的n次方-1，n是树的高度

### 完全二叉树

首先应该是二叉树

所有叶子节点都在最后一层或者倒数第二层。倒数第一次层必须从左边连续，倒数第二层从右至左连续。

==从上到下，从左至右，能数的过来==中间不能有空隙。

### 顺序存储二叉树

通常只考虑完全二叉树

第n个节点的左子节点：2*n+1

第n个节点的右子节点：2*n+2

第n个节点的父节点：(n-1)/2



## 线索二叉树

前驱，后继节点

## 赫夫曼树

权值*路径值最小

## 赫夫曼编码

赫夫曼树存储数据

## 二叉排序树

比根节点小在左，比根节点大在右

## 平衡二叉树

左子树的高度和右子树的高度差不超过1