### Error

In a Lab experiment that trains neural network in the university, after running the given sample code, although training can be started, the training will be finished by prompting `KeyError: 'acc'`.

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-31_17-12-27.png)

### Solution

For safety, We can try to get the key with `trained_model.history.get('acc', None)` where `None` is the default value if the key is missing. 

In addition, we can also try to print all the keys if we want to know the names before trying to get a specific key by `print(trained_model.history.keys())`, assuming `trained_model.history` is an instance of `dict`.

By printing the names of the key, we get the result below:

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-31_17-16-38.png)

The names of the key are not consistent with the names in the code. So, we can change the code to:

```
 accuracy = trained_model.history['accuracy']
 val_accuracy = trained_model.history['val_accuracy']
```

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-31_17-21-55.png)

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-31_17-21-00.png)

Then we can get the final training results below:

### Result