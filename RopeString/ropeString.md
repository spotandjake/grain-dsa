---
title: RopeString
---

## Types

Type declarations included in the RopeString module.

### RopeString.**Rope**

```grain
enum Rope {
  Leaf(String),
  Node(Rope, Rope),
}
```

## Values

Functions and constants included in the RopeString module.

### RopeString.**length**

```grain
length: (rope: Rope) => Number
```

### RopeString.**make**

```grain
make: (str: String) => Rope
```

### RopeString.**insert**

```grain
insert: (rope: Rope, str: String, i: Number) => Rope
```

### RopeString.**delete**

```grain
delete: (rope: Rope, start: Number, end: Number) => Rope
```

### RopeString.**substring**

```grain
substring: (rope: Rope, start: Number, end: Number) => String
```

### RopeString.**find**

```grain
find: (rope: Rope, substr: String) => Number
```

### RopeString.**charAt**

```grain
charAt: (rope: Rope, i: Number) => Char
```

### RopeString.**indexOf**

```grain
indexOf: (rope: Rope, char: Char) => Number
```

### RopeString.**reverse**

```grain
reverse: (rope: Rope) => Rope
```

### RopeString.**toString**

```grain
toString: (rope: Rope) => String
```

### RopeString.**print**

```grain
print: (rope: Rope) => Void
```

