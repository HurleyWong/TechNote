## Matplotlib调整子图间距和整体空白

```python
import matplotlib.pyplot as plt

# 调整整体空白
plt.tight_layout()
# 调整子图间距
# 具体间距可以自定义
plt.subplot_adjust(wspace=0, hspace=0)
```

