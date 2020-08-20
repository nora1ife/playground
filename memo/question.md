# わからん
- 活性化関数にrelu関数を使う意味  
画像はマイナスのデータをとらない(0~255)(なんか初日のゼミではとっていたような気がする)、またrelu関数はマイナスはすべて0にして、プラスはそのままにする。この場合、こrelu関数を使わなくても、値が変わらないのであれば、使う意味はどこにあるのか？
  - これ読め→[勾配消失問題とは？](http://marupeke296.com/IKDADV_DL_No6_vanishing_grad_prob.html)  
  要するに傾きを消さないように変更している。勾配降下法と誤差逆伝播法を使う際に微分するが、傾きを0にしてしまうと、使えなくなってしまうため。