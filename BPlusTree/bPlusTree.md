---
title: BPlusTree
---

## Types

Type declarations included in the BPlusTree module.

### BPlusTree.**BPlusTree**

```grain
type BPlusTree<kType, rType>
```

A B+tree data structure.

A B+tree is a variant of a B-tree in which each node contains only keys,
and to which an additional level of indirection is added to allow for efficient range queries
In a B+tree, all values are stored in the leaf nodes, and the internal nodes only store keys
to guide the search process.

WIKI: https://en.wikipedia.org/wiki/B%2B_tree

## Values

Functions and constants included in the BPlusTree module.

### BPlusTree.**make**

```grain
make: (rank: Uint32) => BPlusTree<a, b>
```

Constructs an empty B+tree with the given rank.

Time Complexity: O(1)

Parameters:

| param  | type     | description                                                                      |
| ------ | -------- | -------------------------------------------------------------------------------- |
| `rank` | `Uint32` | The rank of the B+tree, which determines the maximum number of keys in each node |

Returns:

| type              | description                             |
| ----------------- | --------------------------------------- |
| `BPlusTree<a, b>` | An empty B+tree with the specified rank |

Throws:

`Failure(Message)`

* If the rank is less than 3, since a B+tree of rank less than 3 cannot maintain its properties

### BPlusTree.**isEmpty**

```grain
isEmpty: (tree: BPlusTree<a, b>) => Bool
```

Checks if the B+tree is empty, meaning it contains no entries.

Time Complexity: O(1)

Parameters:

| param  | type              | description                       |
| ------ | ----------------- | --------------------------------- |
| `tree` | `BPlusTree<a, b>` | The B+tree to check for emptiness |

Returns:

| type   | description                                      |
| ------ | ------------------------------------------------ |
| `Bool` | `true` if the B+tree is empty, `false` otherwise |

### BPlusTree.**search**

```grain
search: (key: kType, tree: BPlusTree<kType, rType>) => Option<rType>
```

Retrieves the value associated with a given key in the B+tree.

Time Complexity: O(log n) where n is the number of keys in the tree

Parameters:

| param  | type                      | description                         |
| ------ | ------------------------- | ----------------------------------- |
| `key`  | `kType`                   | The key to search for in the B+tree |
| `tree` | `BPlusTree<kType, rType>` | The B+tree to search within         |

Returns:

| type            | description                                                                   |
| --------------- | ----------------------------------------------------------------------------- |
| `Option<rType>` | `Some(rType)` if the key is found in the tree, `None` if the key is not found |

### BPlusTree.**range**

```grain
range: (k1: kType, k2: kType, tree: BPlusTree<kType, rType>) => List<rType>
```

Retrieves a list of values associated with keys in the range [k1, k2] in the B+tree.

Time Complexity: O(log n + m) where n is the number of keys in the tree and m is the number of keys in the range [k1, k2]

Parameters:

| param  | type                      | description                      |
| ------ | ------------------------- | -------------------------------- |
| `k1`   | `kType`                   | The lower bound of the key range |
| `k2`   | `kType`                   | The upper bound of the key range |
| `tree` | `BPlusTree<kType, rType>` | The B+tree to search within      |

Returns:

| type          | description                                                  |
| ------------- | ------------------------------------------------------------ |
| `List<rType>` | A list of values corresponding to keys in the range [k1, k2] |

### BPlusTree.**insert**

```grain
insert: (key: kType, value: rType, tree: BPlusTree<kType, rType>) => Void
```

Inserts a new entry into the B+tree.

Time Complexity: O(log n) where n is the number of keys in the tree.

Parameters:

| param   | type                      | description                                       |
| ------- | ------------------------- | ------------------------------------------------- |
| `key`   | `kType`                   | The key to insert into the B+tree                 |
| `value` | `rType`                   | The value to associate with the key in the B+tree |
| `tree`  | `BPlusTree<kType, rType>` | The B+tree to insert the record into              |

Throws:

`DuplicateKey`

* If a duplicate key is used, since B+trees do not allow duplicate keys

### BPlusTree.**bulkInsert**

```grain
bulkInsert:
  (records: List<(kType, rType)>, tree: BPlusTree<kType, rType>) => Void
```

Performs a bulk insert of a list of records into the B+tree.
This is more efficient than inserting each record individually, since we can build the tree in a bottom-up manner.

Time Complexity: O(n) in the sorted case, O(n log n) in the unsorted case due to the initial sort

Parameters:

| param     | type                      | description                                                                                        |
| --------- | ------------------------- | -------------------------------------------------------------------------------------------------- |
| `records` | `List<(kType, rType)>`    | The list of records to insert into the B+tree, where each record is a tuple of (key, value)        |
| `tree`    | `BPlusTree<kType, rType>` | The B+tree to insert the records into, which must be empty (i.e., it must not contain any entries) |

Throws:

`DuplicateKey`

* If a duplicate key is found in the list of records, since B+trees do not allow duplicate keys

### BPlusTree.**delete**

```grain
delete: (key: kType, tree: BPlusTree<kType, rType>) => Bool
```

### BPlusTree.**merge**

```grain
merge:
  (tree1: BPlusTree<kType, rType>, tree2: BPlusTree<kType, rType>) =>
   BPlusTree<kType, rType>
```

Merges two B+trees into a single B+tree containing all the entries from both trees.

NOTE: The new tree will have the same rank as `tree1`

Time Complexity: O(n + m) note that this is only the optimal time complexity if entires from both trees interleave a lot is worse because we have todo a lot of sorting, we could sort faster but its not worth it.

Parameters:

| param   | type                      | description                |
| ------- | ------------------------- | -------------------------- |
| `tree1` | `BPlusTree<kType, rType>` | The first B+tree to merge  |
| `tree2` | `BPlusTree<kType, rType>` | The second B+tree to merge |

Returns:

| type                      | description                                                   |
| ------------------------- | ------------------------------------------------------------- |
| `BPlusTree<kType, rType>` | A new B+tree containing all the entries from both input trees |

### BPlusTree.**fromList**

```grain
fromList:
  (rank: Uint32, list: List<(kType, rType)>) => BPlusTree<kType, rType>
```

Constructs a B+tree from a list of records.

TODO: Determine timeComplexity based off bulkInsert

Parameters:

| param  | type                   | description                                   |
| ------ | ---------------------- | --------------------------------------------- |
| `rank` | `Uint32`               | The rank of the B+tree to construct           |
| `list` | `List<(kType, rType)>` | The list of records to insert into the B+tree |

Returns:

| type                      | description                                       |
| ------------------------- | ------------------------------------------------- |
| `BPlusTree<kType, rType>` | A B+tree containing all the records from the list |

Throws:

`DuplicateKey`

* If a duplicate key is found in the list

## BPlusTree.Visualize

This submodule provides functionality to visualize the structure of the B+tree.

### Values

Functions and constants included in the BPlusTree.Visualize module.

#### BPlusTree.Visualize.**toMermaid**

```grain
toMermaid: (tree: BPlusTree<a, b>) => String
```

Generates a Mermaid graph representation of the B+tree, which can be used to visualize the structure of the tree.

Time Complexity: O(n) where n is the number of nodes in the tree, since we need to visit each node once to generate the graph

Parameters:

| param  | type              | description             |
| ------ | ----------------- | ----------------------- |
| `tree` | `BPlusTree<a, b>` | The B+tree to visualize |

Returns:

| type     | description                                                        |
| -------- | ------------------------------------------------------------------ |
| `String` | A string containing the Mermaid graph representation of the B+tree |

#### BPlusTree.Visualize.**toDot**

```grain
toDot: (tree: BPlusTree<a, b>) => String
```

Generates a GraphViz graph representation of the B+tree, which can be used to visualize the structure of the tree.

Time Complexity: O(n) where n is the number of nodes in the tree, since we need to visit each node once to generate the graph

Parameters:

| param  | type              | description             |
| ------ | ----------------- | ----------------------- |
| `tree` | `BPlusTree<a, b>` | The B+tree to visualize |

Returns:

| type     | description                                                         |
| -------- | ------------------------------------------------------------------- |
| `String` | A string containing the GraphViz graph representation of the B+tree |

