# trees-and-graphs

Trees and graphs can easily be some of the most confusing data structures
you’ll encounter in your time as a developer. They are more complicated to
search than other algorithms, but this is where they shine: while their
searching and sorting algorithms might be more complicated to write, trees and
graphs can be designed to perform those functions with lower time complexity
than many other data structures. Their structure also makes them perfect for
emulating some natural structures, like friend relationships or internet
hierarchies. 

A graph is a series of nodes that each may or may not have child nodes. These
nodes may direct to each other in a circular fashion, and they may be
bi-directional, i.e. nodes A and B both have each other as child nodes.  It’s
also possible to have isolated subgraphs – that is, collections of nodes that
are part of the same graph, but no connection exists between them. 

As you can see, graphs can be complicated, messy, and disorganized. It’s rare
that you would ever transform data into a graph to make searching or sorting it
faster, but you will use them to emulate real life data structures. As
previously mentioned, you could use them for mapping out the web of friend
relationships on social media, or to represent intersections from a street map.
But whatever data you are representing with a graph, you’re most often going to
be using the graph in searches. 

When searching a graph, there are two common approaches: breadth-first search,
and depth-first search. Both searches start at the head or root node. In a
depth-first search, you then progress through each branch completely before
moving on to the next branch. This is best used when you are searching for a
specific node, or when you want to guarantee that you check every one. In a
breadth-first search, you explore each neighbor before moving on to any
children. This is useful when you’re trying to find a path from A to B. 

A depth-first search uses this algorithm. You’ll notice two things about this
algorithm: 

```
algorithm DFS is
  input: currentNode - the node being searched,
    target - the target node value being searched for
    
  outpu: the node containing the desired value
  
  if (currentNode == null)
    return null
    
  if (currentNode.data == target)
    return currentNode
    
  currentNode.visited = true
  
  for each (Node n in currentNode.children)
    if (n.visited == false)
      DFS(n)
  
  return null
```

first, you’ll need some way of tracking whether a node has been visited already
or not. Without this, you would search one branch all the way down to the
lowest level child node, then loop back up to its parent, and then search the
child node again in an infinite loop. The second thing you should notice is
that this algorithm is recursive – that is, it calls itself with new data every
time it runs, until it is done. 

Here’s a visualization of a DFS in action. We start at A, our root node, and we
are searching for ‘E’. A isn’t our target, so we mark A as visited and start
searching the children. The first child we visit is C, which doesn’t match the
value we’re looking for. We mark C as visited, and search its children. F isn’t
our target, so its marked as visited, but F also has no children, so the for
each loop is skipped. This search returns null. Now the loop that was started
when we searched C can continue, and we search G. Go doesn’t match, so we
search its child H. H doesn’t match so we search its child D. D doesn’t match,
and D has no children – note that the links are unidirectional – so we return
null and back up to H. No more children, so H’s loop finishes and we back up to
G, then to C, then to A. C has no children that haven’t been visited so we go
back to A. A has another child, D… but D has been visited, so we move to E.
Finally, E matches our value and we return E. No more searching needed. 

While a depth-first search covers searches through every available child node
before moving to a neighbor, a breadth-first search visits every neighbor of a
node before visiting any children. A depth-first search can be written
recursively or iteratively with a stack, but a breadth-first search uses a
queue to track which nodes it still needs to visit. You typically use a BFS to
find a route from one node to another. This is an example of an iterative BFS
algorithm. 

```
algorithm BFS is
  input: first - the first node
    target: the target value being searched for
    
  output: the node containing the desired value
  
  let nodesToVisit = new Queue
  first.visited = true
  nodesToVisit.add(first)
  
  while (queue is not empty)
    let currentNode = nodesToVisit.remove()
    if (currentNode.data == target)
      return currentNode
      
    for each (Node n in currentNode.children)
      if (n.visited == false)
        n.visited == true
        nodesToVisit.add(n)
```

Starting with the first node, the current node is added to a queue. Then the
next item in the queue is removed and checked for a match. If it doesn't match,
its children are added to the back of the queue for later checking. Here we
have the same graph as shown before, but we're going to search it for E with
our BFS algorithm. A is added to the queue, then removed and checked. A doesn't
match, so we add C, D, E, and B to the queue going left to right. The next item
to get pulled from the queue is C, which doesn't match, so its children F and G
are added to the back of the queue. D is then removed and checked, and has no
match or children to queue up. Then we check E, and there's a match so the
algorithm returns that node and quits. 

So graphs can be useful structures, but they're more useful when they have some
structure and rules. That's where trees come in. We all understand what a
family tree looks like, and a tree data structure isn’t very different. They
are a subtype of graph, but do not contain any cycles, where node connections
loop back into each other. A node with no children is called a leaf node.
Oftentimes, a tree will be restricted as to how many children each node can
have. A tree that only allows two children – the most common type of tree – is
called a binary tree. 

Binary trees are used often because if they are sorted, they can be easy to
search through. A sorted binary tree is called a binary search tree, and it
requires that for every node, all lefthand children must be less than or equal
to the node, and that node must be less than all righthand children. This is an
example of a binary search tree, but this is not. The second tree fails because
each node requires that all lefthand children be less than it, and this is not
true for the root node – 15 is not less than 10. Furthermore, the rule also
states that all righthand children of a node must be greater than that node,
and 9 is not greater than 10. 

Searching a binary search tree can happen in LogN time, because the tree is
sorted. Every time you check a node, you know if the current node is less than
or greater than your target, and you can cut the remaining number of nodes in
half each time. The same goes for inserting, because you can quickly find where
an item should be inserted to maintain the sorted property. 

A binary search tree is said to be balanced when the size of each subtree for a
node is roughly the same size as all other subtrees of neighbor nodes in the
same level. This doesn't have to be exact, just close enough that the search
complexity remains close to LogN. 

A complete binary tree is a tree where every level is filled. The last level of
the tree is allowed to remain partially filled, so long as it is filled
left-to-right. 

A full binary tree is one where every level has exactly 0 or 2 children. 

A perfect binary tree is both full and complete. 

When traversing a tree and not performing a search, there are three ways of
doing so: In-order traversal, pre-order, and post-order. You should know how to
implement all of them, but thankfully they're all rather simple. An in-order
traversal visits the left child before the current node, then the right child.
This is true for every node, and the recursive algorithm looks like this. 

```
algorithm preorder is
  input: current - the current node
  
  if (current == null)
    return
    
  visit(current)
  preorder(current.left)
  preorder(current.right)
```

In a binary search tree, in-order traversal will visit every element in
ascending order. Pre-order traversal visits the current node before exploring
the left and right child, and post-order visits the node after the left and
right child. 

```
algorithm postorder is
  input: current - the current node
  
  if (current == null)
    return
    
  postorder(current.left)
  postorder(current.right)
  visit(current)
```

When implemented recursively, these algorithms are easy to differentiate and
remember.

Trees – particularly binary search trees – have a lot of uses in algorithm
design. They are also used behind the scenes to implement some advanced and
efficient data structures. Graphs make for a great approximation of real-life
structures, like internet connectivity routes, or for pathfinding in video
games. 
