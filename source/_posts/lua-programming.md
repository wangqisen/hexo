title: lua的遍历table过程中删除数组元素的问题
categories: Lua
tags: [Lua]
---
## 
lua脚本中并为提供Jdk类库中迭代器这样的机制来供其在动态遍历table的过程中删除元素，因此，在删除的过程中可能会因此错误。
例如以下程序：
```
local array={1, 2, 3, 4, 5, 6}
for i, element in ipairs(array) do
	if i % 2 == 0 then
		table.remove(array, i)
	end
end
```
以上程序是为了删除数组中下标为偶数的元素，但是在删除过程中，lua会把删去元素后面的元素前移，数组的下标变了，也就使得以后遍历过程中的i并不准确。

解决这个问题，有两个方法，第一个是从后向前删除元素，就像下面这样：

```
local array={1, 2, 3, 4, 5, 6}
for i=#array,1,-1 do
	if i % 2 == 0 then
		table.remove(array, i)
	end
end
```
这样尽管删除元素后面的数组元素的下标变了，但由于是由后向前删除，因此，并不影响前面的元素。这种做法在要求删除数组特定位置的元素时而不是顺序由后向前删除时就不适用了。

第二个方法，是对于i来说，如果想要保持其遍历过程中的正确的索引位置，就需要在删除时位置不动，而不删除时正常的依次加一，这样就可以保证在数组删除导致的元素前移时其位置依然正确。代码如下：

```
local array={1,2,3,4,5,6}
local i=1
while i<=#array do
	if(i%2==0) then
		table.remove(array,i)
	else 
		i=i+1
	end
end
```