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


```Java
public class FlowerGroupMember implements Comparable<FlowerGroupMember> {
    // instance variables
    private String name;         
    private int number;          
    private String flowerType; 

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

    // compareTo method
    @Override
    public int compareTo(FlowerGroupMember other) {
        // compare members
        return this.name.compareTo(other.name);
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

// garden class 
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
}
```

## Class for all the sorts


```Java
public class Sorts {
    // bubble sort method
    public void bubbleSort(List<FlowerGroupMember> list) {
        int n = list.size(); // get the size of the list
        for (int i = 0; i < n - 1; i++) { // iterate over the list
            for (int j = 0; j < n - i - 1; j++) { // inner loop for comparisons
                if (list.get(j).compareTo(list.get(j + 1)) > 0) { // compare adjacent elements
                    swap(list, j, j + 1); // swap if elements are out of order
                }
            }
        }
    }

    // selection sort method
    public void selectionSort(List<FlowerGroupMember> list) {
        int n = list.size(); // get the size of the list
        for (int i = 0; i < n - 1; i++) { // iterate over the list
            int minIndex = i; // assume the minimum is the first element
            for (int j = i + 1; j < n; j++) { // find the minimum element in the remaining list
                if (list.get(j).compareTo(list.get(minIndex)) < 0) { // compare elements
                    minIndex = j; // update the minimum element index
                }
            }
            swap(list, i, minIndex); // swap the found minimum with the first element
        }
    }

    // insertion sort method
    public void insertionSort(List<FlowerGroupMember> list) {
        int n = list.size(); // get the size of the list
        for (int i = 1; i < n; i++) { // iterate over the list starting from the second element
            FlowerGroupMember key = list.get(i); // store the current element
            int j = i - 1; // initialize the previous element index
            while (j >= 0 && list.get(j).compareTo(key) > 0) { // move elements greater than key to one position ahead
                list.set(j + 1, list.get(j)); // shift element
                j = j - 1; // move to the previous element
            }
            list.set(j + 1, key); // place the key at its correct position
        }
    }

    // merge sort method
    public void mergeSort(List<FlowerGroupMember> list) {
        if (list.size() <= 1) // base case: if the list size is 1 or less
            return;

        int mid = list.size() / 2; // find the midpoint
        List<FlowerGroupMember> left = new ArrayList<>(list.subList(0, mid)); // create left sublist
        List<FlowerGroupMember> right = new ArrayList<>(list.subList(mid, list.size())); // create right sublist

        mergeSort(left); // recursively sort the left sublist
        mergeSort(right); // recursively sort the right sublist

        merge(list, left, right); // merge the sorted sublists
    }

    // merge method to combine sorted sublists
    private void merge(List<FlowerGroupMember> list, List<FlowerGroupMember> left, List<FlowerGroupMember> right) {
        int i = 0, j = 0, k = 0; // initialize pointers for left, right, and merged list

        while (i < left.size() && j < right.size()) { // iterate until one sublist is exhausted
            if (left.get(i).compareTo(right.get(j)) <= 0) { // compare elements of sublists
                list.set(k++, left.get(i++)); // add smaller element to the merged list
            } else {
                list.set(k++, right.get(j++)); // add smaller element to the merged list
            }
        }

        while (i < left.size()) { // add remaining elements from left sublist
            list.set(k++, left.get(i++));
        }

        while (j < right.size()) { // add remaining elements from right sublist
            list.set(k++, right.get(j++));
        }
    }

    // quick sort method
    public void quickSort(List<FlowerGroupMember> list) {
        quickSort(list, 0, list.size() - 1); // call the quicksort helper method
    }

    // quicksort helper method
    private void quickSort(List<FlowerGroupMember> list, int low, int high) {
        if (low < high) { // base case: if low index is less than high index
            int pi = partition(list, low, high); // partition the list and get the pivot index

            quickSort(list, low, pi - 1); // recursively sort the left sublist
            quickSort(list, pi + 1, high); // recursively sort the right sublist
        }
    }

    // partition method for quicksort
    private int partition(List<FlowerGroupMember> list, int low, int high) {
        FlowerGroupMember pivot = list.get(high); // choose the last element as the pivot
        int i = low - 1; // initialize the smaller element index
        for (int j = low; j < high; j++) { // iterate through the list
            if (list.get(j).compareTo(pivot) < 0) { // if the current element is smaller than the pivot
                i++; // increment the smaller element index
                swap(list, i, j); // swap the elements
            }
        }

        swap(list, i + 1, high); // place the pivot in the correct position
        return i + 1; // return the pivot index
    }

    // swap method to exchange elements in the list
    private void swap(List<FlowerGroupMember> list, int i, int j) {
        FlowerGroupMember temp = list.get(i); // store the first element in a temporary variable
        list.set(i, list.get(j)); // assign the second element to the first element's position
        list.set(j, temp); // assign the temporary variable to the second element's position
    }
}
```

## Main Class for testing


```Java
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

        // Sort by name (alphabetical)
        List<FlowerGroupMember> nameSorted = new ArrayList<>(members);
        nameSorted.sort((m1, m2) -> m1.getName().compareTo(m2.getName()));
        System.out.println("\nSorted by name:");
        printList(nameSorted);

        // Sort by number (numerical)
        List<FlowerGroupMember> numberSorted = new ArrayList<>(members);
        numberSorted.sort((m1, m2) -> Integer.compare(m1.getNumber(), m2.getNumber()));
        System.out.println("\nSorted by number:");
        printList(numberSorted);

        // Sort by flowerType (alphabetical)
        List<FlowerGroupMember> flowerTypeSorted = new ArrayList<>(members);
        flowerTypeSorted.sort((m1, m2) -> m1.getFlowerType().compareTo(m2.getFlowerType()));
        System.out.println("\nSorted by flower type:");
        printList(flowerTypeSorted);

        // Bubble Sort
        List<FlowerGroupMember> bubbleSorted = new ArrayList<>(members);
        sorter.bubbleSort(bubbleSorted);
        System.out.println("\nBubble Sort:");
        printList(bubbleSorted);

        // Selection Sort
        List<FlowerGroupMember> selectionSorted = new ArrayList<>(members);
        sorter.selectionSort(selectionSorted);
        System.out.println("\nSelection Sort:");
        printList(selectionSorted);

        // Insertion Sort
        List<FlowerGroupMember> insertionSorted = new ArrayList<>(members);
        sorter.insertionSort(insertionSorted);
        System.out.println("\nInsertion Sort:");
        printList(insertionSorted);

        // Merge Sort
        List<FlowerGroupMember> mergeSorted = new ArrayList<>(members);
        sorter.mergeSort(mergeSorted);
        System.out.println("\nMerge Sort:");
        printList(mergeSorted);

        // Quick Sort
        List<FlowerGroupMember> quickSorted = new ArrayList<>(members);
        sorter.quickSort(quickSorted);
        System.out.println("\nQuick Sort:");
        printList(quickSorted);
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
    
    Sorted by name:
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
    
    Sorted by number:
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
    
    Sorted by flower type:
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
    
    Insertion Sort:
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


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with merge sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
