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


```Java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class FlowerGroupMember implements Comparable<FlowerGroupMember> {
    private String name;
    private int number;
    private String flowerType;

    public interface KeyTypes {
        String name();
    }

    public enum KeyType implements KeyTypes {
        NAME, NUMBER, FLOWERTYPE
    }

    private KeyType sortKey = KeyType.NUMBER;

    public FlowerGroupMember(String name, int number, String flowerType) {
        this.name = name;
        this.number = number;
        this.flowerType = flowerType;
    }

    public void setSortKey(KeyType key) {
        sortKey = key;
    }

    private KeyType getSortKey() {
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

    public String getName() {
        return name;
    }

    public int getNumber() {
        return number;
    }

    public String getFlowerType() {
        return flowerType;
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
    public void bubbleSort(List<FlowerGroupMember> list, Comparator<FlowerGroupMember> comparator) {
        int n = list.size();
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (comparator.compare(list.get(j), list.get(j + 1)) > 0) {
                    swap(list, j, j + 1);
                }
            }
        }
    }

    public void selectionSort(List<FlowerGroupMember> list, Comparator<FlowerGroupMember> comparator) {
        int n = list.size();
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (comparator.compare(list.get(j), list.get(minIndex)) < 0) {
                    minIndex = j;
                }
            }
            swap(list, i, minIndex);
        }
    }

    public void insertionSort(List<FlowerGroupMember> list, Comparator<FlowerGroupMember> comparator) {
        int n = list.size();
        for (int i = 1; i < n; i++) {
            FlowerGroupMember key = list.get(i);
            int j = i - 1;
            while (j >= 0 && comparator.compare(list.get(j), key) > 0) {
                list.set(j + 1, list.get(j));
                j = j - 1;
            }
            list.set(j + 1, key);
        }
    }

    public void mergeSort(List<FlowerGroupMember> list, Comparator<FlowerGroupMember> comparator) {
        if (list.size() <= 1) {
            return;
        }

        int mid = list.size() / 2;

        List<FlowerGroupMember> left = new ArrayList<>(list.subList(0, mid));
        List<FlowerGroupMember> right = new ArrayList<>(list.subList(mid, list.size()));

        mergeSort(left, comparator);
        mergeSort(right, comparator);

        merge(list, left, right, comparator);
    }

    private void merge(List<FlowerGroupMember> list, List<FlowerGroupMember> left, List<FlowerGroupMember> right, Comparator<FlowerGroupMember> comparator) {
        int i = 0, j = 0, k = 0;

        while (i < left.size() && j < right.size()) {
            if (comparator.compare(left.get(i), right.get(j)) < 0) {
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

    public void quickSort(List<FlowerGroupMember> list, Comparator<FlowerGroupMember> comparator) {
        quickSort(list, 0, list.size() - 1, comparator);
    }

    private void quickSort(List<FlowerGroupMember> list, int low, int high, Comparator<FlowerGroupMember> comparator) {
        if (low < high) {
            int partitionIndex = partition(list, low, high, comparator);

            quickSort(list, low, partitionIndex - 1, comparator);
            quickSort(list, partitionIndex + 1, high, comparator);
        }
    }

    private int partition(List<FlowerGroupMember> list, int low, int high, Comparator<FlowerGroupMember> comparator) {
        FlowerGroupMember pivot = list.get(high);
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (comparator.compare(list.get(j), pivot) < 0) {
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

        Sorts sorter = new Sorts();

        for (FlowerGroupMember.KeyType key : FlowerGroupMember.KeyType.values()) {
            Comparator<FlowerGroupMember> comparator = Comparator.comparing(member -> {
                switch (key) {
                    case NAME:
                        return member.getName();
                    case NUMBER:
                        return String.format("%03d", member.getNumber());
                    case FLOWERTYPE:
                        return member.getFlowerType();
                    default:
                        return member.getName();
                }
            });

            System.out.println("Before " + key.name() + " Sort:");
            gardenMembers.forEach(System.out::println);
            System.out.println();

            sorter.bubbleSort(gardenMembers, comparator);
            System.out.println("After Bubble Sort:");
            gardenMembers.forEach(System.out::println);

            sorter.selectionSort(gardenMembers, comparator);
            System.out.println("After Selection Sort:");
            gardenMembers.forEach(System.out::println);

            sorter.insertionSort(gardenMembers, comparator);
            System.out.println("After Insertion Sort:");
            gardenMembers.forEach(System.out::println);

            sorter.quickSort(gardenMembers, comparator);
            System.out.println("After Quick Sort:");
            gardenMembers.forEach(System.out::println);

            sorter.mergeSort(gardenMembers, comparator);
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
    Before NAME Sort:
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
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    After Selection Sort:
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    After Insertion Sort:
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    After Quick Sort:
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    After Merge Sort:
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    
    Before NUMBER Sort:
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    
    After Bubble Sort:
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    After Selection Sort:
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    After Insertion Sort:
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    After Quick Sort:
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    After Merge Sort:
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    
    Before FLOWERTYPE Sort:
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    
    After Bubble Sort:
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    After Selection Sort:
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    After Insertion Sort:
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    After Quick Sort:
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    After Merge Sort:
    {"name": "Krishiv", "number": 13, "flowerType": "Anemone"}
    {"name": "Ethan T", "number": 7, "flowerType": "Carnation"}
    {"name": "James", "number": 10, "flowerType": "Cherry Blossom"}
    {"name": "Anthony", "number": 11, "flowerType": "Dahlia"}
    {"name": "Yuri", "number": 4, "flowerType": "Daisy"}
    {"name": "Emaad", "number": 12, "flowerType": "Freesia"}
    {"name": "Tay", "number": 13, "flowerType": "Gerbera"}
    {"name": "Alex", "number": 8, "flowerType": "Hydrangea"}
    {"name": "Aditi", "number": 3, "flowerType": "Lily"}
    {"name": "Jishnu", "number": 6, "flowerType": "Orchid"}
    {"name": "Tanvi", "number": 9, "flowerType": "Peony"}
    {"name": "David", "number": 14, "flowerType": "Poppy"}
    {"name": "Alara", "number": 1, "flowerType": "Rose"}
    {"name": "Aditya", "number": 5, "flowerType": "Sunflower"}
    {"name": "Abigail", "number": 2, "flowerType": "Tulip"}
    


## Algorithmic Performance Experience

To begin, I would like to say that the entire experience from forming teams, planning our performance, practicing with my team, and the actual performance itself were absolutely awesome! Our team started by doing some overall research and getting more familiar with merge sort, as we had to figure out a way to create a performance centered around the algorithm. Eventually, our team decided to create a flower performance, with some aspects from Dune, to show off our creativity a bit better for the judges. As everyone in our team knew the algorithm pretty well, we spent most practices working on our dance and ways to show how the sort works (split, sort, merge). Overall, this experience was really fun as it was really cool to plan and practice at lunch, and also include students from the AP Computer Science Principles class into our group.

> Images from Algorithmic

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/be53cc95-98a9-4a68-a167-05c685315030)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/bbe10631-9bcb-4fe4-b971-c75b807a7a97)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/58a7e66c-4cbd-4cd2-8245-084259424bc3)

![image](https://github.com/realethantran/fastpages_EthanT/assets/109186517/83de0135-4b6f-43e4-8132-777988b8eb6f)
