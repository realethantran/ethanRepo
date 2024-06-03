---
title: Algorithmic Code Prep
author: Ethan Tran
toc: True
comments: True
layout: post
type: hacks
courses: {'csse': {'week': 1}, 'csp': {'week': 1, 'categories': ['4.A']}, 'csa': {'week': 25}, 'labnotebook': {'week': 3}}
---

## Learn All sorts

### Bubble Sort

Bubble sort steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until no swaps are needed, meaning the list is sorted. It is inefficient for large datasets, as it has an O(n^2) time complexity meaning that larger datasets mean more operations used to sort.

### Selection Sort

Selection sort splits the given list into two parts. The sort iterates over the list and finds the minimum (or maximum) element. It then swaps that element with the first (or last) unsorted element in the list. This process is repeated for each position in the list. Its time complexity is O(n^2), meaning that it is inefficient for very large datasets but it can be helpful for tiny datasets.

### Insertion Sort

Insertion sort imagines the list is already sorted except for the current element. It then inserts the current element into its correct position in the already sorted sub-list. This process is repeated for each element in the list. It has a time complexity of O(n^2), making it inefficient with large Arrays, but it is efficient for small data sets or nearly sorted Arrays as it is adaptive to partially sorted Arrays, and space-efficient due to its in-place sorting nature.

### Merge Sort

Merge sort is a divide-and-conquer sort. It divides the unsorted list into sub-lists containing a single element (base case). Then, it merges the sub-lists in a way that preserves the sorted order. It has a time complexity of O(n log n), which means that it is efficient even for large arrays.

### Quick Sort

Quick sort, like merge sort is a divide-and-conquer algorithm. It picks a pivot element from the list and partitions the remaining elements into two sub-lists: elements less than the pivot and elements greater than the pivot. Then, it recursively sorts the sub-lists and combines them in sorted order. Quick sort has an average time complexity of O(n log n), making it efficient for large arrays, but it could degrade to O(n^2) in a worst-case scenario. However, it is widely used due to its average-case performance and in-place sorting characteristic, making it memory-efficient.

## FlowerGroupMember Comparable


```java
import java.util.List;
import java.util.ArrayList;
import java.util.Collections;

public class FlowerGroupMember implements Comparable<FlowerGroupMember> {
    // instance variables
    private String name;         
    private int number;          
    private String flowerType; 

    // enum for key types
    public enum KeyType { NAME, NUMBER, FLOWER_TYPE }
    private static KeyType currentKeyType = KeyType.NAME;

    // constructor
    public FlowerGroupMember(String name, int number, String flowerType) {
        this.name = name;
        this.number = number;
        this.flowerType = flowerType;
    }

    // getters
    public String getName() {
        return name;
    }

    public int getNumber() {
        return number;
    }

    public String getFlowerType() {
        return flowerType;
    }

    // setters
    public void setName(String name) {
        this.name = name;
    }

    public void setNumber(int number) {
        this.number = number;
    }

    public void setFlowerType(String flowerType) {
        this.flowerType = flowerType;
    }

    // method to set the current key type
    public static void setKeyType(KeyType keyType) {
        currentKeyType = keyType;
    }

    // compareTo method
    @Override
    public int compareTo(FlowerGroupMember other) {
        switch (currentKeyType) {
            case NAME:
                return this.name.compareTo(other.name);
            case NUMBER:
                return Integer.compare(this.number, other.number);
            case FLOWER_TYPE:
                return this.flowerType.compareTo(other.flowerType);
            default:
                return 0; // should not reach here
        }
    }

    // toString method for better object representation
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
        members = new ArrayList<>();
    }

    public void addMember(FlowerGroupMember member) {
        members.add(member);
    }

    public List<FlowerGroupMember> getMembers() {
        return members;
    }

    public void sortMembers() {
        Collections.sort(members);
    }
}
```

## Class for all the sorts


```java
import java.util.List;
import java.util.ArrayList;

public class Sorts {

// Bubble Sort
public void bubbleSort(List<FlowerGroupMember> list) {
    int n = list.size();
    // Traverse through all elements in the list
    for (int i = 0; i < n - 1; i++) {
        // Last i elements are already in place, so no need to traverse them
        for (int j = 0; j < n - i - 1; j++) {
            // Swap if the element found is greater than the next element
            if (list.get(j).compareTo(list.get(j + 1)) > 0) {
                FlowerGroupMember temp = list.get(j);
                list.set(j, list.get(j + 1));
                list.set(j + 1, temp);
            }
        }
    }
}

// Selection Sort
public void selectionSort(List<FlowerGroupMember> list) {
    int n = list.size();
    // Traverse through all elements in the list
    for (int i = 0; i < n - 1; i++) {
        // Find the minimum element in the unsorted part of the list
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            if (list.get(j).compareTo(list.get(minIdx)) < 0) {
                minIdx = j;
            }
        }
        // Swap the found minimum element with the first element
        FlowerGroupMember temp = list.get(minIdx);
        list.set(minIdx, list.get(i));
        list.set(i, temp);
    }
}

// Insertion Sort
public void insertionSort(List<FlowerGroupMember> list) {
    int n = list.size();
    // Traverse through all elements in the list starting from the second element
    for (int i = 1; i < n; ++i) {
        FlowerGroupMember key = list.get(i);
        int j = i - 1;
        // Move elements of list[0..i-1], that are greater than key, to one position ahead of their current position
        while (j >= 0 && list.get(j).compareTo(key) > 0) {
            list.set(j + 1, list.get(j));
            j = j - 1;
        }
        list.set(j + 1, key);
    }
}

// Merge Sort
public void mergeSort(List<FlowerGroupMember> list) {
    if (list.size() < 2) {
        return;
    }
    int mid = list.size() / 2;
    List<FlowerGroupMember> left = new ArrayList<>(list.subList(0, mid));
    List<FlowerGroupMember> right = new ArrayList<>(list.subList(mid, list.size()));

    mergeSort(left);
    mergeSort(right);

    merge(list, left, right);
}

private void merge(List<FlowerGroupMember> list, List<FlowerGroupMember> left, List<FlowerGroupMember> right) {
    int i = 0, j = 0, k = 0;
    // Merge the two sublists into the original list in sorted order
    while (i < left.size() && j < right.size()) {
        if (left.get(i).compareTo(right.get(j)) <= 0) {
            list.set(k++, left.get(i++));
        } else {
            list.set(k++, right.get(j++));
        }
    }
    // Copy remaining elements of left[] if any
    while (i < left.size()) {
        list.set(k++, left.get(i++));
    }
    // Copy remaining elements of right[] if any
    while (j < right.size()) {
        list.set(k++, right.get(j++));
    }
}

// Quick Sort
public void quickSort(List<FlowerGroupMember> list) {
    quickSort(list, 0, list.size() - 1);
}

private void quickSort(List<FlowerGroupMember> list, int low, int high) {
    if (low < high) {
        // pi is partitioning index
        int pi = partition(list, low, high);
        // Recursively sort elements before and after partition
        quickSort(list, low, pi - 1);
        quickSort(list, pi + 1, high);
    }
}

private int partition(List<FlowerGroupMember> list, int low, int high) {
    FlowerGroupMember pivot = list.get(high);
    int i = (low - 1);
    // Traverse through all elements in the list
    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (list.get(j).compareTo(pivot) < 0) {
            i++;
            // Swap list[i] and list[j]
            FlowerGroupMember temp = list.get(i);
            list.set(i, list.get(j));
            list.set(j, temp);
        }
    }
    // Swap list[i+1] and list[high] (or pivot)
    FlowerGroupMember temp = list.get(i + 1);
    list.set(i + 1, list.get(high));
    list.set(high, temp);

    return i + 1;
}
```

## Main Class for testing


```java
import java.util.ArrayList;
import java.util.List;

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

        List<FlowerGroupMember> members = garden.getMembers();

        Sorts sorter = new Sorts();

        // Apply different sorting algorithms
        System.out.println("Unsorted list:");
        printList(members);

        // Bubble Sort
        FlowerGroupMember.setKeyType(FlowerGroupMember.KeyType.NAME);
        List<FlowerGroupMember> bubbleSorted = new ArrayList<>(members);
        sorter.bubbleSort(bubbleSorted);
        System.out.println("\nBubble Sort:");
        printList(bubbleSorted);

        // Selection Sort 
        FlowerGroupMember.setKeyType(FlowerGroupMember.KeyType.NUMBER);
        List<FlowerGroupMember> selectionSorted = new ArrayList<>(members);
        sorter.selectionSort(selectionSorted);
        System.out.println("\nSelection Sort:");
        printList(selectionSorted);

        // Insertion Sort
        FlowerGroupMember.setKeyType(FlowerGroupMember.KeyType.FLOWER_TYPE);
        List<FlowerGroupMember> insertionSorted = new ArrayList<>(members);
        sorter.insertionSort(insertionSorted);
        System.out.println("\nInsertion Sort:");
        printList(insertionSorted);

        // Merge Sort
        FlowerGroupMember.setKeyType(FlowerGroupMember.KeyType.NAME);
        List<FlowerGroupMember> mergeSorted = new ArrayList<>(members);
        sorter.mergeSort(mergeSorted);
        System.out.println("\nMerge Sort:");
        printList(mergeSorted);

        // Quick Sort
        FlowerGroupMember.setKeyType(FlowerGroupMember.KeyType.NUMBER);
        List<FlowerGroupMember> quickSorted = new ArrayList<>(members);
        sorter.quickSort(quickSorted);
        System.out.println("\nQuick Sort:");
        
        printList(quickSorted);
        // Sort by name (alphabetical)
        FlowerGroupMember.setKeyType(FlowerGroupMember.KeyType.NAME);
        List<FlowerGroupMember> nameSorted = new ArrayList<>(members);
        sorter.bubbleSort(nameSorted);
        System.out.println("\nSort by NAME:");
        printList(nameSorted);

        // Sort by number (numerical)
        FlowerGroupMember.setKeyType(FlowerGroupMember.KeyType.NUMBER);
        List<FlowerGroupMember> numberSorted = new ArrayList<>(members);
        sorter.bubbleSort(numberSorted);
        System.out.println("\nSort by NUMBER:");
        printList(numberSorted);

        // Sort by flowerType (alphabetical)
        FlowerGroupMember.setKeyType(FlowerGroupMember.KeyType.FLOWER_TYPE);
        List<FlowerGroupMember> flowerTypeSorted = new ArrayList<>(members);
        sorter.bubbleSort(flowerTypeSorted);
        System.out.println("\nSort by FLOWERTYPE:");
        printList(flowerTypeSorted);
    }

    private static void printList(List<FlowerGroupMember> list) {
        for (FlowerGroupMember member : list) {
            System.out.println(member);
        }
    }
}
Main.main(null);
```

    Unsorted list:
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
    
    Bubble Sort:
    FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}
    FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}
    FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}
    FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}
    FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}
    FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}
    FlowerGroupMember{name='David', number=14, flowerType='Poppy'}
    FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}
    FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}
    FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}
    FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}
    FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}
    FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}
    FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}
    FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}
    
    Selection Sort:
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
    
    Insertion Sort:
    FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}
    FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}
    FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}
    FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}
    FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}
    FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}
    FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}
    FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}
    FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}
    FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}
    FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}
    FlowerGroupMember{name='David', number=14, flowerType='Poppy'}
    FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}
    FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}
    FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}
    
    Merge Sort:
    FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}
    FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}
    FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}
    FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}
    FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}
    FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}
    FlowerGroupMember{name='David', number=14, flowerType='Poppy'}
    FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}
    FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}
    FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}
    FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}
    FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}
    FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}
    FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}
    FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}
    
    Quick Sort:
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
    FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}
    FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}
    FlowerGroupMember{name='David', number=14, flowerType='Poppy'}
    
    Sort by NAME:
    FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}
    FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}
    FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}
    FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}
    FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}
    FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}
    FlowerGroupMember{name='David', number=14, flowerType='Poppy'}
    FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}
    FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}
    FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}
    FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}
    FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}
    FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}
    FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}
    FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}
    
    Sort by NUMBER:
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
    
    Sort by FLOWERTYPE:
    FlowerGroupMember{name='Krishiv', number=13, flowerType='Anemone'}
    FlowerGroupMember{name='Ethan T', number=7, flowerType='Carnation'}
    FlowerGroupMember{name='James', number=10, flowerType='Cherry Blossom'}
    FlowerGroupMember{name='Anthony', number=11, flowerType='Dahlia'}
    FlowerGroupMember{name='Yuri', number=4, flowerType='Daisy'}
    FlowerGroupMember{name='Emaad', number=12, flowerType='Freesia'}
    FlowerGroupMember{name='Tay', number=13, flowerType='Gerbera'}
    FlowerGroupMember{name='Alex', number=8, flowerType='Hydrangea'}
    FlowerGroupMember{name='Aditi', number=3, flowerType='Lily'}
    FlowerGroupMember{name='Jishnu', number=6, flowerType='Orchid'}
    FlowerGroupMember{name='Tanvi', number=9, flowerType='Peony'}
    FlowerGroupMember{name='David', number=14, flowerType='Poppy'}
    FlowerGroupMember{name='Alara', number=1, flowerType='Rose'}
    FlowerGroupMember{name='Aditya', number=5, flowerType='Sunflower'}
    FlowerGroupMember{name='Abigail', number=2, flowerType='Tulip'}


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with merge sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
