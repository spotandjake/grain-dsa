# Interval Tree

This is an implementation of a mutable augmented interval tree in Grain. For more on interval trees, see [Wikipedia](https://en.wikipedia.org/wiki/Interval_tree). The implementation is augmented with two properties the first property is a `maxHigh` property which allows for efficient searching of intervals that overlap with a given interval, and the second property is a random priority used to improve the balance of the tree.

Documentation for the library can be found in [`./intervalTree.md`](./intervalTree.md).

In order to use this implementation in your own grain project, you can copy [`./intervalTree.gr`](./intervalTree.gr) into your project and include it as a module.

## Task System

This project uses [`Taskfile`](https://taskfile.dev/) as an easy to use task system. The dependency is completely optional, and does not affect the functionality of the library. It purely exists to make running shell commands easier. If you do not have `Taskfile` installed, you can simply run the commands in the `Taskfile` manually.

### Testing

`task test` will run the tests for the library, defined in [`./intervalTree.test.gr`](./intervalTree.test.gr). The tests do not cover every individual edge case and mostly serve as a sanity check for the library. If you find any bugs or edge cases that are not covered by the tests, please feel free to open an issue or submit a pull request with a test case and fix.

### Formatting

`task format` will format the code using the standard grain formatter.

### Documentation

`task doc` will generate the grain doc for the library. Which can be found in [`./intervalTree.md`](./intervalTree.md). The documentation is generated using the standard grain doc generator, and is based on the comments in the code. 

### Clean

`task clean` will remove any programmatically generated files, such as the documentation and build artifacts.