---
title: RegionQuadTree
---

A generic region quad tree implemented in Grain.

Wiki: https://en.wikipedia.org/wiki/Quadtree#Region_quadtree

## Types

Type declarations included in the RegionQuadTree module.

### RegionQuadTree.**QuadTree**

```grain
enum QuadTree<a> {
  Leaf{
    size: Number,
    value: a,
  },
  Node{
    size: Number,
    northWest: QuadTree<a>,
    northEast: QuadTree<a>,
    southEast: QuadTree<a>,
    southWest: QuadTree<a>,
  },
}
```

A region quad tree is a tree data structure in which each internal node has exactly four children.

The tree is used to represent a 2D space by recursively subdividing it into four quadrants or
regions. Until each region is uniform (i.e all the values in the region are the same).
In the worse case, a region quad tree can have a depth of log(n) where n is the size of the
region, this happens when the region is subdivided until we reach 1x1 regions.
(Think of a checkerboard pattern)

Variants:

```grain
Leaf{
  size: Number,
  value: a,
}
```

A leaf node, representing a uniform region.

Fields:

| name    | type     | description                    |
| ------- | -------- | ------------------------------ |
| `size`  | `Number` | The size of the given region.  |
| `value` | `a0`     | The value of the given region. |

```grain
Node{
  size: Number,
  northWest: QuadTree<a>,
  northEast: QuadTree<a>,
  southEast: QuadTree<a>,
  southWest: QuadTree<a>,
}
```

An internal node, representing a non-uniform region.

Fields:

| name        | type           | description                           |
| ----------- | -------------- | ------------------------------------- |
| `size`      | `Number`       | The size of the given region.         |
| `northWest` | `QuadTree<a0>` | The northwest quadrant of the region. |
| `northEast` | `QuadTree<a0>` | The northeast quadrant of the region. |
| `southEast` | `QuadTree<a0>` | The southeast quadrant of the region. |
| `southWest` | `QuadTree<a0>` | The southwest quadrant of the region. |

## Values

Functions and constants included in the RegionQuadTree module.

### RegionQuadTree.**make**

```grain
make: (matrix: Array<Array<a>>, ?compress: Bool) => QuadTree<a>
```

Constructs a brand new region quad tree.

Parameters:

| param       | type              | description                                                            |
| ----------- | ----------------- | ---------------------------------------------------------------------- |
| `matrix`    | `Array<Array<a>>` | The 2D array of values to build the tree from. Must be a square array. |
| `?compress` | `Bool`            | Weather or not to compress the tree.                                   |

Returns:

| type          | description             |
| ------------- | ----------------------- |
| `QuadTree<a>` | A new region quad tree. |

Throws:

`Failure(Message)`

* If the input matrix is not a square array.

### RegionQuadTree.**compress**

```grain
compress: (tree: QuadTree<a>) => QuadTree<a>
```

Compresses a region quad tree by merging nodes that have the same value into a single leaf.

Parameters:

| param  | type          | description                       |
| ------ | ------------- | --------------------------------- |
| `tree` | `QuadTree<a>` | The region quad tree to compress. |

Returns:

| type          | description                                                                                          |
| ------------- | ---------------------------------------------------------------------------------------------------- |
| `QuadTree<a>` | A new region quad tree with the same values as the input tree, but with nodes merged where possible. |

### RegionQuadTree.**setPixel**

```grain
setPixel: (x: Number, y: Number, value: a, tree: QuadTree<a>) => QuadTree<a>
```

Switches the value at the given coordinates in the region quad tree.

Parameters:

| param   | type          | description                                   |
| ------- | ------------- | --------------------------------------------- |
| `x`     | `Number`      | The x coordinate of the value to switch       |
| `y`     | `Number`      | The y coordinate of the value to switch       |
| `value` | `a`           | The new value to set at the given coordinates |
| `tree`  | `QuadTree<a>` | The region quad tree to switch the value in   |

Returns:

| type          | description                                                                               |
| ------------- | ----------------------------------------------------------------------------------------- |
| `QuadTree<a>` | A new region quad tree with the value at the given coordinates switched to the new value. |

### RegionQuadTree.**getPixel**

```grain
getPixel: (x: Number, y: Number, tree: QuadTree<a>) => a
```

Gets the value at the given coordinates in the region quad tree.

Parameters:

| param  | type          | description                                |
| ------ | ------------- | ------------------------------------------ |
| `x`    | `Number`      | The x coordinate of the value to get       |
| `y`    | `Number`      | The y coordinate of the value to get       |
| `tree` | `QuadTree<a>` | The region quad tree to get the value from |

Returns:

| type | description                                                 |
| ---- | ----------------------------------------------------------- |
| `a`  | The value at the given coordinates in the region quad tree. |

### RegionQuadTree.**apply**

```grain
apply:
  (tree1: QuadTree<a>, tree2: QuadTree<b>, f: ((a, b) => c)) => QuadTree<c>
```

Combines the two quad trees using the given function.

Parameters:

| param   | type          | description                                                     |
| ------- | ------------- | --------------------------------------------------------------- |
| `tree1` | `QuadTree<a>` | The first region quad tree.                                     |
| `tree2` | `QuadTree<b>` | The second region quad tree.                                    |
| `f`     | `(a, b) => c` | The combining function to apply to the values of the two trees. |

Returns:

| type          | description                                                       |
| ------------- | ----------------------------------------------------------------- |
| `QuadTree<c>` | A new region quad tree that is the result of the two input trees. |

Throws:

`Failure(Message)`

* If the two input trees are of different sizes.

Examples:

```grain
apply(tree1, tree2, (a, b) => a | b) // This would be a union of two binary images represented as region quad trees.
```

### RegionQuadTree.**toMatrix**

```grain
toMatrix: (tree: QuadTree<a>) => Array<Array<a>>
```

Converts a region quad tree back into a 2D array of values.

Parameters:

| param  | type          | description                      |
| ------ | ------------- | -------------------------------- |
| `tree` | `QuadTree<a>` | The region quad tree to convert. |

Returns:

| type              | description                                                                    |
| ----------------- | ------------------------------------------------------------------------------ |
| `Array<Array<a>>` | A 2D array of values representing the same data as the input region quad tree. |

