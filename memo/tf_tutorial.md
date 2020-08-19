# Tensor Flow Tutorial Memo
## 予定
- [基本的な画像分類](https://www.tensorflow.org/tutorials/keras/classification?hl=ja)
- [csv](https://www.tensorflow.org/tutorials/load_data/csv?hl=ja)
- [NumPy](https://www.tensorflow.org/tutorials/load_data/numpy?hl=ja)
- [pandas.DataFrame](https://www.tensorflow.org/tutorials/load_data/pandas_dataframe?hl=ja)
- [畳み込みニューラルネットワーク](https://www.tensorflow.org/tutorials/images/cnn?hl=ja)
- [画像分類](https://www.tensorflow.org/tutorials/images/classification?hl=ja)

## classfication
- ニューラルネットはなぜ0~1にスケールする必要があるのか
  - 正規化するため。[詳しい解説](https://qiita.com/ryouka0122/items/a7fbad253680bb7f815e)
- tf.keras.layers.Dense 調べるべし
  - 全結合層
- softmaxの活性化関数がなんかよくわからん
  - とりあえず、活性化関数の一種という認識で止める。
- plt.imshow()のplt.cm.binaryはなに？
  - カラーマップの色のこと、binaryは色
- xtickes, ylimなどなど調べる
  - 軸のラベルのこと
- [plot.grid(False)をplot.grid = False と一度してしまうと、再起動しないと動くようにならない。](https://forum.omz-software.com/topic/906/mathplotlib-grid)

## csv
```
def get_dataset(file_path, **kwargs):
    dataset = tf.data.experimental.make_csv_dataset(
        file_path,
        batch_size=5,
        label_name = LABEL_COLUMN,
        na_value="?",
        num_epochs=1,
        ignore_errors=True,
        **kwargs)
    return dataset
```
ここで返されるdatasetの形がよくわからん。

```
def show_batch(dataset):
    for batch, label in dataset.take(1):
        for key, value in batch.items():
            print("{:20s}: {}".format(key,value.numpy()))
```
上のdatasetに関係して、どんな形で渡されているのかわからんので、挙動がよくわからん。  
どこで label使ってる？？

```
# survivedがどっか行ってる、なんで？？
SELECT_COLUMNS = ['survived', 'age', 'n_siblings_spouses', 'parch', 'fare']
DEFAULTS = [0, 0.0, 0.0, 0.0, 0.0]
temp_dataset = get_dataset(train_file_path, 
                           select_columns=SELECT_COLUMNS,
                           column_defaults = DEFAULTS)
show_batch(temp_dataset)
```
連動して、これもいまいちわからん。

## images
pathlibはreplaceが効かない
```
image_rel = pathlib.Path(image_path).relative_to(data_root).replace('\', '/')

SyntaxError: EOL while scanning string literal
```

```
 def caption_image(image_path):
----> 4     image_rel = pathlib.Path(image_path).relative_to(data_root).replace('\\', '/')
      5     print(image_rel)
      6     print(attributions[str(image_rel)])

TypeError: replace() takes 2 positional arguments but 3 were given
```

```
a =pathlib.Path(image_path).relative_to(data_root).replace('\\', '/')

TypeError: replace() takes 2 positional arguments but 3 were given
```
## CNN
 - modelの層はなんであの順番で決められているのか？
   -  ゼロから学ぶディープラーニング読め（第７章）

## image classification
```
fig, axes = plt.subplots(1, 5, figsize=(20,20))
```
これ↑なんで二つに分けられる？？
```
>>> plt.subplots(1, 5, figsize=(20,20))
(<Figure size 2000x2000 with 5 Axes>, array([<matplotlib.axes._subplots.AxesSubplot object at 0x00000201F4EB8FA0>,
       <matplotlib.axes._subplots.AxesSubplot object at 0x00000201F70263A0>,
       <matplotlib.axes._subplots.AxesSubplot object at 0x00000201F70567C0>,
       <matplotlib.axes._subplots.AxesSubplot object at 0x00000201F7082BE0>,
       <matplotlib.axes._subplots.AxesSubplot object at 0x00000201F70B1160>],
      dtype=object))
>>> fig, axes = plt.subplots(1, 5, figsize=(20,20))
>>> axes
array([<matplotlib.axes._subplots.AxesSubplot object at 0x00000201F70F86A0>,
       <matplotlib.axes._subplots.AxesSubplot object at 0x00000201F7120A30>,
       <matplotlib.axes._subplots.AxesSubplot object at 0x00000201F56EEE50>,
       <matplotlib.axes._subplots.AxesSubplot object at 0x00000201F57272B0>,
       <matplotlib.axes._subplots.AxesSubplot object at 0x00000201F57546D0>],
      dtype=object)
>>> fig
<Figure size 2000x2000 with 5 Axes>
```
ということらしい。

- 水平方向の回転が、垂直方向の回転に見える。なぜ？？

## image_seggmentation
```
from tensorflow_examples.models.pix2pix import pix2pix

No module named 'tensorflow_examples'
```
`!pip install git+https://github.com/tensorflow/examples.git`
`!pip install -U tfds-nightly`
で解決。[issue](https://github.com/tensorflow/tensorflow/issues/42451)


