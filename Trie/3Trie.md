---
title: Trie
---

## Types

Type declarations included in the Trie module.

### Trie.**Trie**

```grain
type Trie<a>
```

## Values

Functions and constants included in the Trie module.

### Trie.**make**

```grain
make: () => Trie<a>
```

### Trie.**insert**

```grain
insert: (key: String, value: a, self: Trie<a>) => Bool
```

### Trie.**remove**

```grain
remove: (key: String, self: Trie<a>) => Bool
```

### Trie.**printKeyValues**

```grain
printKeyValues: (self: Trie<a>) => Void
```

### Trie.**print**

```grain
print: (self: Trie<a>) => Void
```

### Trie.**contains**

```grain
contains: (key: String, self: Trie<a>) => Bool
```

### Trie.**getValue**

```grain
getValue: (key: String, self: Trie<a>) => Option<a>
```

