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

### Selection Sort

Selection sort splits the given list into two parts: sorted (at the beginning of the list) and the unsorted part falling after. The items start in the unsorted part while the sorted part is empty. The algorithm moves the smallest/maximum (depends on sort) element from the unsorted section to the end of the sorted part with each iteration.Its time complexity is O(n^2), meaning that it is inefficient for very large datasets but it can be helpful for tiny datasets.

### Insertion Sort

Insertion sort builds the final sorted Array one element at a time, iterating through the input Array and moving each element into the correct position through comparing it with elements to its left. It has a time complexity of O(n^2), making it inefficient with large Arrays, but it is efficient for small data sets or nearly sorted Arrays as it is adaptive to partially sorted Arrays, and space-efficient due to its in-place sorting nature.

### Merge Sort

Merge sort divides the input numay into smaller halves until each sub-numay contains a single element, then merges the smaller numays into the sorted order. It has a time complexity of O(n log n), which means that it is efficient even for large numays. 

### Quick Sort

Quick Sort splits the array based on a selected pivot element, in which elements smaller than the pivot are moved to its left, and larger elements to its right. This process continues until the entire array is sorted by sorting the sub-arrays before and after the pivot element. Quick Sort has an average time complexity of O(n log n), making it efficient for large arrays, but it could degrade to O(n^2) in a worst-case scenario. However, it is widely used due to its average-case performance and in-place sorting characteristic, making it memory-efficient.

### LinkedList Implementation / Flower Group Collection


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

    public LinkedList(LinkedList<T> list) {
        this.head = null;
        Node<T> current = list.head;
        while (current != null) {
            add(current.data);
            current = current.next;
        }
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

    // bubble Sort
    public void bubbleSort() {
        boolean swapped;
        Node<T> current;
        Node<T> lastSorted = null;

        do {
            swapped = false;
            current = head;

            while (current.next != lastSorted) {
                if (current.data.compareTo(current.next.data) > 0) {
                    T temp = current.data;
                    current.data = current.next.data;
                    current.next.data = temp;
                    swapped = true;
                }
                current = current.next;
            }
            lastSorted = current;
        } while (swapped);
    }

    // selection Sort
    public void selectionSort() {
        Node<T> current = head;
        while (current != null) {
            Node<T> min = current;
            Node<T> nextNode = current.next;
            while (nextNode != null) {
                if (nextNode.data.compareTo(min.data) < 0) {
                    min = nextNode;
                }
                nextNode = nextNode.next;
            }
            T temp = current.data;
            current.data = min.data;
            min.data = temp;
            current = current.next;
        }
    }

    // insertion Sort
    public void insertionSort() {
        if (head == null || head.next == null) {
            return;
        }

        Node<T> sorted = null;
        Node<T> current = head;

        while (current != null) {
            Node<T> next = current.next;
            if (sorted == null || sorted.data.compareTo(current.data) > 0) {
                current.next = sorted;
                sorted = current;
            } else {
                Node<T> temp = sorted;
                while (temp.next != null && temp.next.data.compareTo(current.data) < 0) {
                    temp = temp.next;
                }
                current.next = temp.next;
                temp.next = current;
            }
            current = next;
        }

        head = sorted;
    }

    // merge Sort
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

    // quick Sort
    public void quickSort() {
        head = quickSort(head);
    }

    private Node<T> quickSort(Node<T> node) {
        if (node == null || node.next == null)
            return node;

        T pivot = node.data;
        Node<T> lessThanPivotHead = null;
        Node<T> lessThanPivotTail = null;
        Node<T> equalToPivotHead = null;
        Node<T> equalToPivotTail = null;
        Node<T> greaterThanPivotHead = null;
        Node<T> greaterThanPivotTail = null;

        while (node != null) {
            if (node.data.compareTo(pivot) < 0) {
                if (lessThanPivotHead == null) {
                    lessThanPivotHead = lessThanPivotTail = node;
                } else {
                    lessThanPivotTail.next = node;
                    lessThanPivotTail = lessThanPivotTail.next;
                }
            } else if (node.data.compareTo(pivot) == 0) {
                if (equalToPivotHead == null) {
                    equalToPivotHead = equalToPivotTail = node;
                } else {
                    equalToPivotTail.next = node;
                    equalToPivotTail = equalToPivotTail.next;
                }
            } else {
                if (greaterThanPivotHead == null) {
                    greaterThanPivotHead = greaterThanPivotTail = node;
                } else {
                    greaterThanPivotTail.next = node;
                    greaterThanPivotTail = greaterThanPivotTail.next;
                }
            }
            node = node.next;
        }

        if (lessThanPivotTail != null) lessThanPivotTail.next = null;
        if (equalToPivotTail != null) equalToPivotTail.next = null;
        if (greaterThanPivotTail != null) greaterThanPivotTail.next = null;

        Node<T> sorted = null;
        if (lessThanPivotHead != null) {
            lessThanPivotHead = quickSort(lessThanPivotHead);
            sorted = concatLists(sorted, lessThanPivotHead);
        }
        if (equalToPivotHead != null) {
            equalToPivotTail.next = quickSort(equalToPivotHead.next);
            sorted = concatLists(sorted, equalToPivotHead);
        }
        if (greaterThanPivotHead != null) {
            greaterThanPivotHead = quickSort(greaterThanPivotHead);
            sorted = concatLists(sorted, greaterThanPivotHead);
        }
        return sorted;
    }

    private Node<T> concatLists(Node<T> list1, Node<T> list2) {
        if (list1 == null)
            return list2;
        Node<T> current = list1;
        while (current.next != null) {
            current = current.next;
        }
        current.next = list2;
        return list1;
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
        members.add(new FlowerGroupMember("Alara", 1, "Rose"));
        members.add(new FlowerGroupMember("Abigail", 2, "Tulip"));
        members.add(new FlowerGroupMember("Aditi", 3, "Lily"));
        members.add(new FlowerGroupMember("Yuri", 4, "Daisy"));
        members.add(new FlowerGroupMember("Aditya", 5, "Sunflower"));
        members.add(new FlowerGroupMember("Jishnu", 6, "Orchid"));
        members.add(new FlowerGroupMember("Ethan T", 7, "Carnation"));
        members.add(new FlowerGroupMember("Alex", 8, "Hydrangea"));
        members.add(new FlowerGroupMember("Tanvi", 9, "Peony"));
        members.add(new FlowerGroupMember("James", 10, "Cherry Blossom"));
        members.add(new FlowerGroupMember("Anthony", 11, "Dahlia"));
        members.add(new FlowerGroupMember("Emaad", 12, "Freesia"));
        members.add(new FlowerGroupMember("Tay", 13, "Gerbera"));
        members.add(new FlowerGroupMember("Krishiv", 13, "Anemone"));
        members.add(new FlowerGroupMember("David", 14, "Poppy"));

        System.out.println("Original List:");
        System.out.println(members);

        // bubble Sort
        LinkedList<FlowerGroupMember> bubbleSortedList = new LinkedList<>(members);
        bubbleSortedList.bubbleSort();
        System.out.println("\nSorted List using Bubble Sort:");
        System.out.println(bubbleSortedList);

        // selection Sort
        LinkedList<FlowerGroupMember> selectionSortedList = new LinkedList<>(members);
        selectionSortedList.selectionSort();
        System.out.println("\nSorted List using Selection Sort:");
        System.out.println(selectionSortedList);

        // Insertion Sort
        LinkedList<FlowerGroupMember> insertionSortedList = new LinkedList<>(members);
        insertionSortedList.insertionSort();
        System.out.println("\nSorted List using Insertion Sort:");
        System.out.println(insertionSortedList);

        // merge Sort
        LinkedList<FlowerGroupMember> mergeSortedList = new LinkedList<>(members);
        mergeSortedList.mergeSort();
        System.out.println("\nSorted List using Merge Sort:");
        System.out.println(mergeSortedList);

        // quick Sort
        LinkedList<FlowerGroupMember> quickSortedList = new LinkedList<>(members);
        quickSortedList.quickSort();
        System.out.println("\nSorted List using Quick Sort:");
        System.out.println(quickSortedList);
    }
}

class FlowerGroupMember implements Comparable<FlowerGroupMember> {
    protected String name;
    protected int number;
    protected String flower;

    public FlowerGroupMember(String name, int number, String flower) {
        this.name = name;
        this.number = number;
        this.flower = flower;
    }

    @Override
    public int compareTo(FlowerGroupMember other) {
        // compare FlowerGroupMembers alphabetically by name
        return this.name.compareTo(other.name);
    }

    @Override
    public String toString() {
        return "{\"name\": \"" + name + "\", \"number\": " + number + ", \"flower\": \"" + flower + "\"}";
    }
}
Main.main(null);
```

    Original List:
    [{"name": "Alara", "number": 1, "flower": "Rose"}, {"name": "Abigail", "number": 2, "flower": "Tulip"}, {"name": "Aditi", "number": 3, "flower": "Lily"}, {"name": "Yuri", "number": 4, "flower": "Daisy"}, {"name": "Aditya", "number": 5, "flower": "Sunflower"}, {"name": "Jishnu", "number": 6, "flower": "Orchid"}, {"name": "Ethan T", "number": 7, "flower": "Carnation"}, {"name": "Alex", "number": 8, "flower": "Hydrangea"}, {"name": "Tanvi", "number": 9, "flower": "Peony"}, {"name": "James", "number": 10, "flower": "Cherry Blossom"}, {"name": "Anthony", "number": 11, "flower": "Dahlia"}, {"name": "Emaad", "number": 12, "flower": "Freesia"}, {"name": "Tay", "number": 13, "flower": "Gerbera"}, {"name": "Krishiv", "number": 13, "flower": "Anemone"}, {"name": "David", "number": 14, "flower": "Poppy"}]
    
    Sorted List using Bubble Sort:
    [{"name": "Abigail", "number": 2, "flower": "Tulip"}, {"name": "Aditi", "number": 3, "flower": "Lily"}, {"name": "Aditya", "number": 5, "flower": "Sunflower"}, {"name": "Alara", "number": 1, "flower": "Rose"}, {"name": "Alex", "number": 8, "flower": "Hydrangea"}, {"name": "Anthony", "number": 11, "flower": "Dahlia"}, {"name": "David", "number": 14, "flower": "Poppy"}, {"name": "Emaad", "number": 12, "flower": "Freesia"}, {"name": "Ethan T", "number": 7, "flower": "Carnation"}, {"name": "James", "number": 10, "flower": "Cherry Blossom"}, {"name": "Jishnu", "number": 6, "flower": "Orchid"}, {"name": "Krishiv", "number": 13, "flower": "Anemone"}, {"name": "Tanvi", "number": 9, "flower": "Peony"}, {"name": "Tay", "number": 13, "flower": "Gerbera"}, {"name": "Yuri", "number": 4, "flower": "Daisy"}]
    
    Sorted List using Selection Sort:
    [{"name": "Abigail", "number": 2, "flower": "Tulip"}, {"name": "Aditi", "number": 3, "flower": "Lily"}, {"name": "Aditya", "number": 5, "flower": "Sunflower"}, {"name": "Alara", "number": 1, "flower": "Rose"}, {"name": "Alex", "number": 8, "flower": "Hydrangea"}, {"name": "Anthony", "number": 11, "flower": "Dahlia"}, {"name": "David", "number": 14, "flower": "Poppy"}, {"name": "Emaad", "number": 12, "flower": "Freesia"}, {"name": "Ethan T", "number": 7, "flower": "Carnation"}, {"name": "James", "number": 10, "flower": "Cherry Blossom"}, {"name": "Jishnu", "number": 6, "flower": "Orchid"}, {"name": "Krishiv", "number": 13, "flower": "Anemone"}, {"name": "Tanvi", "number": 9, "flower": "Peony"}, {"name": "Tay", "number": 13, "flower": "Gerbera"}, {"name": "Yuri", "number": 4, "flower": "Daisy"}]
    
    Sorted List using Insertion Sort:
    [{"name": "Abigail", "number": 2, "flower": "Tulip"}, {"name": "Aditi", "number": 3, "flower": "Lily"}, {"name": "Aditya", "number": 5, "flower": "Sunflower"}, {"name": "Alara", "number": 1, "flower": "Rose"}, {"name": "Alex", "number": 8, "flower": "Hydrangea"}, {"name": "Anthony", "number": 11, "flower": "Dahlia"}, {"name": "David", "number": 14, "flower": "Poppy"}, {"name": "Emaad", "number": 12, "flower": "Freesia"}, {"name": "Ethan T", "number": 7, "flower": "Carnation"}, {"name": "James", "number": 10, "flower": "Cherry Blossom"}, {"name": "Jishnu", "number": 6, "flower": "Orchid"}, {"name": "Krishiv", "number": 13, "flower": "Anemone"}, {"name": "Tanvi", "number": 9, "flower": "Peony"}, {"name": "Tay", "number": 13, "flower": "Gerbera"}, {"name": "Yuri", "number": 4, "flower": "Daisy"}]
    
    Sorted List using Merge Sort:
    [{"name": "Abigail", "number": 2, "flower": "Tulip"}, {"name": "Aditi", "number": 3, "flower": "Lily"}, {"name": "Aditya", "number": 5, "flower": "Sunflower"}, {"name": "Alara", "number": 1, "flower": "Rose"}, {"name": "Alex", "number": 8, "flower": "Hydrangea"}, {"name": "Anthony", "number": 11, "flower": "Dahlia"}, {"name": "David", "number": 14, "flower": "Poppy"}, {"name": "Emaad", "number": 12, "flower": "Freesia"}, {"name": "Ethan T", "number": 7, "flower": "Carnation"}, {"name": "James", "number": 10, "flower": "Cherry Blossom"}, {"name": "Jishnu", "number": 6, "flower": "Orchid"}, {"name": "Krishiv", "number": 13, "flower": "Anemone"}, {"name": "Tanvi", "number": 9, "flower": "Peony"}, {"name": "Tay", "number": 13, "flower": "Gerbera"}, {"name": "Yuri", "number": 4, "flower": "Daisy"}]
    
    Sorted List using Quick Sort:
    [{"name": "Abigail", "number": 2, "flower": "Tulip"}, {"name": "Aditi", "number": 3, "flower": "Lily"}, {"name": "Aditya", "number": 5, "flower": "Sunflower"}, {"name": "Alara", "number": 1, "flower": "Rose"}, {"name": "Alex", "number": 8, "flower": "Hydrangea"}, {"name": "Anthony", "number": 11, "flower": "Dahlia"}, {"name": "David", "number": 14, "flower": "Poppy"}, {"name": "Emaad", "number": 12, "flower": "Freesia"}, {"name": "Ethan T", "number": 7, "flower": "Carnation"}, {"name": "James", "number": 10, "flower": "Cherry Blossom"}, {"name": "Jishnu", "number": 6, "flower": "Orchid"}, {"name": "Krishiv", "number": 13, "flower": "Anemone"}, {"name": "Tanvi", "number": 9, "flower": "Peony"}, {"name": "Tay", "number": 13, "flower": "Gerbera"}, {"name": "Yuri", "number": 4, "flower": "Daisy"}]


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with Merge Sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
