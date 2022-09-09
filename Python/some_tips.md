---
sort: 1
---

# Some Tips for Python

## NumPy Subarrays as No-copy Views vs Copy Views

```python
print(x2)
# Output:
# [[12  5  2  4]
#  [ 7  6  8  8]
#  [ 1  6  7  7]]

x2_sub = x2[:2, :2]
print(x2_sub)
# Output:
# [[12  5]
#  [ 7  6]]
x2_sub[0, 0] = 99
print(x2_sub)
# Output:
# [[99  5]
#  [ 7  6]]

print(x2)
#Output:
# [[99  5  2  4]
#  [ 7  6  8  8]
#  [ 1  6  7  7]]

x2_sub_copy = x2[:2, :2].copy()
print(x2_sub_copy)
# Output:
# [[99  5]
#  [ 7  6]]
# If we now modify this subarray, the original array is not touched:
x2_sub_copy[0, 0] = 42
print(x2_sub_copy)
# Output:
# [[42  5]
#  [ 7  6]]
print(x2)
# Output: 
# [[99  5  2  4]
#  [ 7  6  8  8]
#  [ 1  6  7  7]]
```
> This default behavior is actually quite useful: it means that when we work with large datasets, we can access and process pieces of these datasets without the need to copy the underlying data buffer.
> 
> Jake VanderPlas, *Python Data Science Handbook*