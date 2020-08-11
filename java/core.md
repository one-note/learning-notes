# core

## oops
* class vs interface
* annonymous class or interface.
* marker interface. can we write custom interface.
* explain system.out.println
* static vs non-static variables
* static vs non-static blocks
* static vs non-static methods
* constructor overloading
* method overloading
* use of this keyword
* use of super keyword
* super() vs this()
* constructor in inheritance (compilation and use super(x))
* singleton class early loading & lazy loading.
* Class.forName(fullyQualifiedlClassName). which exception it throws.
* data types. wrapper types. Float Vs Double
* Integer cache.

* interface vs abstrcat class (strategy vs template design pattern)
* method overriding from abstract class
* method implementaion from interface.
* interface extending anoter interface.
* abstract subclass extends abstrcat class or implements interface.

* method overriding. modifiers, return types (covariant?)., parameters(covariant?), method name, throws exception(covariant type)
* overriding only equals method.
* == vs equals
* Immutable class containing mutable field. don't allow mutable field modification as it is part of the immutable field.
* run code with java -jar
* jdk, jre jvm.
* javac vs java. where these are located in your laptop.
* what is bytecode. why java is portable.
* jar vs war vs ear.


## collections

* Interfaces in collection.
* Enumeration vs Iterator.
* Iterator vs ListIterator
* ArrayList vs LinkedList
* Given a list of students(name, percentage). group them by thr ranks. 0-30% - 3rd, 30-60% - 2nd , 60-100 - first. Use hashmap.
* Give a string. Map the words by the initial character of each word.
* Anagram string.

* stack vs queue.
* balanced parantheses example in stack.
* Iterate using iterator, for loop. Think a scenario where you need to use continue or break in a for loop.

* what are the arraylist methods.
* removeAll vs retainAll.

* given employees with id(int), name, salary(double)
* Sort employee list by name using comparable or compartor.
* Sort employee list, if salary is same then sort by name.

* reverse a array list with recursion.
* binary search in an array list.
* find the missing number in array of 1 to n
* find the occurance of a number in a sorter array. ( no hashmap , use binary search)
* code to create custom list add / iterate operations
* delete the given node (head is not given)
* find the merging point of 2 linked list.
* merge 2 sorted linked list or array list. (hard)
* write a custome iterator to iterateover arraylist.

* hashmap internal with key conflict using get and put.
* hashmap threshold.
* hashmap rehashing.
* structure of Map.Entry<K,V>
* map operations with entrySet, keySet
* Let say you create a new hashmap. what does put(k1,v1) and put(k1,v2) returns. 

* do operations like put, get , remove, size
* equals return true always. hashcode returns id of the employee.
* equals return true always. hashcode return random number of the employee.
* equals return false always. hashcode returns id of the employee.
* equals return false always. hashcode return random number of the employee.
* equals compare id. hashcode returns id.

* hashtable vs hashmap
* hashtable vs synchronizedmap
* custom synchronized for Colections.SynchronizedMap
* Treemap without comparator (means the key class need to implements comparable, else class cast exception)
* Treemap is sorted. so does it uses equals & hashcode for the key for comparison or it uses comparable( or comparator)
* Treemap has parameter as a compartor. also the key class implements comparable. on which basics the keys will be sorted in the treemap.

* concurrent collections for list and map.
* unmodiable collections 
* synchronized collections
* empty collections.

* What is the internal for hashset.
* what is weak hashmap.
* what is identity hashmap.
* what is enum map.

* what is multi value map. ( Http Headers is an example of multivalue map. How to create custom multi value map)
* when concurrent modification occurs. how to avoid that.
* concurrent collections.

### collections time complexity (add, remove, get) and why
* arraylist, linkedlist, hashmap, treemap, priority queue, blocking queue.
* Does priority queue sorted. Internal of priproty queue.
* Does treemap uses equals and hashcode.
* How blocking queue works internally.

## Exceptions

* Checked Exception vs RuntimeException
* Custom Checked Exception creation and when to use.
* Custom runtime exception creation and when to use.
* ClassNotFoundException vs NoClassDefFoundError.
* Can we catch Error.
* try with multi catch and order of exceptions.
* System.exit(0) and finally block execution.
* Name some checked exceptions and runtim exceptions in java.
* when we shoould use user defined checked exception.

## Multi Threading & Executor Service
* creating threads with extends or implements.
* adding callbacks to threads
* join vs join(ms), wait vs wait(ms)
* synchronization ( locking on method or block )
* deadloack creation.
* wait, notify, notifyall
* producer and consume problem. print even odd using 2 threads.
* use of blocking queue in multithreading. Does blocking queue uses wait, notify.
* executor services, singleThread, fixedThread, cachedThread. 
* Countdown Latch, Cyclcic Barrier.
* callable, future object
* design a custom callable
* completable future.

## Design Patterns
* singleton
* factory
* abstract factory
* state
* visitor
* strategy ( interface )
* template method ( abstrcat class )
* observer (observer vs pub / sub)

## File IO

## Non Blocking IO


