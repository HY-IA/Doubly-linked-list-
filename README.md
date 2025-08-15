# Doubly Linked List Module (Circular with Sentinel)

This C module implements a **circular doubly linked list** with a **sentinel node** and a **current item pointer**.  
The design allows for constant-time operations for navigation, insertion, deletion, and access.

---

## Features

- **Circular doubly linked list** with a sentinel `"none"` node.
- **Current item pointer** that can be moved forward or backward.
- **Default item** returned when no item is selected.
- Supports:
  - Navigation (`first`, `last`, `after`, `before`)
  - Access (`get`, `set`)
  - Modification (`insertAfter`, `insertBefore`)
  - Deletion (`deleteToAfter`, `deleteToBefore`)
- **All operations run in O(1) time**.
- Custom `item` type (currently `int`).

---

## Data Structure Design

Each list contains:

- **Sentinel Node (`none`)**:
  - Always present.
  - Holds the default item.
  - Points to the first and last elements in the list.
- **Current Node (`current`)**:
  - Points to the currently selected item.
  - If pointing to `none`, no item is selected.

---

## API Reference

| Function | Description |
|----------|-------------|
| `list *newList(item e)` | Create a new empty list with default item `e`. |
| `void freeList(list *xs)` | Free all nodes (including sentinel) and the list structure. |
| `void first(list *xs)` | Set current to first item (if any). |
| `void last(list *xs)` | Set current to last item (if any). |
| `bool none(list *xs)` | Check if no item is selected. |
| `bool after(list *xs)` | Move current forward one position. |
| `bool before(list *xs)` | Move current backward one position. |
| `item get(list *xs)` | Return current item or default item if none selected. |
| `bool set(list *xs, item x)` | Set current item value. |
| `void insertAfter(list *xs, item x)` | Insert after current (or at start if none). |
| `void insertBefore(list *xs, item x)` | Insert before current (or at end if none). |
| `bool deleteToAfter(list *xs)` | Delete current and select its successor. |
| `bool deleteToBefore(list *xs)` | Delete current and select its predecessor. |

---

## Example Usage

```c
#include "list.h"
#include <stdio.h>

int main() {
    list *xs = newList(-1); // default item = -1
    insertAfter(xs, 10);
    insertAfter(xs, 20);
    first(xs);
    printf("First: %d\n", get(xs)); // 10
    after(xs);
    printf("Next: %d\n", get(xs)); // 20
    freeList(xs);
    return 0;
}
```

---

## Testing

A built-in test harness is included using `#ifdef test_list`.  
To compile and run tests:

```bash
clang -std=c11 -Wall -pedantic -g list.c -Dtest_list -o test \
    -fsanitize=undefined -fsanitize=address
./test
```

Expected output:
```
List module tests run OK.
```

---

## Notes

- **Thread Safety:** Not thread safe.
- **Item Type:** Change the `typedef int item;` in `list.h` to store a different type.
- **Memory Management:** All nodes are heap-allocated; `freeList()` must be called to avoid leaks.

---
