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
- softmaxの活性化関数がなんかよくわからん
- plt.imshow()のplt.cm.binaryはなに？
- xtickes, ylimなどなど調べる
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




