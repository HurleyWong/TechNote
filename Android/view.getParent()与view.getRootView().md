## view.getParent()与view.getRootView()

getParent()是获取view的父结点，getRootView()是获取当前view层次中处于最顶层的view，可以理解为找出该view实例所在的view层次的根view。

### view处于Activity

如果view文件是一个activity中引用的一个view，则

- 当view处于xml文件的根节点时，通过getParent得到的view是它本身
- 当view处于xml文件的非根节点时，通过getParent得到的是view的父节点
- 无论view处于xml文件的根节点还是非根结点，通过getRootView得到的都是当前Activity的DecorView

### view处于Fragment

如果view文件是一个fragment中引用的一个view，则

- 当view处于xml文件的根节点时，通过getParent得到的是null
- 当view处于xml文件的非根节点时，通过getParent得到的是view的父节点
- 无论view处于xml文件的根节点还是非根结点，通过getRootView得到的都是它本身