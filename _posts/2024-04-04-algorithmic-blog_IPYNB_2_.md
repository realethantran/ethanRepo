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
// bubbleSort
public void bubbleSort(List<FlowerGroupMember> list) {
    int n = list.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (list.get(j).getNumber() > list.get(j + 1).getNumber()) {
                swap(list, j, j + 1);
            }
        }
    }
}
```

### Selection Sort

Selection sort splits the given list into two parts: sorted (at the beginning of the list) and the unsorted part falling after. The items start in the unsorted part while the sorted part is empty. The algorithm moves the smallest/maximum (depends on sort) element from the unsorted section to the end of the sorted part with each iteration.Its time complexity is O(n^2), meaning that it is inefficient for very large datasets but it can be helpful for tiny datasets.

> Code


```java
// selectionSort
public void selectionSort(List<FlowerGroupMember> list) {
    int n = list.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (list.get(j).getNumber() < list.get(minIndex).getNumber()) {
                minIndex = j;
            }
        }
        swap(list, i, minIndex);
    }
}
```

### Insertion Sort

Insertion sort builds the final sorted Array one element at a time, iterating through the input Array and moving each element into the correct position through comparing it with elements to its left. It has a time complexity of O(n^2), making it inefficient with large Arrays, but it is efficient for small data sets or nearly sorted Arrays as it is adaptive to partially sorted Arrays, and space-efficient due to its in-place sorting nature.

> Code 


```java
// insertionSort
public void insertionSort(List<FlowerGroupMember> list) {
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
```

### Merge Sort

Merge sort divides the input array into smaller halves until each sub-array contains a single element, then merges the smaller arrays into sorted order. It has a time complexity of O(n log n), which means that it is efficient even for large arrays.
> Code


```java
// mergeSort
public void mergeSort(List<FlowerGroupMember> list) {
    if (list.size() <= 1) {
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
    
    while (i < left.size() && j < right.size()) {
        if (left.get(i).getNumber() < right.get(j).getNumber()) {
            list.set(k++, left.get(i++));
        } else {
            list.set(k++, right.get(j++));
        }
    }
    
    while (i < left.size()) {
        list.set(k++, left.get(i++));
    }
    
    while (j < right.size()) {
        list.set(k++, right.get(j++));
    }
}

private void swap(List<FlowerGroupMember> list, int i, int j) {
    FlowerGroupMember temp = list.get(i);
    list.set(i, list.get(j));
    list.set(j, temp);
}
```

### Quick Sort

Quick sort splits the array based on a selected pivot element, in which elements smaller than the pivot are moved to its left, and larger elements to its right. This process continues until the entire array is sorted by sorting the sub-arrays before and after the pivot element. quick sort has an average time complexity of O(n log n), making it efficient for large arrays, but it could degrade to O(n^2) in a worst-case scenario. However, it is widely used due to its average-case performance and in-place sorting characteristic, making it memory-efficient.

> Code


```java
// quickSort
private void quickSort(List<FlowerGroupMember> list, int low, int high) {
    if (low < high) {
        int partitionIndex = partition(list, low, high);

        quickSort(list, low, partitionIndex - 1);
        quickSort(list, partitionIndex + 1, high);
    }
}

private int partition(List<FlowerGroupMember> list, int low, int high) {
    int pivot = list.get(high).getNumber();
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (list.get(j).getNumber() < pivot) {
            i++;
            swap(list, i, j);
        }
    }

    swap(list, i + 1, high);

    return i + 1;
}

private void swap(List<FlowerGroupMember> list, int i, int j) {
    FlowerGroupMember temp = list.get(i);
    list.set(i, list.get(j));
    list.set(j, temp);
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

public class Sorts {
    // bubbleSort
    public void bubbleSort(List<FlowerGroupMember> list) {
        int n = list.size();
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (list.get(j).getNumber() > list.get(j + 1).getNumber()) {
                    swap(list, j, j + 1);
                }
            }
        }
    }
    
    // selectionSort
    public void selectionSort(List<FlowerGroupMember> list) {
        int n = list.size();
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (list.get(j).getNumber() < list.get(minIndex).getNumber()) {
                    minIndex = j;
                }
            }
            swap(list, i, minIndex);
        }
    }

    // insertionSort
    public void insertionSort(List<FlowerGroupMember> list) {
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

    // mergeSort
    public void mergeSort(List<FlowerGroupMember> list) {
        if (list.size() <= 1) {
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
        
        while (i < left.size() && j < right.size()) {
            if (left.get(i).getNumber() < right.get(j).getNumber()) {
                list.set(k++, left.get(i++));
            } else {
                list.set(k++, right.get(j++));
            }
        }
        
        while (i < left.size()) {
            list.set(k++, left.get(i++));
        }
        
        while (j < right.size()) {
            list.set(k++, right.get(j++));
        }
    }

    // quickSort
    public void quickSort(List<FlowerGroupMember> list) {
        quickSort(list, 0, list.size() - 1);
    }

    private void quickSort(List<FlowerGroupMember> list, int low, int high) {
        if (low < high) {
            int partitionIndex = partition(list, low, high);

            quickSort(list, low, partitionIndex - 1);
            quickSort(list, partitionIndex + 1, high);
        }
    }

    private int partition(List<FlowerGroupMember> list, int low, int high) {
        int pivot = list.get(high).getNumber();
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (list.get(j).getNumber() < pivot) {
                i++;
                swap(list, i, j);
            }
        }

        swap(list, i + 1, high);

        return i + 1;
    }

    private void swap(List<FlowerGroupMember> list, int i, int j) {
        FlowerGroupMember temp = list.get(i);
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
        
        Sorts sorts = new Sorts();
        
        sorts.bubbleSort(new ArrayList<>(gardenMembers));
        System.out.println("\nAfter bubble sort:");
        System.out.println(gardenMembers);

        sorts.selectionSort(new ArrayList<>(gardenMembers));
        System.out.println("\nAfter selection sort:");
        System.out.println(gardenMembers);

        sorts.insertionSort(new ArrayList<>(gardenMembers));
        System.out.println("\nAfter insertion sort:");
        System.out.println(gardenMembers);

        sorts.mergeSort(new ArrayList<>(gardenMembers));
        System.out.println("\nAfter merge sort:");
        System.out.println(gardenMembers);

        sorts.quickSort(new ArrayList<>(gardenMembers));
        System.out.println("\nAfter quick sort:");
        System.out.println(gardenMembers);
    }
}
Main.main(null);
```

    Original Garden:
    Garden{members=[{"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "David", "number": 14, "flowerType": "Poppy"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}]}
    
    After bubble sort:
    [{"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "David", "number": 14, "flowerType": "Poppy"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}]
    
    After selection sort:
    [{"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "David", "number": 14, "flowerType": "Poppy"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}]
    
    After insertion sort:
    [{"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "David", "number": 14, "flowerType": "Poppy"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}]
    
    After merge sort:
    [{"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "David", "number": 14, "flowerType": "Poppy"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}]
    
    After quick sort:
    [{"name": "Tanvi", "number": 9, "flowerType": "Peony"}, {"name": "Yuri", "number": 4, "flowerType": "Daisy"}, {"name": "Abigail", "number": 2, "flowerType": "Tulip"}, {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}, {"name": "Alara", "number": 1, "flowerType": "Rose"}, {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}, {"name": "David", "number": 14, "flowerType": "Poppy"}, {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}, {"name": "Emaad", "number": 12, "flowerType": "Freesia"}, {"name": "Tay", "number": 13, "flowerType": "Gerbera"}, {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}, {"name": "Aditi", "number": 3, "flowerType": "Lily"}, {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}, {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}, {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}]


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with merge sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
