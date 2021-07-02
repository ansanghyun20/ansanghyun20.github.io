---
layout: post
title: Swift Syudy! - 2
subtitle: Data Structure
categories: swift
tags: [swift]
---
   
This time, I focused on the data structure.

### Set

I know two characteristics about this.

1. There is no order.
2. There is no duplicate data.

This can be found out through examples.

```swift

var a : Set = [1,2,3,1,1,1]
print(a)

```

![image](https://user-images.githubusercontent.com/62547169/123563752-54849f80-d7f1-11eb-90b7-4b0d6b77aeeb.png)

The datatype can be used as a Set and elements can be listed in [ ].


#### Add elements

In an arrangement, elements are added as follows.

```swift
var b : [Int] = [1,2,3]
b.append(5)
print(b)
```

So then, How to insert datatype at Set?

Yeah, that's the insert.

```swift
var a : Set = [1,2,3,1,1,1]
a.insert(5)
print(a)
```

![image](https://user-images.githubusercontent.com/62547169/123564193-55b6cc00-d7f3-11eb-9743-3cb551b0c7d5.png)


By executing this code, you can see that the element has been added.


#### It's good to know.


```swift
var a : Set = [1,2,3,1,1,1]
a.insert(5)     // add element
print(a.count)  // count
print(a.contains(3))  // include?
print(a.isEmpty)
a.remove(3)
print(a)
print(a.max())  // max
```

![image](https://user-images.githubusercontent.com/62547169/123564599-f8237f00-d7f4-11eb-81b9-f00a2cde7675.png)



























