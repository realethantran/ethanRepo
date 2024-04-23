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

### Class for All Sorts


```java
import java.util.ArrayList;
import java.util.List;

public class FlowerGroupMember implements Comparable<FlowerGroupMember> {
    private String name;
    private int number;
    private String flowerType;

    public enum KeyType implements KeyTypes {
        NAME, NUMBER, FLOWERTYPE
    }

    private KeyType sortKey = KeyType.NUMBER;

    public FlowerGroupMember(String name, int number, String flowerType) {
        this.name = name;
        this.number = number;
        this.flowerType = flowerType;
    }

    public interface KeyTypes {
        String name();
    }

    public void setSortKey(KeyType key) {
        sortKey = key;
    }

    private KeyTypes getSortKey() {
        return sortKey;
    }

    private String getSortKeyValue() {
        switch (sortKey) {
            case NAME:
                return name;
            case NUMBER:
                return String.format("%03d", number);
            case FLOWERTYPE:
                return flowerType;
            default:
                return name;
        }
    }

    @Override
    public int compareTo(FlowerGroupMember other) {
        return this.getSortKeyValue().compareTo(other.getSortKeyValue());
    }

    @Override
    public String toString() {
        return "{\"name\": \"" + name + "\", \"number\": " + number + ", \"flowerType\": \"" + flowerType + "\"}";
    }
}

class Garden {
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

class Sorts {
    // bubbleSort
    public void bubbleSort(List<FlowerGroupMember> list) {
        int n = list.size(); // get the size of the list
        for (int i = 0; i < n - 1; i++) { // loop through the list
            for (int j = 0; j < n - i - 1; j++) { // inner loop for comparisons
                if (list.get(j).compareTo(list.get(j + 1)) > 0) { // compare adjacent elements
                    swap(list, j, j + 1); // swap if needed
                }
            }
        }
    }

    // selectionSort
    public void selectionSort(List<FlowerGroupMember> list) {
        int n = list.size(); // get the size of the list
        for (int i = 0; i < n - 1; i++) { // loop through the list
            int minIndex = i; // assume the minimum is at the current index
            for (int j = i + 1; j < n; j++) { // find the minimum in the unsorted part
                if (list.get(j).compareTo(list.get(minIndex)) < 0) { // update minIndex
                    minIndex = j;
                }
            }
            swap(list, i, minIndex); // swap the minimum element with the current element
        }
    }

    // insertionSort
    public void insertionSort(List<FlowerGroupMember> list) {
        int n = list.size(); // get the size of the list
        for (int i = 1; i < n; i++) { // loop through the list starting from the second element
            FlowerGroupMember key = list.get(i); // current element to be inserted
            int j = i - 1; // start comparing with the previous element
            while (j >= 0 && list.get(j).compareTo(key) > 0) { // shift elements to make space for the key
                list.set(j + 1, list.get(j));
                j = j - 1;
            }
            list.set(j + 1, key); // insert the key at its correct position
        }
    }

    // mergeSort
    public void mergeSort(List<FlowerGroupMember> list) {
        if (list.size() <= 1) { // base case
            return;
        }

        int mid = list.size() / 2; // find the middle index

        List<FlowerGroupMember> left = new ArrayList<>(list.subList(0, mid)); // divide the list into two halves
        List<FlowerGroupMember> right = new ArrayList<>(list.subList(mid, list.size()));

        mergeSort(left); // recursively sort the left half
        mergeSort(right); // recursively sort the right half

        merge(list, left, right); // merge the sorted halves
    }

    private void merge(List<FlowerGroupMember> list, List<FlowerGroupMember> left, List<FlowerGroupMember> right) {
        int i = 0, j = 0, k = 0; // initialize pointers for left, right, and merged lists

        while (i < left.size() && j < right.size()) { // merge two sorted lists
            if (left.get(i).compareTo(right.get(j)) < 0) {
                list.set(k++, left.get(i++));
            } else {
                list.set(k++, right.get(j++));
            }
        }

        while (i < left.size()) { // copy remaining elements from left list
            list.set(k++, left.get(i++));
        }

        while (j < right.size()) { // copy remaining elements from right list
            list.set(k++, right.get(j++));
        }
    }

    // quickSort
    public void quickSort(List<FlowerGroupMember> list) {
        quickSort(list, 0, list.size() - 1); // call helper function with initial low and high indices
    }

    private void quickSort(List<FlowerGroupMember> list, int low, int high) {
        if (low < high) { // check if the list has more than one element
            int partitionIndex = partition(list, low, high); // partition the list

            quickSort(list, low, partitionIndex - 1); // recursively sort the left part
            quickSort(list, partitionIndex + 1, high); // recursively sort the right part
        }
    }

    private int partition(List<FlowerGroupMember> list, int low, int high) {
        FlowerGroupMember pivot = list.get(high); // choose the last element as pivot
        int i = low - 1; // index of smaller element

        for (int j = low; j < high; j++) { // partitioning process
            if (list.get(j).compareTo(pivot) < 0) {
                i++;
                swap(list, i, j);
            }
        }

        swap(list, i + 1, high); // place the pivot element at its correct position

        return i + 1; // return the partition index
    }

    private void swap(List<FlowerGroupMember> list, int i, int j) {
        FlowerGroupMember temp = list.get(i); // swap two elements in the list
        list.set(i, list.get(j));
        list.set(j, temp);
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

        List<FlowerGroupMember> gardenMembers = garden.getMembers();

        Sorts sorter = new Sorts();

        for (FlowerGroupMember.KeyType key : FlowerGroupMember.KeyType.values()) {
            System.out.println("Before Sorting by " + key.name() + ":");
            for (FlowerGroupMember member : gardenMembers) {
                member.setSortKey(key);
                System.out.println(member);
            }
            System.out.println();

            sorter.bubbleSort(new ArrayList<>(gardenMembers));
            System.out.println("After Bubble Sort:");
            gardenMembers.forEach(System.out::println);

            sorter.selectionSort(new ArrayList<>(gardenMembers));
            System.out.println("After Selection Sort:");
            gardenMembers.forEach(System.out::println);

            sorter.insertionSort(new ArrayList<>(gardenMembers));
            System.out.println("After Insertion Sort:");
            gardenMembers.forEach(System.out::println);
            
            sorter.quickSort(new ArrayList<>(gardenMembers));
            System.out.println("After Quick Sort:");
            gardenMembers.forEach(System.out::println);
            
            sorter.mergeSort(new ArrayList<>(gardenMembers));
            System.out.println("After Merge Sort:");
            gardenMembers.forEach(System.out::println);

            System.out.println();
        }
    }
}
Main.main(null);
```

    Original Garden:
    Garden{members=[{"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "David", "number": 14, "flowerType": "Poppy"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}]}
    Before Sorting by NAME:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    
    After Bubble Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Selection Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Insertion Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Quick Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Merge Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    
    Before Sorting by NUMBER:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    
    After Bubble Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Selection Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Insertion Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Quick Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Merge Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    
    Before Sorting by FLOWERTYPE:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    
    After Bubble Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Selection Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Insertion Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Quick Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    After Merge Sort:
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with merge sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
