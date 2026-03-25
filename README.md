# Grain DataStructures

This is simple collection of data structures implemented in grain. The goal of this project is to provide a collection of commonly used generic data structures, both for use within the grain ecosystem and as a reference for implementing other data structures in grain. The data structures in this project are designed to be simple and easy to understand, rather than optimized for absolute performance. If you are looking for a high performance data structure, you may want to look elsewhere or implement your own based on the principles outlined in this project.

## Data Structures

### Interval Tree

An interval tree is a data structure that allows for efficient querying of intervals. The source can be found in [`./IntervalTree`](./IntervalTree). along with a better description in the [`./IntervalTree/README.md`](./IntervalTree/README.md).

### QuadTree
A quadtree is a tree data structure in which each internal node has exactly four children. It is commonly used to partition a two-dimensional space by recursively subdividing it into four quadrants or regions. The data structure is particularly useful for spatial indexing, such as images. The source can be found in [`./QuadTree`](./QuadTree).

### RopeString

TODO: These libraries are a work in progress and need testing, and documentation. The ropeString is missing a rebalance function.

### Trie

TODO: This library is a work in progress and needs testing, and documentation. The trie implementation is not fully complete.

## Dependencies
This project has no external library dependencies and is implemented using only the standard library of grain. The only system dependencies are listed below or in [`flake.nix`](./flake.nix). 
* `Nix` this is a completely optional dependency, purely used for managing system dependencies.
* `Taskfile` this is also a completely optional dependency, purely used for running shell commands, in a reusable and configurable way. If you do not have `Taskfile` installed, you can simply run the commands in the `Taskfile` manually.
* `Grain` of course, you will need the grain compiler to use this library. You can find instructions for installing grain on the [official grain website](https://grain-lang.org/). I aim to keep the library up to date, you can see the version of grain we are currently testing against in [`./flake.nix`](./flake.nix). If you find any compatibility issues with newer versions of grain, please feel free to open an issue or submit a pull request with a fix.

## Task System

This project uses [`Taskfile`](https://taskfile.dev/) as an easy to use task system. The dependency is completely optional, and does not affect the functionality of the library. It purely exists to make running shell commands easier. If you do not have `Taskfile` installed, you can simply run the commands in the `Taskfile` manually.

### Testing

`task test` will run the tests for each data structure. The tests are located alongside the implementation of each data structure, and are designed to be simple and easy to understand. They are not exhaustive, as this project is not intended to be production ready, but they should provide a good starting point and cover the basic functionality of each data structure. If you find any bugs or edge cases that are not covered by the tests, please feel free to open an issue or submit a pull request with a fix and additional tests.

### Formatting

`task format` will format the code using the standard grain formatter.

### Documentation

`task doc` will generate the grain doc for each data structure, which is located along with each implementation.

### Clean

`task clean` will remove any programmatically generated files, such as the documentation and build artifacts.

Copyright ©️ 2025 Jake Follest, Kara Wilson