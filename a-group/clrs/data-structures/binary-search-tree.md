# Binary Search Tree

The search tree data structure supports many dynamic-set operations, including SEARCH, MINIMUM, MAXIMUM, PREDECESSOR, SUCCESSOR, INSERT, and DELETE. Thus, we can use a search tree both as a dictionary and as a priority queue.

The keys in a binary search tree are always stored in such a way as to satisfy the **binary-search-tree property**:&#x20;

{% hint style="info" %}
Let x be a node in a binary search tree. If y is a node in the left subtree of x, then y.key <= x.key. If y is a node in the right subtree of x, then y.key >= x.key.
{% endhint %}

## Minimum and maximum

#### TREE-MINIMUM(x)

```bash
while x.left != NIL
    x = x:left
return x
```

#### TREE-MAXIMUM(x)

```bash
while x.right != NIL
    x = x.right
return x
```

## Successor and predecessor

#### TREE-SUCCESSOR(x)

```bash
if x.right != NIL
    return TREE-MINIMUM(x.right)
y = x.p
while y != NIL and x == y.right
    x = y
    y = y.p
return y
```

#### TREE-PREDECESSOR(x)

```bash
if x.left != NIL
    return TREE-MAXIMUM(x.left)
y = x.p
while y != NIL and x == y.left
    x = y
    y = y.p
return y
```

## Insertion

#### TREE-INSERT(T,z)

```bash
y = NIL
x = T.root
while x != NIL
    y = x
    if z.key < x.key
        x = x.left
    else x = x.right
z.p = y
if y == NIL
    T.root = z // tree T was empty
elseif z.key < y.key
    y.left = z
else y.right = z
```

## Deletion

When TRANSPLANT replaces the subtree rooted at node _u_ with the subtree rooted at node _v_, node _u_’s parent becomes node _v_’s parent, and _u_’s parent ends up having _v_ as its appropriate child.

#### TRANSPLANT(T, u, v)

```bash
if u.p == NIL
    T.root = v
elseif u == u.p.left
    u.p.left = v
else u.p.right = v
if v != NIL
    v.p = u.p
```

#### TREE-DELETE(T,z)

```bash
if z.left == NIL
    TRANSPLANT(T, z, z.right)
elseif z.right == NIL
    TRANSPLANT(T, z, z.left)
else 
    y = TREE-MINIMUM(z.right)
    if y.p != z
        TRANSPLANT(T, y, y.right)
        y.right = z.right
        y.right.p = y
    TRANSPLANT(T, z, y)
    y.left = z.left
    y.left.p = y
```
