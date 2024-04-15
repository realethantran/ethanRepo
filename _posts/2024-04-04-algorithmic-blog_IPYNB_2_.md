---
title: Algorithmic Code Prep
author: Ethan Tran
toc: True
comments: True
layout: post
type: hacks
courses: {'csse': {'week': 1}, 'csp': {'week': 1, 'categories': ['4.A']}, 'csa': {'week': 0}, 'labnotebook': {'week': 3}}
---

## Learn All sorts

### bubble sort

bubble sort is iteratively goes through the list, compares nearby elements, and switches items if necessary to keep them in the correct order. It is inefficient for large datasets, as it has an O(n^2) time complexity meaning that larger datasets mean more operations used to sort.

### selection sort

selection sort splits the given list into two parts: sorted (at the beginning of the list) and the unsorted part falling after. The items start in the unsorted part while the sorted part is empty. The algorithm moves the smallest/maximum (depends on sort) element from the unsorted section to the end of the sorted part with each iteration.Its time complexity is O(n^2), meaning that it is inefficient for very large datasets but it can be helpful for tiny datasets.

### insertion sort

insertion sort builds the final sorted Array one element at a time, iterating through the input Array and moving each element into the correct position through comparing it with elements to its left. It has a time complexity of O(n^2), making it inefficient with large Arrays, but it is efficient for small data sets or nearly sorted Arrays as it is adaptive to partially sorted Arrays, and space-efficient due to its in-place sorting nature.

### merge sort

merge sort divides the input numay into smaller halves until each sub-numay contains a single element, then merges the smaller numays into the sorted order. It has a time complexity of O(n log n), which means that it is efficient even for large numays. 

### quick sort

quick sort splits the array based on a selected pivot element, in which elements smaller than the pivot are moved to its left, and larger elements to its right. This process continues until the entire array is sorted by sorting the sub-arrays before and after the pivot element. quick sort has an average time complexity of O(n log n), making it efficient for large arrays, but it could degrade to O(n^2) in a worst-case scenario. However, it is widely used due to its average-case performance and in-place sorting characteristic, making it memory-efficient.

### LinkedList Implementation / Flower Group Collection


```java
import java.util.ArrayList;
import java.util.List;

public class FlowerGroupMember {
    private String name;
    private int number;
    private String flowerType;

    public FlowerGroupMember(String name, int number, String flowerType) {
        this.name = name;
        this.number = number;
        this.flowerType = flowerType;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getNumber() {
        return number;
    }

    public void setNumber(int number) {
        this.number = number;
    }

    public String getFlowerType() {
        return flowerType;
    }

    public void setFlowerType(String flowerType) {
        this.flowerType = flowerType;
    }

    @Override
    public String toString() {
        return "FlowerGroupMember{" +
                "name='" + name + '\'' +
                ", number=" + number +
                ", flowerType='" + flowerType + '\'' +
                '}';
    }
}

public class Garden {
    private List<FlowerGroupMember> members;

    public Garden() {
        this.members = new ArrayList<>();
    }

    public void addMember(FlowerGroupMember member) {
        members.add(member);
    }

    public List<FlowerGroupMember> getMembers() {
        return members;
    }

    public void setMembers(List<FlowerGroupMember> members) {
        this.members = members;
    }

    @Override
    public String toString() {
        return "Garden{" +
                "members=" + members +
                '}';
    }
}

public class TestSort {
    // bubble sort
    public static void bubblesort(List<FlowerGroupMember> list) {
        int n = list.size();
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (list.get(j).getNumber() > list.get(j + 1).getNumber()) {
                    // swap list[j] and list[j+1]
                    FlowerGroupMember temp = list.get(j);
                    list.set(j, list.get(j + 1));
                    list.set(j + 1, temp);
                }
            }
        }
    }

    // selection sort
    public static void selectionsort(List<FlowerGroupMember> list) {
        int n = list.size();
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (list.get(j).getNumber() < list.get(minIndex).getNumber()) {
                    minIndex = j;
                }
            }
            // swap list[i] and list[minIndex]
            FlowerGroupMember temp = list.get(i);
            list.set(i, list.get(minIndex));
            list.set(minIndex, temp);
        }
    }

    // insertion sort
    public static void insertionsort(List<FlowerGroupMember> list) {
        int n = list.size();
        for (int i = 1; i < n; i++) {
            FlowerGroupMember key = list.get(i);
            int j = i - 1;
            while (j >= 0 && list.get(j).getNumber() > key.getNumber()) {
                list.set(j + 1, list.get(j));
                j = j - 1;
            }
            list.set(j + 1, key);
        }
    }

    // merge sort
    public static void mergesort(List<FlowerGroupMember> list, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            mergesort(list, left, mid);
            mergesort(list, mid + 1, right);
            merge(list, left, mid, right);
        }
    }

    private static void merge(List<FlowerGroupMember> list, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        List<FlowerGroupMember> leftList = new ArrayList<>();
        List<FlowerGroupMember> rightList = new ArrayList<>();

        for (int i = 0; i < n1; ++i) {
            leftList.add(list.get(left + i));
        }
        for (int j = 0; j < n2; ++j) {
            rightList.add(list.get(mid + 1 + j));
        }

        int i = 0, j = 0;
        int k = left;
        while (i < n1 && j < n2) {
            if (leftList.get(i).getNumber() <= rightList.get(j).getNumber()) {
                list.set(k, leftList.get(i));
                i++;
            } else {
                list.set(k, rightList.get(j));
                j++;
            }
            k++;
        }

        while (i < n1) {
            list.set(k, leftList.get(i));
            i++;
            k++;
        }

        while (j < n2) {
            list.set(k, rightList.get(j));
            j++;
            k++;
        }
    }

    // quick sort
    public static void quicksort(List<FlowerGroupMember> list, int low, int high) {
        if (low < high) {
            int pi = partition(list, low, high);
            quicksort(list, low, pi - 1);
            quicksort(list, pi + 1, high);
        }
    }

    private static int partition(List<FlowerGroupMember> list, int low, int high) {
        int pivot = list.get(high).getNumber();
        int i = (low - 1);
        for (int j = low; j < high; j++) {
            if (list.get(j).getNumber() < pivot) {
                i++;

                FlowerGroupMember temp = list.get(i);
                list.set(i, list.get(j));
                list.set(j, temp);
            }
        }

        FlowerGroupMember temp = list.get(i + 1);
        list.set(i + 1, list.get(high));
        list.set(high, temp);

        return i + 1;
    }
}

public class Main {
    public static void main(String[] args) {
        Garden garden = new Garden();

        garden.addMember(new FlowerGroupMember("Tanvi", 9, "Peony"));
        garden.addMember(new FlowerGroupMember("Yuri", 4, "Daisy"));
        garden.addMember(new FlowerGroupMember("Abigail", 2, "Tulip"));
        garden.addMember(new FlowerGroupMember("Aditya", 5, "Sunflower"));
        garden.addMember(new FlowerGroupMember("Alara", 1, "Rose"));
        garden.addMember(new FlowerGroupMember("Ethan T", 7, "Carnation"));
        garden.addMember(new FlowerGroupMember("David", 14, "Poppy"));
        garden.addMember(new FlowerGroupMember("James", 10, "Cherry Blossom"));
        garden.addMember(new FlowerGroupMember("Emaad", 12, "Freesia"));
        garden.addMember(new FlowerGroupMember("Tay", 13, "Gerbera"));
        garden.addMember(new FlowerGroupMember("Anthony", 11, "Dahlia"));
        garden.addMember(new FlowerGroupMember("Aditi", 3, "Lily"));
        garden.addMember(new FlowerGroupMember("Alex", 8, "Hydrangea"));
        garden.addMember(new FlowerGroupMember("Jishnu", 6, "Orchid"));
        garden.addMember(new FlowerGroupMember("Krishiv", 13, "Anemone"));

        System.out.println("Original Garden:");
        System.out.println(garden);

        // test bubble sort
        List<FlowerGroupMember> bubblesortedList = new ArrayList<>(garden.getMembers());
        TestSort.bubblesort(bubblesortedList);
        System.out.println("\nAfter bubble sort:");
        System.out.println(bubblesortedList);

        // test selection sort
        List<FlowerGroupMember> selectionsortedList = new ArrayList<>(garden.getMembers());
        TestSort.selectionsort(selectionsortedList);
        System.out.println("\nAfter selection sort:");
        System.out.println(selectionsortedList);

        // test insertion sort
        List<FlowerGroupMember> insertionsortedList = new ArrayList<>(garden.getMembers());
        TestSort.insertionsort(insertionsortedList);
        System.out.println("\nAfter insertion sort:");
        System.out.println(insertionsortedList);

        // test merge sort
        List<FlowerGroupMember> mergesortedList = new ArrayList<>(garden.getMembers());
        TestSort.mergesort(mergesortedList, 0, mergesortedList.size() - 1);
        System.out.println("\nAfter merge sort:");
        System.out.println(mergesortedList);

        // test quick sort
        List<FlowerGroupMember> quicksortedList = new ArrayList<>(garden.getMembers());
        TestSort.quicksort(quicksortedList, 0, quicksortedList.size() - 1);
        System.out.println("\nAfter quick sort:");
        System.out.println(quicksortedList);
    }
}
Main.main(null);
```

    Original Garden:
    Garden{members=[FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}, FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}, FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}, FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}, FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}, FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}, FlowerGroupMember{name='David', number=14, flowerType='Poppy'}, FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}, FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}, FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}, FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}, FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}, FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}, FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}, FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}]}
    
    After bubble sort:
    [FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}, FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}, FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}, FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}, FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}, FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}, FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}, FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}, FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}, FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}, FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}, FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}, FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}, FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}, FlowerGroupMember{name='David', number=14, flowerType='Poppy'}]
    
    After selection sort:
    [FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}, FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}, FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}, FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}, FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}, FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}, FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}, FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}, FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}, FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}, FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}, FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}, FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}, FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}, FlowerGroupMember{name='David', number=14, flowerType='Poppy'}]
    
    After insertion sort:
    [FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}, FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}, FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}, FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}, FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}, FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}, FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}, FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}, FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}, FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}, FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}, FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}, FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}, FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}, FlowerGroupMember{name='David', number=14, flowerType='Poppy'}]
    
    After merge sort:
    [FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}, FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}, FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}, FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}, FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}, FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}, FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}, FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}, FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}, FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}, FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}, FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}, FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}, FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}, FlowerGroupMember{name='David', number=14, flowerType='Poppy'}]
    
    After quick sort:
    [FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}, FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}, FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}, FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}, FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}, FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}, FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}, FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}, FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}, FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}, FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}, FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}, FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}, FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}, FlowerGroupMember{name='David', number=14, flowerType='Poppy'}]


### MergeSort with LinkedList


```java
public class FlowerGroupMember {
    private String name;
    private int number;
    private String flowerType;

    public FlowerGroupMember(String name, int number, String flowerType) {
        this.name = name;
        this.number = number;
        this.flowerType = flowerType;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getNumber() {
        return number;
    }

    public void setNumber(int number) {
        this.number = number;
    }

    public String getFlowerType() {
        return flowerType;
    }

    public void setFlowerType(String flowerType) {
        this.flowerType = flowerType;
    }

    @Override
    public String toString() {
        return "FlowerGroupMember{" +
                "name='" + name + '\'' +
                ", number=" + number +
                ", flowerType='" + flowerType + '\'' +
                '}';
    }
}

public class Node {
    public FlowerGroupMember data;
    public Node next;

    public Node(FlowerGroupMember data) {
        this.data = data;
        this.next = null;
    }
}

public class LinkedList {
    private Node head;

    public LinkedList() {
        this.head = null;
    }

    public void add(FlowerGroupMember data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }

    public void printList() {
        Node current = head;
        while (current != null) {
            System.out.println(current.data);
            current = current.next;
        }
    }

    public Node getHead() {
        return head;
    }

    public void setHead(Node head) {
        this.head = head;
    }
}

public class TestSort {
    // mrge sort for LinkedList
    public static Node mergeSort(Node head) {
        if (head == null || head.next == null) {
            return head;
        }

        Node middle = getMiddle(head);
        Node nextToMiddle = middle.next;

        middle.next = null;

        Node left = mergeSort(head);
        Node right = mergeSort(nextToMiddle);

        return merge(left, right);
    }

    private static Node merge(Node left, Node right) {
        Node result = null;

        if (left == null) {
            return right;
        }

        if (right == null) {
            return left;
        }

        if (left.data.getNumber() <= right.data.getNumber()) {
            result = left;
            result.next = merge(left.next, right);
        } else {
            result = right;
            result.next = merge(left, right.next);
        }

        return result;
    }

    private static Node getMiddle(Node head) {
        if (head == null) {
            return head;
        }

        Node slow = head;
        Node fast = head;

        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}

public class Main {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();

        list.add(new FlowerGroupMember("Tanvi", 9, "Peony"));
        list.add(new FlowerGroupMember("Yuri", 4, "Daisy"));
        list.add(new FlowerGroupMember("Abigail", 2, "Tulip"));
        list.add(new FlowerGroupMember("Aditya", 5, "Sunflower"));
        list.add(new FlowerGroupMember("Alara", 1, "Rose"));
        list.add(new FlowerGroupMember("Ethan T", 7, "Carnation"));
        list.add(new FlowerGroupMember("David", 14, "Poppy"));
        list.add(new FlowerGroupMember("James", 10, "Cherry Blossom"));
        list.add(new FlowerGroupMember("Emaad", 12, "Freesia"));
        list.add(new FlowerGroupMember("Tay", 13, "Gerbera"));
        list.add(new FlowerGroupMember("Anthony", 11, "Dahlia"));
        list.add(new FlowerGroupMember("Aditi", 3, "Lily"));
        list.add(new FlowerGroupMember("Alex", 8, "Hydrangea"));
        list.add(new FlowerGroupMember("Jishnu", 6, "Orchid"));
        list.add(new FlowerGroupMember("Krishiv", 13, "Anemone"));

        System.out.println("Original List:");
        list.printList();

        Node sortedList = TestSort.mergeSort(list.getHead());

        System.out.println("\nAfter Merge Sort:");
        LinkedList sortedLinkedList = new LinkedList();
        sortedLinkedList.setHead(sortedList);
        sortedLinkedList.printList();
    }
}
Main.main(null);
```

    Original List:
    FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}
    FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}
    FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}
    FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}
    FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}
    FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}
    FlowerGroupMember{name='David', number=14, flowerType='Poppy'}
    FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}
    FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}
    FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}
    FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}
    FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}
    FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}
    FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}
    FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}
    
    After Merge Sort:
    FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}
    FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}
    FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}
    FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}
    FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}
    FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}
    FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}
    FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}
    FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}
    FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}
    FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}
    FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}
    FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}
    FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}
    FlowerGroupMember{name='David', number=14, flowerType='Poppy'}


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with merge sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
