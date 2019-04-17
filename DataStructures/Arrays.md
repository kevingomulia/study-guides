# Arrays
Stores a **fixed-size** sequential collection of elements of the same type.

You can add elements into an array, but it is cumbersome. Use ArrayList instead.

## Creating Arrays
```
datatype[] arrayName = new datatype[arraySize];
```

Alternatively, you can create arrays with initial values as follows:
```
datatype[] arrayName = {value0, value1, ..., valuek};
```
The array elements are accessed through the `index`. Array indices are 0-based; that is, they start from 0 to arrayRefVar.length-1.

## Processing Arrays
Use **for** or **foreach** loop because all of the elements are of the same type and the size of the array is known.

Can use `Arrays.equals` method to check if the elements in two arrays are the same.

## Notes

The key benefit of an array data structure is that it offers fast O(1) search if you know the index, but **adding and removing an element from an array is slow** because you cannot change the size of the array once it’s created.

In order to create a shorter or longer array, you need to create a new array and copy all elements from old to new.

## Questions to expect
Reversing an array, Sorting the array, or Searching elements on the array.

## Questions
### Question 1. How do you find the missing number in a given integer array of 1 to 100?

**Solution:**
METHOD 1: Use Sum Formula
```
1. Get the sum of numbers
       total = n*(n+1)/2
2  Subtract all the numbers from sum and
   you will get the missing number.
```
**Time Complexity**: O(n)

But doesn't work with multiple missing numbers.

METHOD 2：Create a new array that is working like a map and check the indices that are not marked.
```

public static void main(String[] args){
  int[] input = {1, 1, 1, 2, 3, 5, 7, 9, 9 };
  int[] register = new int [input.length]; // Or new int [input[input.length - 1]]
  for (int i : input){
    register[i] = 1; // Or register[1] += 1
  }

  for (int i = 1; i < register.length; i++){
    if (register[i] == 0){
      System.out.println(i); // Missing number
    }
  }

}

```
**Time Complexity**: iterate through the array twice, so O(2n) = O(n).

### Question 2: Removing Duplicates from an Array.

A few solutions to different conditions.
- Using Collections API.

Using LinkedHashSet (or HashMap) is the best approach for removing duplicate elements in an array.
It also does maintains the order of elements added to it.

```
public static void main(String[] args) throws CloneNotSupportedException
    {
        //Array with duplicate elements
        Integer[] numbers = new Integer[] {1,2,3,4,5,1,3,5};

        //This array has duplicate elements
        System.out.println( Arrays.toString(numbers) );

        //Create set from array elements
        LinkedHashSet<Integer> linkedHashSet = new LinkedHashSet<>( Arrays.asList(numbers) );

        //Get back the array without duplicates
        Integer[] numbersWithoutDuplicates = linkedHashSet.toArray(new Integer[] {});

        //Verify the array content
        System.out.println( Arrays.toString(numbersWithoutDuplicates) );
    }
    ```

- Not being able to use Collections API and array elements are sorted.

If array elements are sorted then removing duplicates involve following steps:

1. Create a new array 'tempArray' with same size as original array 'origArray'.
2. Iterate over array starting from index location ‘0’.
3. Match current element with next element indexes until mismatch is found.
4. Add element to 'tempArray' and make current element to eleemnt which was mismatched.
5. Continue the iteration.
```
public static void main(String[] args) throws CloneNotSupportedException
    {
        // Array with duplicate elements
        Integer[] origArray = new Integer[] { 1, 1, 2, 3, 3, 3, 4, 5, 6, 6, 6, 7, 8 };

        // This array has duplicate elements
        System.out.println(Arrays.toString(origArray));

        Integer[] tempArray = removeDuplicates(origArray);

        // Verify the array content
        System.out.println(Arrays.toString(tempArray));
    }

    private static Integer[] removeDuplicates(Integer[] origArray) {

        Integer[] tempArray = new Integer[origArray.length];

        int indexJ = 0;
        for (int indexI = 0; indexI < origArray.length - 1; indexI++)
        {
            Integer currentElement = origArray[indexI];

            if (currentElement != origArray[indexI+1]) {
                tempArray[indexJ++] = currentElement;
            }
        }

        tempArray[indexJ++] = origArray[origArray.length-1];

        return tempArray;
    }
```

**Time Complexity**: O(n)

- No Collections API and array elements NOT sorted

If array elements are not sorted then to remove duplicate elements we need to iterate whole array for each current element. During each iteration, set 'null' for each matching element with current element.

In next iteration, select a non-null element and repeat above step.

```
public static void main(String[] args) throws CloneNotSupportedException
    {
        // Array with duplicate elements
        Integer[] origArray = new Integer[] { 1, 1, 2, 3, 3, 3, 4, 5, 6, 6, 6, 7, 8 };

        // This array has duplicate elements
        System.out.println(Arrays.toString(origArray));

        Integer[] tempArray = removeDuplicatesUnSorted(origArray);

        // Verify the array content
        System.out.println(Arrays.toString(tempArray));
    }

    private static Integer[] removeDuplicatesUnSorted(Integer[] origArray) {

    for (int j = 0; j < origArray.length - 1; j++) {
      for (int i = j+1; i < origArray.length - 1; i++) {
        if (origArray[j] == origArray[i]) {
          origArray[i] = null;
        }
      }
    }

    origArray[origArray.length-1] = null;

    return origArray;
  }
```

**Time Complexity**: O(n^2)

### Question 3: Reversing an Array
```
for(int i = 0; i < validData.length / 2; i++)
{
    int temp = validData[i];
    validData[i] = validData[validData.length - i - 1];
    validData[validData.length - i - 1] = temp;
}
```
### Question 4: Sorting an Array using QuickSort

```
class QuickSort {
    private int input[];
    private int length;

    public void sort(int[] numbers) {
        if (numbers == null || numbers.length == 0) {
            return;
        }
        this.input = numbers;
        length = numbers.length;
        quickSort(0, length - 1);
    } // This method implements in-place quicksort algorithm recursively.

    private void quickSort(int low, int high) {
        int i = low;
        int j = high; // pivot is middle index
        int pivot = input[low + (high - low) / 2]; // Divide into two arrays
        while (i <= j) {
            /**
             * As shown in above image, In each iteration, we will identify a
             * number from left side which is greater then the pivot value, and
             * a number from right side which is less then the pivot value. Once
             * search is complete, we can swap both numbers.
             */
            while (input[i] < pivot) {
                i++;
            }
            while (input[j] > pivot) {
                j--;
            }
            if (i <= j) {
                swap(i, j); // move index to next position on both sides
                i++;
                j--;
            }
        } // calls quickSort() method recursively

        if (low < j) {
            quickSort(low, j);
        }
        if (i < high) {
            quickSort(i, high);
        }
    }

    private void swap(int i, int j) {
        int temp = input[i];
        input[i] = input[j];
        input[j] = temp;
    }
}
```
### Important things about QuickSort
1) QuickSort is a divide and conquer algorithm. Large list is divided into two and sorted separately (conquered), sorted list is merge later.

2) On "in-place" implementation of quick sort, list is sorted using same array, no additional array is required. Numbers are re-arranged pivot, also known as partitioning.

3) Partitioning happen around pivot, which is usually middle element of array.

4) Average case time complexity of Quicksort is O(n log n) and worst case time complexity is O(n ^2), which makes it one of the fasted sorting algorithm. Interesting thing is it's worst case performance is equal to Bubble Sort :)

5) Quicksort can be implemented with an in-place partitioning algorithm, so the entire sort can be done with only O(log n) additional space used by the stack during the recursion.

6) Quicksort is also a good example of algorithm which makes best use of CPU caches, because of it's divide and conquer nature.

7) In Java, Arrays.sort() method uses quick sort algorithm to sort array of primitives. It's different than our algorithm, and uses two pivots. Good thing is that it perform much better than most of the quicksort algorithm available on internet for different data sets, where traditional quick sort perform poorly. One more reason, not to reinvent the wheel but to use the library method, when it comes to write production code.
