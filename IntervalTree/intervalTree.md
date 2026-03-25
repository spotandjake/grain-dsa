---
title: IntervalTree
---

An implementation of an augmented interval tree in Grain.

This tree is augmented with a random priority used to help maintain balance and a maxHigh field
used to optimize overlap queries.

## Types

Type declarations included in the IntervalTree module.

### IntervalTree.**Tree**

```grain
type Tree<a>
```

An augmented interval tree.

## Values

Functions and constants included in the IntervalTree module.

### IntervalTree.**make**

```grain
make: (seed: Uint64) => Tree<a>
```

Creates a new interval tree.

Parameters:

| param  | type     | description                                                                      |
| ------ | -------- | -------------------------------------------------------------------------------- |
| `seed` | `Uint64` | The seed for the random generator used to assign priorities to nodes in the tree |

Returns:

| type      | description               |
| --------- | ------------------------- |
| `Tree<a>` | A new empty interval tree |

### IntervalTree.**reset**

```grain
reset: (self: Tree<a>) => Void
```

Empties the given interval tree.

Parameters:

| param  | type      | description                     |
| ------ | --------- | ------------------------------- |
| `self` | `Tree<a>` | The interval tree to be emptied |

### IntervalTree.**isEmpty**

```grain
isEmpty: (self: Tree<a>) => Bool
```

Checks if the given interval tree is empty

Parameters:

| param  | type      | description                       |
| ------ | --------- | --------------------------------- |
| `self` | `Tree<a>` | The interval tree to be inspected |

Returns:

| type   | description                                    |
| ------ | ---------------------------------------------- |
| `Bool` | `true` if the tree is empty, `false` otherwise |

### IntervalTree.**size**

```grain
size: (self: Tree<a>) => Number
```

Returns the size of the given interval tree.

Parameters:

| param  | type      | description                  |
| ------ | --------- | ---------------------------- |
| `self` | `Tree<a>` | The interval tree to inspect |

Returns:

| type     | description                     |
| -------- | ------------------------------- |
| `Number` | The number of nodes in the tree |

### IntervalTree.**add**

```grain
add: (period: Range<a>, self: Tree<a>) => Void
```

Adds a new interval to the tree.

Time Complexity: O(log n)

Parameters:

| param    | type       | description                                           |
| -------- | ---------- | ----------------------------------------------------- |
| `period` | `Range<a>` | The interval to be added                              |
| `self`   | `Tree<a>`  | The interval tree to which the interval will be added |

### IntervalTree.**remove**

```grain
remove: (period: Range<a>, self: Tree<a>) => Void
```

Removes a new interval from the tree.

Time Complexity: O(log n)

Parameters:

| param    | type       | description                                             |
| -------- | ---------- | ------------------------------------------------------- |
| `period` | `Range<a>` | The interval to be removed                              |
| `self`   | `Tree<a>`  | The interval tree of which the interval will be removed |

### IntervalTree.**contains**

```grain
contains: (period: Range<a>, self: Tree<a>) => Bool
```

Checks if the tree contains a given interval.

Time Complexity: O(log n)

Parameters:

| param    | type       | description                                     |
| -------- | ---------- | ----------------------------------------------- |
| `period` | `Range<a>` | The interval to be checked for containment      |
| `self`   | `Tree<a>`  | The interval tree to be checked for containment |

Returns:

| type   | description                                                       |
| ------ | ----------------------------------------------------------------- |
| `Bool` | `true` if the tree contains the given interval, `false` otherwise |

### IntervalTree.**overlap**

```grain
overlap: (period: Range<Number>, self: Tree<Number>) => Option<Range<Number>>
```

Finds an interval in the tree that overlaps with the given interval.

Parameters:

| param    | type            | description                                 |
| -------- | --------------- | ------------------------------------------- |
| `period` | `Range<Number>` | The interval to be checked for overlap      |
| `self`   | `Tree<Number>`  | The interval tree to be checked for overlap |

Returns:

| type                    | description                                                                    |
| ----------------------- | ------------------------------------------------------------------------------ |
| `Option<Range<Number>>` | Some(interval) if there is an overlapping interval in the tree, None otherwise |

### IntervalTree.**toString**

```grain
toString: (self: Tree<a>) => String
```

Prints the given tree in a human readable format.

Parameters:

| param  | type      | description            |
| ------ | --------- | ---------------------- |
| `self` | `Tree<a>` | The tree to be printed |

