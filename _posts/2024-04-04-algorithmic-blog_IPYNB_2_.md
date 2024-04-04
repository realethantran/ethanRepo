---
title: Algorithmic Code Prep
author: Ethan Tran
toc: True
comments: True
layout: post
type: hacks
courses: {'csse': {'week': 1}, 'csp': {'week': 1, 'categories': ['4.A']}, 'csa': {'week': 0}, 'labnotebook': {'week': 3}}
---

## Learn All Sorts

### Bubble Sort

Bubble Sort is iteratively goes through the list, compares nearby elements, and switches items if necessary to keep them in the correct order. It is inefficient for large datasets, as it has an O(n^2) time complexity meaning that larger datasets mean more operations used to sort.


```Java
public class BubbleSort {
    public static void bubbleSort(int[] num) {
        int n = num.length;
        for (int i = 0; i < n-1; i++) {
            for (int j = 0; j < n-i-1; j++) {
                if (num[j] > num[j+1]) {
                    // swap num[j] and num[j+1]
                    int temp = num[j];
                    num[j] = num[j+1];
                    num[j+1] = temp;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] num = {1, 5, 3, 19, 1, 50, 23, 12};
        System.out.println("Array (before sort):");
        printAlgorithm(num);

        bubbleSort(num);

        System.out.println("Array (after sort):");
        printAlgorithm(num);
    }

    public static void printAlgorithm(int[] num) {
        for (int i = 0; i < num.length; i++) {
            System.out.print(num[i] + " ");
        }
        System.out.println();
    }
}
BubbleSort.main(null);
```

    Array (before sort):
    1 5 3 19 1 50 23 12 
    Array (after sort):
    1 1 3 5 12 19 23 50 


### Selection Sort

Selection sort splits the given list into two parts: sorted (at the beginning of the list) and the unsorted part falling after. The items start in the unsorted part while the sorted part is empty. The algorithm moves the smallest/maximum (depends on sort) element from the unsorted section to the end of the sorted part with each iteration.Its time complexity is O(n^2), meaning that it is inefficient for very large datasets but it can be helpful for tiny datasets.


```Java
public class SelectionSort {
    public static void SelectionSort(int[] num) {
        int n = num.length;
        for (int i = 0; i < n-1; i++) {
            int min_idx = i;
            for (int j = i+1; j < n; j++) {
                if (num[j] < num[min_idx]) {
                    min_idx = j;
                }
            }
            int temp = num[min_idx];
            num[min_idx] = num[i];
            num[i] = temp;
        }
    }

    public static void main(String[] args) {
        int[] num = {1, 5, 3, 19, 1, 50, 23, 12};
        System.out.println("Array (before sort):");
        printAlgorithm(num);

        SelectionSort(num);

        System.out.println("Array (after sort):");
        printAlgorithm(num);
    }

    public static void printAlgorithm(int[] num) {
        for (int i = 0; i < num.length; i++) {
            System.out.print(num[i] + " ");
        }
        System.out.println();
    }
}
SelectionSort.main(null);
```

    Array (before sort):
    1 5 3 19 1 50 23 12 
    Array (after sort):
    1 1 3 5 12 19 23 50 


### Insertion Sort

Insertion sort builds the final sorted Array one element at a time, iterating through the input Array and moving each element into the correct position through comparing it with elements to its left. It has a time complexity of O(n^2), making it inefficient with large Arrays, but it is efficient for small data sets or nearly sorted Arrays as it is adaptive to partially sorted Arrays, and space-efficient due to its in-place sorting nature.


```Java
public class InsertionSort {
    public static void InsertionSort(int[] num) {
        int n = num.length;
        for (int i = 1; i < n; i++) {
            int key = num[i];
            int j = i - 1;
            while (j >= 0 && num[j] > key) {
                num[j + 1] = num[j];
                j--;
            }
            num[j + 1] = key;
        }
    }
    public static void main(String[] args) {
        int[] num = {1, 5, 3, 19, 1, 50, 23, 12};
        System.out.println("Array (before sort):");
        printAlgorithm(num);

        InsertionSort(num);

        System.out.println("Array (after sort):");
        printAlgorithm(num);
    }

    public static void printAlgorithm(int[] num) {
        for (int i = 0; i < num.length; i++) {
            System.out.print(num[i] + " ");
        }
        System.out.println();
    }
}
InsertionSort.main(null);
```

    Array (before sort):
    1 5 3 19 1 50 23 12 
    Array (after sort):
    1 1 3 5 12 19 23 50 


### Merge Sort

Merge sort divides the input numay into smaller halves until each sub-numay contains a single element, then merges the smaller numays into the sorted order. It has a time complexity of O(n log n), which means that it is efficient even for large numays. 


```Java
public class MergeSort {
    public static void MergeSort(int[] num) {
        if (num.length > 1) {
            int mid = num.length / 2;
            int[] left = Arrays.copyOfRange(num, 0, mid);
            int[] right = Arrays.copyOfRange(num, mid, num.length);

            MergeSort(left);
            MergeSort(right);

            int i = 0, j = 0, k = 0;

            while (i < left.length && j < right.length) {
                if (left[i] < right[j]) {
                    num[k++] = left[i++];
                } else {
                    num[k++] = right[j++];
                }
            }

            while (i < left.length) {
                num[k++] = left[i++];
            }

            while (j < right.length) {
                num[k++] = right[j++];
            }
        }
    }
    public static void main(String[] args) {
        int[] num = {1, 5, 3, 19, 1, 50, 23, 12};
        System.out.println("Array (before sort):");
        printAlgorithm(num);

        MergeSort(num);

        System.out.println("Array (after sort):");
        printAlgorithm(num);
    }

    public static void printAlgorithm(int[] num) {
        for (int i = 0; i < num.length; i++) {
            System.out.print(num[i] + " ");
        }
        System.out.println();
    }
}
MergeSort.main(null);
```

    Array (before sort):
    1 5 3 19 1 50 23 12 
    Array (after sort):
    1 1 3 5 12 19 23 50 


### Quick Sort

Quick Sort splits the array based on a selected pivot element, in which elements smaller than the pivot are moved to its left, and larger elements to its right. This process continues until the entire array is sorted by sorting the sub-arrays before and after the pivot element. Quick Sort has an average time complexity of O(n log n), making it efficient for large arrays, but it could degrade to O(n^2) in a worst-case scenario. However, it is widely used due to its average-case performance and in-place sorting characteristic, making it memory-efficient.


```Java
public class QuickSort {
    public static void QuickSort(int[] num, int low, int high) {
        if (low < high) {
            int pi = partition(num, low, high);

            QuickSort(num, low, pi - 1);
            QuickSort(num, pi + 1, high);
        }
    }

    public static int partition(int[] num, int low, int high) {
        int pivot = num[high];
        int i = (low - 1);
        for (int j = low; j < high; j++) {
            if (num[j] < pivot) {
                i++;

                int temp = num[i];
                num[i] = num[j];
                num[j] = temp;
            }
        }

        int temp = num[i + 1];
        num[i + 1] = num[high];
        num[high] = temp;

        return i + 1;
    }

    public static void main(String[] args) {
        int[] num = {1, 5, 3, 19, 1, 50, 23, 12};
        System.out.println("Array (before sort):");
        printAlgorithm(num);

        QuickSort(num, 0, num.length - 1);

        System.out.println("Array (after sort):");
        printAlgorithm(num);
    }

    public static void printAlgorithm(int[] num) {
        for (int i = 0; i < num.length; i++) {
            System.out.print(num[i] + " ");
        }
        System.out.println();
    }
}
QuickSort.main(null);
```

    Array (before sort):
    1 5 3 19 1 50 23 12 
    Array (after sort):
    1 1 3 5 12 19 23 50 


### LinkedList Collection


```Java
class Node<T extends Comparable<T>> {
    T data;
    Node<T> next;

    public Node(T data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList<T extends Comparable<T>> {
    private Node<T> head;

    public LinkedList() {
        this.head = null;
    }

    public void add(T data) {
        Node<T> newNode = new Node<>(data);
        if (head == null) {
            head = newNode;
        } else {
            Node<T> current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }

    public void mergeSort() {
        head = mergeSort(head);
    }

    private Node<T> mergeSort(Node<T> h) {
        if (h == null || h.next == null) {
            return h;
        }

        Node<T> middle = getMiddle(h);
        Node<T> nextOfMiddle = middle.next;
        middle.next = null;

        Node<T> left = mergeSort(h);
        Node<T> right = mergeSort(nextOfMiddle);

        return merge(left, right);
    }

    private Node<T> merge(Node<T> left, Node<T> right) {
        Node<T> result = null;

        if (left == null)
            return right;
        if (right == null)
            return left;

        if (left.data.compareTo(right.data) <= 0) {
            result = left;
            result.next = merge(left.next, right);
        } else {
            result = right;
            result.next = merge(left, right.next);
        }

        return result;
    }

    private Node<T> getMiddle(Node<T> h) {
        if (h == null)
            return h;

        Node<T> fastPtr = h.next;
        Node<T> slowPtr = h;

        while (fastPtr != null) {
            fastPtr = fastPtr.next;
            if (fastPtr != null) {
                slowPtr = slowPtr.next;
                fastPtr = fastPtr.next;
            }
        }
        return slowPtr;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder("[");
        Node<T> current = head;
        while (current != null) {
            sb.append(current.data);
            if (current.next != null)
                sb.append(", ");
            current = current.next;
        }
        sb.append("]");
        return sb.toString();
    }
}

public class Main {
    public static void main(String[] args) {
        LinkedList<FlowerGroupMember> members = new LinkedList<>();
        members.add(new FlowerGroupMember("Alara", 1));
        members.add(new FlowerGroupMember("Abigail", 2));
        members.add(new FlowerGroupMember("Aditi", 3));
        members.add(new FlowerGroupMember("Yuri", 4));
        members.add(new FlowerGroupMember("Aditya", 5));
        members.add(new FlowerGroupMember("Jishnu", 6));
        members.add(new FlowerGroupMember("Ethan T", 7));
        members.add(new FlowerGroupMember("Alex", 8));
        members.add(new FlowerGroupMember("Tanvi", 9));
        members.add(new FlowerGroupMember("James", 10));
        members.add(new FlowerGroupMember("Anthony", 11));
        members.add(new FlowerGroupMember("Emaad", 12));
        members.add(new FlowerGroupMember("Tay", 13));
        members.add(new FlowerGroupMember("Krishiv", 13));
        members.add(new FlowerGroupMember("David", 14));

        System.out.println("Original List:");
        System.out.println(members);

        //  merge sort
        members.mergeSort();
        System.out.println("\nSorted List (Merge Sort):");
        System.out.println(members);
    }
}

class FlowerGroupMember implements Comparable<FlowerGroupMember> {
    private String name;
    private int number;

    public FlowerGroupMember(String name, int number) {
        this.name = name;
        this.number = number;
    }

    @Override
    public int compareTo(FlowerGroupMember other) {
        // compare members based on their numbers
        return Integer.compare(this.number, other.number);
    }

    @Override
    public String toString() {
        return "{\"name\": \"" + name + "\", \"number\": " + number + "}";
    }
}
Main.main(null);
```

    Original List:
    [{"name": "Alara", "number": 1}, {"name": "Abigail", "number": 2}, {"name": "Aditi", "number": 3}, {"name": "Yuri", "number": 4}, {"name": "Aditya", "number": 5}, {"name": "Jishnu", "number": 6}, {"name": "Ethan T", "number": 7}, {"name": "Alex", "number": 8}, {"name": "Tanvi", "number": 9}, {"name": "James", "number": 10}, {"name": "Anthony", "number": 11}, {"name": "Emaad", "number": 12}, {"name": "Tay", "number": 13}, {"name": "Krishiv", "number": 13}, {"name": "David", "number": 14}]
    
    Sorted List (Merge Sort):
    [{"name": "Alara", "number": 1}, {"name": "Abigail", "number": 2}, {"name": "Aditi", "number": 3}, {"name": "Yuri", "number": 4}, {"name": "Aditya", "number": 5}, {"name": "Jishnu", "number": 6}, {"name": "Ethan T", "number": 7}, {"name": "Alex", "number": 8}, {"name": "Tanvi", "number": 9}, {"name": "James", "number": 10}, {"name": "Anthony", "number": 11}, {"name": "Emaad", "number": 12}, {"name": "Tay", "number": 13}, {"name": "Krishiv", "number": 13}, {"name": "David", "number": 14}]


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with Merge Sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
