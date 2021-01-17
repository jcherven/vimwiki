# hashing

What happens… when you need to compare two complex and large pieces of data? Whether it’s two strings or two files, you need to determine if they’re the same, and you need to do it quickly. You could go bit by bit and compare them linearly… but of course, there’s an easier way. 

Of course, the big problem with comparing two large and complex items is that, well, they’re large and complex. Comparing each bit is an O(n) operation where n is the number of bits in one item. Why only one? Because if one has a different size than the other, they’re obviously not the same. O(n) scaling isn’t bad… but your average mp3 file has over 25 million bits, and an HD movie over 34 billion. When you consider that this is a common task for operating systems and other programs, this process rapidly becomes inefficient for real use-cases. 

A hash function is an algorithm that takes a set of variable-length data, and compresses it to a fixed-length data set. This fixed-length data is called a hash, digest, or hash code. Hash functions have a variety of uses, particularly in the field of cryptography. But because a hash is always a fixed length, comparing two hashes is always an O(1) operation – a lot of fancy data structures take advantage of this fact to improve their overall performance. A hash function only needs to be run once, but hash codes are compared very frequently. If the upfront one-time cost of a hash function is more complex than O(1), it’s amortized out over every use of the resulting hash code. 

There are a lot of different kinds of hashing functions, and we’re not going to delve too deeply into the common ones. A good hashing function must have several features to be practical, and those features add to the complexity. But we can talk about what a hash function is, and how to make a very basic one. So at their core, a hash function must take in some kind of data of variable length, and put out some data of a fixed length. That’s the only rule. So let’s make a hash function that accepts a string – an array of characters, and generates a hash for that string. Let’s say that our hash function will treat the character ‘a’ as 1, and ‘z’ as 26, and the resulting hash will be an integer that is the sum of every character in the String. That algorithm would look like this. 

```
algorithm basicHashFunction is
  input: text[] - a string of characters
  output: a 32-bit integer of hash
  
  let alpha[] be a pre-filled array of size 26
    where 'a' is at index 0 and 'z' is at 25.
  let hash = 0
  
  let c = 0
  while (c < text.length)
    let val = binarySearch(alpha, text[c]) + 1
    hash = hash + value
    c = c + 1
    
  return hash
```

You can see that we abstract the actual value lookup into a binary search, which we know will run in O(log(n)). We have to do this for every character in the input string, so the overall complexity is O(nlog(n)). Note that we’re adding 1 to the value each time, because the binary search will return a value between 0 and 25 (because of the way arrays are indexed), and we want values from 1 to 26. The resulting hash is always a 32-bit integer, no matter the size of the data. If we take the hashing algorithm from before, and run the word MOON through it, we’ll get the integer 57 as our hash. If we run DOG through, we get 26. Not only is comparing two integers an O(1) task, but in real terms it’s one of the fastest operations a computer can perform. We can quickly determine that these two strings are not the same. In fact, hashing is so efficient that whenever you see a comparison getting made between complex data, hashes are probably used somewhere in the implementation of that comparison. But wait, DOG hashes out to a value of 26. The letter ‘Z’ by itself would also return the same hash!  Obviously DOG is not the same String as Z, but if we only compared the hashes, the comparison would return true. This is called a collision, and it’s guaranteed to happen with any hashing function. The reasoning is this: A hashing function’s job is to convert data from some arbitrary size into data of a fixed size. If the size of the input data is greater than the size of the output data, then there is guaranteed to be two permutations of input that will generate the same output. Here’s another way of thinking about it:if you have 366 people in a room, each born on a different day of the year (counting February 29th), and you add a 367th person, the newcomer must have the same birthday as someone else in the room – there’s only 366 possible days in a year. When you use a hashing function and treat the resulting hashes as unique, you need to account for collisions somehow. As I mentioned before, hashes are often used to create more efficient data structures. Determining if two items are equal is only an O(1) operation using their hashcode, and we can take advantage of that to build a data structure called a Hash Table, that has O(1) insertion, deletion, lookup, and search times across the board. We start with an array, which is already a pretty speedy data structure. A hash table should also be able to store items as key-value pairs. In other words, we want to be able to retrieve an item by only supplying a key. We want to be able to use the hash of that key as the index for the item itself, because then we can search the table for an item just by computing its key’s hash. Now, this is going to run into a problem – we need a way of handling collisions. An array can only hold one element per index, and if each index is supposed to be a hash, then we could end up needing to store the multiple items in one index. This is usually worked around by having the array hold linked lists instead of items. These are called buckets, and items that generate the same hash can be thrown in the same bucket. For example, if we have an array backing our hash table, both DOG and Z would get placed in the bucket for hash code 26. If we wanted to search the hash table to see if it contains the item “DOG”, we would first use the hash code to get the index – O(1), and then iterate through the linked list to find “DOG” – an O(n) operation. So we can see that buckets solve our collision problem, but they reduce the efficiency of our data structure where the buckets have more than 1 item in them. This is a real problem, and the development of effective hash tables is a real concern in software development. If you know the exact elements your hash table will need to store ahead of time, you could create a perfect hash function and a perfect hash table with no collisions. But another problem is this – our hash function returns a 32-bit int, which has a range of 2^32 possible values. An array of integers of size 2^32, where each integer takes 4 bytes of memory would take 16 GB of memory. So we need a way to essentially reduce the size of our array, and thus the number of buckets that we have. This compression will lead to scenarios though, where two items might end up placed in the same bucket even through their hashes don’t actually collide. In other words, efficiency is lowered further. Now, these examples aren’t geared toward practicality, just illustration. So let’s have our backing array be size 100. We’ll figure out which index an item should be placed into by taking its hash, and using the modulo operator to find it’s remainder after dividing it by 100. This will generate a number between 0 and 99. Finally, we can start to build our hash table. Here’s what it looks like. Our hash table is backed by an array of linked list head nodes, and the size of that array is 100. Nodes in this structure store both a key and the data value we expect them to. 

```
structure HashTable is
  let nodes[] be an array of LLs, of size 100.
    Each node stores a key and the data
    
  algorithm clear is
    let i = 0
    while (i < nodes.size)
      nodes[i] = null
      i = i + 1
      
  algorithm insert is
    input: key - for the item to be stored
      data - the item to be stored
      
    let newNode = new Node(key, data)
    let hash = basicHashFunction(key)
    
    if (nodes[hash % nodes.length] == null)
      nodes[hash % nodes.length] = newNode
    else
      nodes[hash % nodes.length].add(newNode)
      
  algorithm get is
    input: key - for the item to be retrieved
    output: the item with the given key
    
    let hash = basicHashFunction(key)
    let linkedListNode = nodes[hash % nodes.length]
    
    if (linkedListNode != null)
      while (linkedListNode.next != null)
        if (linkedListNode.key == key)
          return linkedListNode.data
        linkedListNode = linkedListNode.next
        
    return null
    
  algorithm remove is
    input: key - for the item to be removed
    output: the item removed from the hash table
    
    let hash = basicHashFunction(key)
    let linkedListNode = nodes[hash % nodes.length]
    
    while (linkedListNode.next != null)
      if (linkedListNode.key == key)
        return linkedListNode.remove().data
        
    return null
```

Our clear algorithm iterates through the array and sets every index to null, effectively emptying it. The insert algorithm takes a key and a value to store, and uses both to create a new node for a linked list. Then the linked list at the proper index of the backing array is retrieved – first by computing the hash, and then using the modulo operator to retrieve an index between 0 and 99. The new node becomes the linked list head node if there isn’t one, or it’s added to an existing linked list. Our get algorithm first computes the hash of the key, and uses that to get the linked list head node at that index. If it exists, we iterate through the linked list to see if the provided key matches that of any items in the list at that location. We return the first data value that matches the key. Note that we do not expressly forbid duplicate keys in our insert algorithm, we just ensure that only the first value for a given key is ever deleted or removed. If you want some practice, how would you design an algorithm to iterate through a linked list and check for a duplicate value?Removing a value works much the same as retrieving it, save that the node is fully removed from the linked list. This is just the tip of the iceberg when it comes to working with hashes. You can combine hashes and trees to create a HashMap data structure, which can be more efficient than a HashTable. You can use cryptographic hashes to encrypt and decrypt messages. You can use them to improve the efficiency of other algorithms, like determining the equality of two data structures. 
