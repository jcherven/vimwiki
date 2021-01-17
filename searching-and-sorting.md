# searching-and-sorting

In the last several videos, we’ve covered a lot of the common data structures, and some of the algorithms that use them. Now we’re going to switch tacks and talk about some common algorithms that can be used in tandem with those data structures. In this video, we’re going to discuss a selection of algorithms for searching and sorting through data. 

If you have an unsorted selection of elements in a data structure, searching through them is always going to be an O(n) function. Ideally, we would like to be able to search a selection of elements in O(logN) or even O(1) time, but doing that usually requires that the data be sorted in some way first. There are many different searching and sorting algorithms, with varying degrees of performance in terms of both speed and memory use. 

One of the simplest kinds of search you can do on a sorted data set is a binary search, which runs in O(LogN) time. It works by first checking the middle element, and determining if that element is greater than or less than the target. If it’s greater than the target, the result must exist “left” of the middle element, and if the middle element is less than the target, the desired result must exist right of it. The algorithm for a binary search looks like this. 

```
algorithm binarySearch is
  input: array - the array being searched
    target: the value being searched for
    
  output: the index of a match between the target, or -1 if not found
  
  let minRange = 0
  let maxRange = array.length - 1
  let midpoint = 0
  
  while (minRange <= maxRange)
    midpoint = (minrange + maxRange) / 2
    
    if (array[midpoint] < target)
      minRange = midpoint + 1
    else if (a[midpoint] > target)
      maxRange = midpoint - 1
    else
      return midpoint
  
  return -1
```

It’s rather simple, the algorithm computes the midpoint of the current search range, which starts between the first and last elements. Each time it compares the midpoint to the target, and either raises the low end of the search range, or reduces the high end until the midpoint lands on the target. This guarantees an O(logN) run time, because the number of elements to search is divided in half with each iteration. 

Sorting a collection is a much more complicated topic. It’s hard for a sorting algorithm to get as low as O(n) complexity, because in order to know where every element goes, you need to look at every element. 

A bubble sort is the kind of sorting algorithm most people conceive of first. It works like this: Starting at index 0, you iterate over a collection to find the index that contains a smaller value. Every time you find a value smaller than the value currently in index 0, you swap that value at that index with index 0. You repeat this process, but you start at index 1, and iterate over the rest of the collection again, swapping the next-smallest element with the element at index 1. You repeat this until you’ve iterated over the entire list. The smaller values literally “bubble up” to the front of the collection. The algorithm for that looks like this. 

```
algorithm bubbleSort is
  input: array - the aray being sorted
  
  let x = 0
  let y = 1
  
  if (array.length < 2)
    return
    
  while ( x < array.length -1 )
    while (y < array.length)
      if (array[y] < array[x])
        let temp = array[x]
        array[x] = array[y]
        array[y] = temp
      y = y + 1
    x = x + 1
```

Notice how the values that are searched in each loop are offset. X starts at 0 and ends 1 index before the last, Y starts at 1 and ends at the last index. In this way, we avoid comparing an index to itself, and we also guarantee that we won’t accidentally compare an index outside the bounds of the array. 

You should recognize this as running in O(n^2) time. If you draw out the indexes that are getting compared in each iteration, you’ll see it forms half a square, split diagonally. The area represents the runtime of the algorithm, which while it’s technically 1/2n^2, we disregard coefficients. The memory use of this algorithm is only O(1) however, because we just work with the initial array and need no other supplementary data structures. 

So how could we sort an algorithm faster? Well, between O(n) and O(n^2) is O(nlog(n)). This means that for every element we perform an O(log(n)) function to it. Or put another way, we divide the collection into O(log(n)) parts, and perform an O(n) operation on each part. 

A merge sort works by recursively dividing a collection in half, until the size of each partitioned array is 1. Then adjacent partitions are compared and merged into a temporary array in sorted order, and then back into the main array. Because this algorithm is recursive, the size of the partitions starts at 1, and then doubles until the last iteration compares every element. This can be a bit complicated, so let’s visualize the algorithm with a simple 5 element array, with the values 4, 2, 3, 1, 5. 

```
algorithm mergeSort is
  input: arr - the array being sorted
  
  let temp be a new array of size arr.length
  
  partition(arr, temp, 0, arr.length - 1)
  
algorithm partition is
  input: arr - the array being sorted
    temp - a temp array
    min - the min index of the array
    max - the max index of the array
    
  if (min < max)
    let mid = (min + max) / 2
    partition(arr, temp, min, mid)
    partition(arr, temp, mid + 1, max)
    merge(arr, temp, min, mid, max)
```
```
algorithm merge is
  input: arr - the array being sorted
    temp - a temp array
    min - the minimum index of the array
    mid - the midpoint between min and the max
    maxIndex - the maximum index
    
  let i = min
  while ( i <= max )
    temp[i] = arr[i]
    i++
    
  let left = min
  let right = mid + 1
  let current = min
  
  while ((left <= mid) AND (right <= max))
    if (temp[left] <= temp[right])
      arr[current] = temp[left]
      left = left + 1
    else
      arr[current] = temp[right]
      right = right + 1
      
    current = current + 1
  
  let remaining = mid - left
  let i = 0
  while (i <= remaining)
    arr[current + i] = temp[left + i]
    i = i + 1
```

The recursive nature of the partition algorithm splits the array into 5 partitions of size 1. Then the first two partitions are compared, and merged into the temp array in sorted order – the right element is smaller than the left, so it’s inserted into the first index of the temp array, then the right element. Then these are merged back into the final array. 

The next iteration includes the midpoint, since this the size of this array is an odd number. But don’t be confused, we’re comparing two partitions – the left two elements are one partition, and the midpoint is the rightmost partition. We know the left partition is sorted, so we compare the leftmost element of the left partition to the leftmost element of the right partition. 2 is smaller than 3, so 2 gets inserted into the temp array first. Then we compare the leftmost remaining element of the left partition – 4 – to the leftmost remaining element of the right partition, which is 3. Now 3 is smaller, so it gets inserted. 4 is left, so 4 gets inserted again. Once again, all the elements are then merged back into the main array. Now we start on the right-hand side of the array. We compare the right two partitions, and they’re already in sorted order, so they’re inserted into the temp array as-is and merged back into the main array accordingly. 

The final iteration compares the left partition (including the midpoint) with the right partition. Notice how the left side is already sorted?Now we just have to compare the leftmost values of each partition, and insert the smallest into the temp array. This finally puts all elements in sorted order, and merges them back. 

Mergesort can be a huge headache, but it’s still less complex than an O(n^2) algorithm. However, it does require additional memory for the temp array, which is size n. Therefore, while it runs in O(nlog(n)) time, it requires O(n) additional memory. 

There are several other searching and sorting algorithms out there, these are just a basic starting point. A good developer isn’t expected to memorize all of them, but you should know a few by heart and be able to understand and implement others if given a brief description of how they work. 
