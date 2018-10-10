###checklist
- list copy  append
- `//` devide

### for loop for list
If you need to modify the sequence you are iterating over while inside the loop (for example to duplicate selected items), it is recommended that you first make a copy. Iterating over a sequence does not implicitly make a copy. The slice notation makes this especially convenient:

```
>>>
>>> for w in words[:]:  # Loop over a slice copy of the entire list.
...     if len(w) > 6:
...         words.insert(0, w)
...
>>> words
['defenestrate', 'cat', 'window', 'defenestrate']
```

```
>>> list(range(5))
[0, 1, 2, 3, 4]
```

```
if len(matrix[0]) == 1:
    return [col_val for row in matrix for col_val in row]

blocked = [[False for n in range(len(matrix[0]))] for m in range(len(matrix))]
```

#### enumerate for list
```
>>> elements = ('foo', 'bar', 'baz')
>>> for elem in elements:
...     print elem
... 
foo
bar
baz
>>> for count, elem in enumerate(elements):
...     print count, elem
... 
0 foo
1 bar
2 baz
```

####empty list 
```
self.storedNodes != []
```

#### item for dict
```
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...
gallahad the pure
robin the brave
```


### function
#### parameter
Default parameter:

```
def foo(val, arr=[]):
    arr.append(val)
    return arr
```
When using the function:

print(foo(1))  
[1]  
print(foo(2))  
[1, 2]  
This happens because the default value (an empty list) was evaluated once, when the function was compiled, then re-used on every call to the function. To get an empty list on every call, the code needs to be written like this:

```
def foo(val, arr=None):
    if arr is None:
        arr = []
    arr.append(val)
    return arr
```

Pass by Object reference:

In many cases these side effects are wanted, i.e. they are part of the functions specification. But in other cases, they are not wanted , they are hidden side effects. In this chapter we are only interested in the side effects, which change global variables, which have been passed as arguments to a function. 
Let's assume, we are passing a list to a function. We expect that the function is not changing this list. First let's have a look at a function which has no side effects. As a new list is assigned to the parameter list in func1(), a new memory location is created for list and list becomes a local variable.

```
>>> def func1(list):
...     print list
...     list = [47,11]
...     print list
... 
>>> fib = [0,1,1,2,3,5,8]
>>> func1(fib)
[0, 1, 1, 2, 3, 5, 8]
[47, 11]
>>> print fib
[0, 1, 1, 2, 3, 5, 8]
>>> 
```
This changes drastically, if we include something in the list by using +=. To show this, we have a different function func2() in the following example:

```
>>> def func2(list):
...     print list
...     list += [47,11]
...     print list
... 
>>> fib = [0,1,1,2,3,5,8]
>>> func2(fib)
[0, 1, 1, 2, 3, 5, 8]
[0, 1, 1, 2, 3, 5, 8, 47, 11]
>>> print fib
[0, 1, 1, 2, 3, 5, 8, 47, 11]
>>> 
```

#### various number of parameter

```
def formatString(stringTemplate, *args, **kwargs):
    # Replace any positional parameters
    for i in range(0, len(args)):
        tmp = '{%s}' % str(1+i)
        while True:
            pos = stringTemplate.find(tmp)
            if pos < 0:
                break
            stringTemplate = stringTemplate[:pos] + \
                             str(args[i]) + \
                             stringTemplate[pos+len(tmp):]
 
    # Replace any named parameters
    for key, val in kwargs.items():
        tmp = '{%s}' % key
        while True:
            pos = stringTemplate.find(tmp)
            if pos < 0:
                break
            stringTemplate = stringTemplate[:pos] + \
                             str(val) + \
                             stringTemplate[pos+len(tmp):]
 
    return stringTemplate
```
 
Here it is in action:

```
stringTemplate = 'pos1={1} pos2={2} pos3={3} foo={foo} bar={bar}'
print(formatString(stringTemplate, 1, 2))
pos1=1 pos2=2 pos3={3} foo={foo} bar={bar}
print(formatString(stringTemplate, 42, bar=123, foo='hello'))
pos1=42 pos2={2} pos3={3} foo=hello bar=123
```

### data structure

#### stack
```
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
```

#### queue

```
>>> from collections import deque
>>> queue = deque()
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> a = queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```

#### heap

How to use PriorityQueue

```
from queue import PriorityQueue

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        counter = 0
        head = point = ListNode(0)
        q = PriorityQueue()
        for l in lists:
            if l:
                q.put((l.val,counter, l))
                counter += 1
        while not q.empty():
            val, _counter, node = q.get()
            point.next = ListNode(val)
            point = point.next
            node = node.next
            if node:
                q.put((node.val, counter, node))
                counter += 1
        return head.next
        
```    

How to use heapq:

```
from heapq import heappush, heappop, heapify

class Node:
    def __init__(self, val):
        self.val = val


if __name__ == '__main__':
    # if Node can't be compared, let's have a 3-tuple list
    arr = [(2, 1, Node(3)), (3, 5,  Node(4)), (3, 2, Node(4))]
    heapify(arr)
    heappush(arr, (2, 4,  Node(5)))
    print(heappop(arr))
    print(heappop(arr))
    print(heappop(arr))
    print(heappop(arr))

```

###check empty
`if matrix is None or len(matrix) == 0:`
or 
` if matrix == []`

###class variable

```
class Solution:
    leastNum = [0] #class variable list here
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        """
        #leastNum = [0] * (n + 1)
        
        for num in range(len(self.leastNum), n+1):
            root = 1
            curMin = num
            while root * root <= num:
                # math.floor(math.sqrt(num))
                curMin = min(curMin, self.leastNum[num - root * root] + 1)
                root = root + 1
            #leastNum[num] = curMin
            self.leastNum.append(curMin)
        return self.leastNum[n]
```

```
solution = Solution()
solution.numSquares(3)
solution.numSquares(5)
solution.numSquares(33)
...
```

### dict

```
d = {}
d = {key:value}
d[new_key] = new_value

dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
dict['Age'] = 8; # update existing entry
dict['School'] = "DPS School"; # Add new entry

print "dict['Age']: ", dict['Age']
print "dict['School']: ", dict['School']

```

### sort

```
# in place list sort tuples based on second element:
my_list.sort(key=lambda x: x[1])

# create a new list
newList = sorted([('abc', 121),('abc', 231),('abc', 148), ('abc',221)], key=lambda x: x[1])
```
