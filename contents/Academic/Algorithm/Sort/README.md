# ソートアルゴリズム

## 概要

学習用にまとめたコード集です。実際は実行速度の観点から言語標準のソート関数の使用をお勧めします。

## 一覧

### バブルソート

安定なソート
オーダー：O(n^2)

```python
def sort(array: list) -> list:
    size = len(array)
    for i in range(size):
        for j in range(i, size):
            if array[i] > array[j]:
                array[i], array[j] = array[j], array[i]
    return array
```

### マージソート

```python
def sort(array) -> list:
    size = len(array)

    if size <= 1:
        return array
    else:
        # 半分の位置を求める
        mid = int(size / 2)

        # リストを左右に分割する(再帰処理)
        left = sort(array[:mid])
        right = sort(array[mid:])

        # 出力用の配列を作成
        output = []

        # 左右のリストから小さい順に取り出す
        while len(left) != 0 and len(right) != 0:
            if left[0] < right[0]:
                output.append(left.pop(0))
            else:
                output.append(right.pop(0))

        # 残った左右どちらかのリストを出力に結合する
        if len(left) != 0:  # 左が残った
            output += left
        elif len(right) != 0:  # 右が残った
            output += right

        return output
```

### クイックソート

```python
def sort(array) -> list:
    # 最大要素をバケットのサイズとする
    size = max(array) + 1

    # バケットを初期化する
    buckets = list()
    for i in range(size):
        buckets.append(False)

    # 対応するバケットに要素を追加する
    for element in array:
        index = element
        buckets[index] = True

    # 空の要素を取り除く
    output = list()
    for i in range(size):
        if buckets[i] == True:
            output.append(i)

    return output
```

### シェルソート

```python
def sort(array):
    h = len(array) // 2

    while h > 0:
        # h間隔の挿入ソート
        size = len(array)
        for i in range(h, size):
            target = array[i]
            left = i
            while left >= h and target < array[left - h]:
                array[left] = array[left - h]
                left -= h
            array[left] = target
        h //= 2
    return array
```

### バケットソート

```python
def sort(array: list) -> list:
    size = len(array)
    for i in range(size):
        for j in range(i, size):
            if array[i] > array[j]:
                array[i], array[j] = array[j], array[i]
    return array
```

### 選択ソート

```python
def sort(array):
    size = len(array)
    for i in range(size):
        # 最小要素の場所を取得する
        min_id = i
        for j in range(i, size):
            if array[j] < array[min_id]:
                min_id = j
        # 要素を交換する
        array[i], array[min_id] = array[min_id], array[i]
    return array
```

##　ソートの実行時間比較

```
⭐️実行時間計測⭐️
バブルソート　：4303.65ms
選択ソート　　：2616.54ms
マージソート　：  33.44ms
クイックソート：  19.90ms
シェルソート　：  16.06ms
バケットソート：   2.40ms
挿入ソート　　：   1.58ms
```