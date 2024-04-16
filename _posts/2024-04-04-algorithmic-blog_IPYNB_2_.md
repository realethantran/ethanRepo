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

Bubble sort is iteratively goes through the list, compares nearby elements, and switches items if necessary to keep them in the correct order. It is inefficient for large datasets, as it has an O(n^2) time complexity meaning that larger datasets mean more operations used to sort.

> Code


```java
public static void bubblesort(List<FlowerGroupMember> list) {
    int n = list.size(); // get size of list
    for (int i = 0; i < n - 1; i++) { // loop through the list
        for (int j = 0; j < n - i - 1; j++) { // loop through unsorted part of the list
            if (list.get(j).getNumber() > list.get(j + 1).getNumber()) { // check if current element > next element
                // swap list[j] and list[j+1]
                FlowerGroupMember temp = list.get(j); // store current element in temporary variable
                list.set(j, list.get(j + 1)); // set current element to next element
                list.set(j + 1, temp); // set next element to temporary variable
            }
        }
    }
}
```

### Selection Sort

Selection sort splits the given list into two parts: sorted (at the beginning of the list) and the unsorted part falling after. The items start in the unsorted part while the sorted part is empty. The algorithm moves the smallest/maximum (depends on sort) element from the unsorted section to the end of the sorted part with each iteration.Its time complexity is O(n^2), meaning that it is inefficient for very large datasets but it can be helpful for tiny datasets.

> Code


```java
public static void selectionsort(List<FlowerGroupMember> list) {
    int n = list.size(); // get size of list
    for (int i = 0; i < n - 1; i++) { // loop through list
        int minIndex = i; // assume current index is minimum
        for (int j = i + 1; j < n; j++) { // loop through remaining elements
            if (list.get(j).getNumber() < list.get(minIndex).getNumber()) { // compare numbers
                minIndex = j; // update minimum index if smaller number found
            }
        }
        // swap list[i] and list[minIndex]
        FlowerGroupMember temp = list.get(i); // store current element in temporary variable
        list.set(i, list.get(minIndex)); // set current element to minimum element
        list.set(minIndex, temp); // set minimum element to temporary variable
    }
}
```

### Insertion Sort

Insertion sort builds the final sorted Array one element at a time, iterating through the input Array and moving each element into the correct position through comparing it with elements to its left. It has a time complexity of O(n^2), making it inefficient with large Arrays, but it is efficient for small data sets or nearly sorted Arrays as it is adaptive to partially sorted Arrays, and space-efficient due to its in-place sorting nature.

> Code 


```java
public static void insertionsort(List<FlowerGroupMember> list) {
    int n = list.size();  // get size of list
    for (int i = 1; i < n; i++) {  // iterate through list starting from second element
        FlowerGroupMember key = list.get(i);  // current element to be inserted
        int j = i - 1;  // index of previous element
        // move elements of list[0..i-1] that are greater than key to one position ahead of their current position
        while (j >= 0 && list.get(j).getNumber() > key.getNumber()) {
            list.set(j + 1, list.get(j));  // shift element to right
            j = j - 1;  // move to previous element
        }
        list.set(j + 1, key);  // insert key at its correct position
    }
}
```

### Merge Sort

Merge sort divides the input array into smaller halves until each sub-array contains a single element, then merges the smaller arrays into sorted order. It has a time complexity of O(n log n), which means that it is efficient even for large arrays.
> Code


```java
public static void mergesort(List<FlowerGroupMember> list, int left, int right) {
    // check if there's more than one element in the sublist
    if (left < right) {
        // calculate the middle index
        int mid = (left + right) / 2;
        
        // recursively sort the left and right sublists
        mergesort(list, left, mid);
        mergesort(list, mid + 1, right);
        
        // merge the sorted sublists
        merge(list, left, mid, right);
    }
}

// merge function to merge two sorted sublists into one sorted list
private static void merge(List<FlowerGroupMember> list, int left, int mid, int right) {
    // calculate the sizes of the two sublists
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // create temporary lists to hold the two sublists
    List<FlowerGroupMember> leftList = new ArrayList<>();
    List<FlowerGroupMember> rightList = new ArrayList<>();

    // populate the left sublist
    for (int i = 0; i < n1; ++i) {
        leftList.add(list.get(left + i));
    }
    
    // populate the right sublist
    for (int j = 0; j < n2; ++j) {
        rightList.add(list.get(mid + 1 + j));
    }

    // initialize indices for the two sublists and the merged list
    int i = 0, j = 0;
    int k = left;

    // merge the two sublists into the main list
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

    // copy any remaining elements from the left sublist
    while (i < n1) {
        list.set(k, leftList.get(i));
        i++;
        k++;
    }

    // copy any remaining elements from the right sublist
    while (j < n2) {
        list.set(k, rightList.get(j));
        j++;
        k++;
    }
}
```

### Quick Sort

Quick sort splits the array based on a selected pivot element, in which elements smaller than the pivot are moved to its left, and larger elements to its right. This process continues until the entire array is sorted by sorting the sub-arrays before and after the pivot element. quick sort has an average time complexity of O(n log n), making it efficient for large arrays, but it could degrade to O(n^2) in a worst-case scenario. However, it is widely used due to its average-case performance and in-place sorting characteristic, making it memory-efficient.

> Code


```java
public static void quicksort(List<FlowerGroupMember> list, int low, int high) {
    // check if the list has more than one element
    if (low < high) {
        // find the partition index
        int pi = partition(list, low, high);
        
        // recursively sort the elements before and after partition
        quicksort(list, low, pi - 1);
        quicksort(list, pi + 1, high);
    }
}

// partition function for quick sort
private static int partition(List<FlowerGroupMember> list, int low, int high) {
    // select the pivot element (last element in this case)
    int pivot = list.get(high).getNumber();
    
    // index of smaller element
    int i = (low - 1);
    
    // iterate through the list
    for (int j = low; j < high; j++) {
        // if current element is smaller than the pivot
        if (list.get(j).getNumber() < pivot) {
            // increment the index of smaller element
            i++;

            // swap list[i] and list[j]
            FlowerGroupMember temp = list.get(i);
            list.set(i, list.get(j));
            list.set(j, temp);
        }
    }

    // swap list[i + 1] and list[high] (or the pivot)
    FlowerGroupMember temp = list.get(i + 1);
    list.set(i + 1, list.get(high));
    list.set(high, temp);

    // return the partition index
    return i + 1;
}
```

### Sort Implementation with Flower Group 


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
        return "{\"name\": \"" + name + "\", \"number\": " + number + ", \"flowerType\": \"" + flowerType + "\"}";
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
    Garden{members=[{"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "David", "number": 14, "flowerType": "Poppy"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}]}
    
    After bubble sort:
    [{"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}, {"name": "David", "number": 14, "flowerType": "Poppy"}]
    
    After selection sort:
    [{"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}, {"name": "David", "number": 14, "flowerType": "Poppy"}]
    
    After insertion sort:
    [{"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}, {"name": "David", "number": 14, "flowerType": "Poppy"}]
    
    After merge sort:
    [{"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}, {"name": "David", "number": 14, "flowerType": "Poppy"}]
    
    After quick sort:
    [{"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "David", "number": 14, "flowerType": "Poppy"}]


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with merge sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
