## RuntimeError: Expected 4-dimensional input for 4-dimensional weight [6, 3, 5, 5\], but got 3-dimensional input of size [3, 256, 256] instead

Try to unsqueeze your data using:

```python
inputs = inputs.unsqueeze(0)
```

