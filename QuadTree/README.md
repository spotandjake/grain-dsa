# Region Quad Tree

This is a simple implementation of an immutable region quad tree, in grain. It is designed to be used as a spatial index for 2D data, such as images. The quad tree is immutable meaning that once it is created, it cannot be modified. For more information on region quad trees see the [wiki](https://en.wikipedia.org/wiki/Quadtree#Region_quadtree).

Documentation for the library can be found in [`./regionQuadTree.md`](./regionQuadTree.md).

In order to use this implementation in your own grain project, you can copy [`./regionQuadTree.gr`](./regionQuadTree.gr) into your project and include it as a module.

## Task System

This project uses [`Taskfile`](https://taskfile.dev/) as an easy to use task system. The dependency is completely optional, and does not affect the functionality of the library. It purely exists to make running shell commands easier. If you do not have `Taskfile` installed, you can simply run the commands in the `Taskfile` manually.

### Testing

`task test` will run the tests for the library, defined in [`./regionQuadTree.test.gr`](./regionQuadTree.test.gr). The tests do not cover every individual edge case and mostly serve as a sanity check for the library. If you find any bugs or edge cases that are not covered by the tests, please feel free to open an issue or submit a pull request with a test case and fix.

### Formatting

`task format` will format the code using the standard grain formatter.

### Documentation

`task doc` will generate the grain doc for the library. Which can be found in [`./regionQuadTree.md`](./regionQuadTree.md). The documentation is generated using the standard grain doc generator, and is based on the comments in the code. 

### Clean

`task clean` will remove any programmatically generated files, such as the documentation and build artifacts.