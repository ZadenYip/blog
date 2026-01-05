# 红黑树改为区间树

相比于普通的红黑树，区间树的每个节点多了一个 max 属性，这个的定义是：以当前节点为根的子树中，取子树下所有节点区间的右端点的最大值。  

红黑树扩展为区间树，需要保证红黑树的原本的操作**维护**好 max 属性。此外，在这约定 T.nil 节点的 max 属性为负无穷（假设类型整数）。

**注意：key 的定义变为区间的左端点，不是整个区间**

Introduction to Algorithms 指出区间树基于红黑树扩展的，而唯一的“新”的操作函数是查询操作。 
> The only new operation is INTERVAL-SEARCH, which searches for an interval in the tree that overlaps a given interval. All the other operations on red-black trees remain the same, except that they must be modified to maintain the max fields of the nodes.

## 查询操作

没啥好说的，根据 Introduction to Algorithms 中的区间树章节实现即可，书里有现成的伪代码。

```pseudocode
INTERVAL-SEARCH(T, i)
x = T.root
while x != T.NIL and i does not overlap x.int
    if x.left != T.NIL and x.left.max >= i.low
        x = x.left
    else
        x = x.right
return x
```

overlap 这里给出伪代码实现
```pseudocode
OVERLAP(int_a, int_b)
    return int_a.low <= int_b.high and int_b.low <= int_a.high
```


## 插入操作

区间树插入和红黑树的插入类似，只是需要在插入过程中维护 max 属性。从根节点找到插入位置的过程中，沿途更新 max 属性即可。

```pseudocode
INTERVAL-INSERT(T, z)
x = T.root
y = T.NIL
while x != T.NIL
    y = x
    x.max = max(x.max, z.int.high) // 多添加的代码
    if z.int.low < x.int.low
        x = x.left
    else
        x = x.right
z.p = y
if y == T.NIL
    T.root = z
else if z.int.low < y.int.low
    y.left = z
else
    y.right = z
z.left = T.NIL
z.right = T.NIL
z.color = RED
z.max = z.int.high // 多添加的代码
INTERVAL-INSERT-FIXUP(T, z)
```

## 插入修复操作

INTERVAL-INSERT-FIXUP 和红黑树的 INSERT-FIXUP 几乎一样，只是将旋转操作改为区间树的旋转操作。因为区间树旋转时需要维护 max 属性。

红黑树基础上改区间树，旋转的操作会涉及子树下区间 max 属性的改变，因此原红黑树的左旋操作无法使用，得进行修改。
原因如下：
```
    P
    |
    x
  /   \
T1     y
      / \
    T2   T3
```

以上树为例，进行 x 左旋后变为：

```
      P
      |
      y
     / \
    x   T3
   / \
 T1   T2
```
**显然**子树 P，T1，T2，T3 max 不变，因为以它们为根的子树所有区间集合是同一个，但是 x 子树和 y 子树的 max 都要更新。 

对于 x 子树来说，右节点发生了变化，而对于 y 子树来说，左节点发生了变化，因此需要重新计算 max。 
固对 x，y 使用 node.max = max(node.int.high, node.left.int.max, node.right.int.max)  

伪代码如下：
```pseudocode
INTERVAL-LEFT-ROTATE(T, x)
y = x.right
x.right = y.left
if y.left != T.NIL
    y.left.p = x
y.p = x.p
if x.p == T.NIL
    T.root = y
else if x == x.p.left
    x.p.left = y
else
    x.p.right = y
y.left = x
x.p = y

x.max = max(x.int.high, x.left.max, x.right.max) // 多添加的代码
y.max = max(y.int.high, y.left.max, y.right.max) // 多添加的代码
```
至于右旋操作，根据对称性将 left 改为 right 即可得到对应的伪代码，对于最后两行其实 left 和 right 互换不互换都是可以的。

## 删除操作
因为我目前的项目不需要用所以没看怎么实现（

## 实际实现代码（TypeScript）

见[区间树实现](https://github.com/ZadenYip/Todo-Project/commit/3bfe072ad11a7f9b67992244c8bccee74f2b773a)，等写完项目相关模块后会给最终链接。