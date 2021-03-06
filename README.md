# amplify_abc190C

## 実行方法

1. プログラムと同じ階層にAmplifyのアクセストークンを記載した`tokenfile.txt`を作成する。

（もしくは直接`client.token`にアクセストークンを入力する）

2. テストケースをダウンロードする。
https://www.dropbox.com/sh/nx3tnilzqz7df8a/AAByf3VY9tx1sJULb5peSBQka/ABC190?dl=0&subfolder_nav_tracking=1

3. テストケースを置いたフォルダを指定する
```shell
folder = "ABC190/C/"
files = os.listdir(folder + "in")
``` 
        
4. プログラムをを実行する

AC

```shell
01_sample.txt Amplify結果 = 2 正解 = 2
02_sample.txt Amplify結果 = 4 正解 = 4
03_sample.txt Amplify結果 = 9 正解 = 9
04_small.txt Amplify結果 = 9 正解 = 9
05_small.txt Amplify結果 = 1 正解 = 1
06_small.txt Amplify結果 = 19 正解 = 19
07_small.txt Amplify結果 = 7 正解 = 7
08_small.txt Amplify結果 = 17 正解 = 17
09_small.txt Amplify結果 = 0 正解 = 0
10_small.txt Amplify結果 = 15 正解 = 15
11_small.txt Amplify結果 = 17 正解 = 17
12_small.txt Amplify結果 = 1 正解 = 1
13_large.txt Amplify結果 = 1 正解 = 1
14_large.txt Amplify結果 = 30 正解 = 30
15_large.txt Amplify結果 = 13 正解 = 13
16_large.txt Amplify結果 = 5 正解 = 5
17_large.txt Amplify結果 = 82 正解 = 82
18_large.txt Amplify結果 = 21 正解 = 21
19_large.txt Amplify結果 = 6 正解 = 6
20_large.txt Amplify結果 = 1 正解 = 1
21_large.txt Amplify結果 = 8 正解 = 8
22_max.txt Amplify結果 = 4 正解 = 4
23_max.txt Amplify結果 = 6 正解 = 6
24_max.txt Amplify結果 = 46 正解 = 46
25_max.txt Amplify結果 = 29 正解 = 29
26_max.txt Amplify結果 = 20 正解 = 20
27_max.txt Amplify結果 = 74 正解 = 74
28_max.txt Amplify結果 = 100 正解 = 100
29_max.txt Amplify結果 = 0 正解 = 0
30_max.txt Amplify結果 = 15 正解 = 15
31_max.txt Amplify結果 = 5 正解 = 5
32_max.txt Amplify結果 = 78 正解 = 78
33_max.txt Amplify結果 = 0 正解 = 0
34_max.txt Amplify結果 = 18 正解 = 18
35_star.txt Amplify結果 = 56 正解 = 56
36_star.txt Amplify結果 = 41 正解 = 41
37_star.txt Amplify結果 = 37 正解 = 37
38_star.txt Amplify結果 = 15 正解 = 15
```

## 考え方

プログラムのf, g, hがQUBOの各項になっています。

f：満たされる条件の個数です。多い方が良いのでマイナスをつけています。

g：K人の人がC[i]とD[i]のどちらか一方にボールを置くという制約です。q2[i][0]とq2[i][1]のどちらかのみを1としたいです。

　 equal_to関数を使おうとしたのですが、テストケース3でエラーが発生してしまったため、愚直にペナルティ項を書き下しました。
  
h：fで用いたqubit(q)とgで用いたqubit(q2)を関連付けるものです。

　　gで用いた皿kに対応するqubitのどれか1つ以上が1になってるときはfで用いたqubitが1になってほしいです。
  
  　スマートな方法が分からなかったので、(-q[皿i] + Σq2[皿i])^2としました。Σq2[皿i]が0の時はq[皿i]が0の時に最小値(=0)を取り、そうでないときはq[皿i]が1の時に最小値(0とは限らない）を取ります。
   
欲しい値は-fですが、h>0になりうるので直接エネルギーの値が答えにはならないことがあります。

そのため、アニーリング計算したのちに出力された組合せを使って評価値を計算しています。


## 疑問点

equal_toがうまく機能しなかった（コメントアウトしています）

## 使用したアニーリングマシン

Fixstars Amplify AE

https://amplify.fixstars.com/


## 使用した問題

https://atcoder.jp/contests/abc190/tasks/abc190_c
