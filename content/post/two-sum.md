---
title: "Two Sum"
date: 2019-01-14T15:18:07+09:00
draft: true
---

# 問題概要
* 引数1: 整数列 nums
* 引数2: 整数 target

引数1で与えられる整数列より，異なる2つの値を選んでたした値が，引数2で与えられる整数値に等しい場合，選んだ引数のindexの列を返せ

# 例
```
[2,7,11,15]
9
=> [0, 1]
```

# 最初の回答

```go
func twoSum(nums []int, target int) []int {
    for i, v := range nums {
        for i2, v2 := range nums[i + 1:] {
            if (v + v2) == target {
                return []int{i, i + 1+i2}
            }
        }  
    }
    return nil
}

```

方針は脳死でブルートフォースでできんじゃね？ｗとか言って実装したら，テストケースが通過したが実行時間が長すぎる．  
O(n^2)なので多少はね……

# 模範解答1: Two-pass Hash Table
まずハッシュテーブルに`key=numsの数値, value=数値のindex`となるようにマップを作る．  
これでO(n)．  
次に，`complement = target - nums[i]; (complement == map.has(complement) && map.gets(complement) != i)`としてnumsをなめるようにもう一度ループを回して走査．  
これでO(n)  
  
なるほどね，

# 模範解答2: One-pass Hash Table
ハッシュテーブルをlookupしつつ追加するループが1回のやつ

```go
func twoSum(nums []int, target int) []int {
    m := make(map[int]int)
    for i, v := range nums {
        cmp := target - v
        if val, ok := m[cmp]; ok {
            return []int{val, i}
        }
        m[v] = i
    }
    return nil
}
```

> Your runtime beats 100.00 % of golang submissions.

やったね！
