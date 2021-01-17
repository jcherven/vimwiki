# stacks-and-queues

Stacks and queues are two data structures that are similar to lists, but they have rules about the order in which you can access their contents. These rules make them useful for emulating real-life constructs. 

A stack is a data structure that works on a Last In First Out principle, or LIFO. When an item is added to the stack – called pushing – it’s pushed onto the top of the stack. When an item is removed from the stack – called popping – it’s popped off the top as well. You cannot insert an item to or remove one from anywhere else in the stack but the top. Additionally, you can peek at the item at the top of the stack – this returns its data without removing the item itself. 

Some languages offer a pre-built implementation for stacks, but not all of them do. For those that don’t, you should recognize their similarity to single-linked lists. Pushing a new item is the same as adding a new node as the head, and setting the “next” property to the old head. Popping is the same as removing the node that operated as the old head. Stacks thus offer constant-time inserts and deletes. 

Stacks are best used when you need to enforce an ordering for your data or processing. As an example, think of how a moving arm might be digitally rendered on a computer screen. An arm has three segments – the upper arm, the forearm, and the hand. We’re used to thinking of these as physically joined at the elbow and wrist, but this might not be true in a 3D model. If we want to describe how these parts might move through a 3D space, we can describe their movements in relation to each other. The hand rotates at an angle based off the position of the forearm. The forearm rotates in relation to the position of the upper arm. The upper arm rotates around a fixed point – the shoulder. If we know the final location where each part should be, we might think that we can just translate the parts through space, right? Well if you try this, you might see our 3D model transform into a freakish caricature. A lot of glitchy 3D animation is due to trying to render or move one component of a 3D model before the other components are ready. Using a stack, we can push the animations of the hand in relation to the forearm, the forearm in relation to the upper arm, and the upper arm onto the stack. When we animate, we’ll pop those motions off the stack in reverse order, guaranteeing a smooth motion. 

A queue is similar to a stack, but it uses FIFO ordering – First In, First Out. You can think of this like it’s literal name – a queue of people. The first person to arrive becomes the front of the line, and every new person goes to the back of the line. When you need to remove a person from the line, you always remove from the front – the first person to arrive, who’s been waiting there the longest. Queues have adding, removal, and peeking functionality just like stacks – save that they call them “adding” and “removing” instead of “pushing” and “popping”. 

They can also be implemented with a linked list, so long as you make sure to add and remove accordingly. In this case, adding an item to the back of the list might not operate in constant time – you’d have to iterate over the entire list to get to the current last item before you could add a new one. 

You can improve this by using a circular doubly-linked list. A circular linked list is pretty much what it sounds like – the last node in the list stores a reference to the head in its “next” field, creating a circular link.  In a doubly-linked list, each node has variables for both the “next” node and the “previous” node. So in a circular doubly-linked list, you can always access the last node directly from the head. This means you won’t have to iterate over the entire list to get to the last item. 

Queues are typically used for scheduling certain events to happen. A computer processor core for example, can typically do only one thing at a time. It might do one million operations in a second, but it does each one in order. Computers often make use of queues to line up operations for a processor, even while it’s in the middle of doing something else. Queues can also be used in some time of searching algorithms, which we’ll discuss more later. But you can envision trying to find your way through a maze – with each intersection you come across, you choose one path and queue the others for exploration later. 

So once again, let’s look at an example algorithm question that uses our understanding of both stacks and queues – how could you implement a queue using two stacks?Go ahead and pause here if you want to work it out. 

```
structure QueueFromStacks is
  variables:
    let oldest = new Stack
    let newest = new Stack
    
    functions:
      function add is
        input data
        
        newest.push(data)
        
      function peek is
        input: none
        output: the oldest item
        
        if (oldest is empty)
          while (newest is not empty)
            oldest.push(newest.pop())
        
        return oldest.peek()
        
      function remove is
        input: none
        output: the oldest item
        
        if (oldest is empty)
          while (newest is not empty)
            oldest.push(newest.pop())
            
        return oldest.pop()
```

Recall that the only real difference between a stack and a queue is that stacks are Last In First Out, while queues are First In First Out. In other words, removing or peeking from a queue should return the oldest element, while popping or peeking from a stack should return the newest. We can use our two stacks then to divide the elements into a stack of the newest elements, and a stack of the oldest. When a new item is added to the queue, it is pushed onto the newest stack. When an item is removed or peeked, the corresponding operation is performed on the oldest stack. When the oldest stack is empty, all the newest items are popped from the newest stack and popped onto the oldest stack. This reverses their order, so the newest item in the newest stack goes to the bottom of the oldest stack, and thus will get popped or peeked last. When the last item is removed from the oldest stack, the oldest stack is refreshed – again in reverse order – from the newest stack. 

Unfortunately, we can’t guarantee that add, remove, and peek operations work in O(1) time here. They will in the best-case scenario, but in the worst-case scenario the remove and peek operations will need to transfer all the old items from the newest stack into the oldest stack first, which could be an O(n) operation. 

Up until now we’ve been writing algorithms as standalone procedures. Some algorithms are written like this, but in object oriented programming languages you’ll often see algorithms written as functions contained inside a structure like a class. It’s the same idea, but the rules for invoking the algorithms is a little different. You invoke the function that belongs to the structure, and send in the inputs between parenthesis. Again, the exact implementation of these structures, functions, and algorithms will depend on the language you are using. 
