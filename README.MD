这里利用java加载macbert模型，并进行中文拼写纠错。

#### 步骤

1.利用java加载macbert模型，并进行纠错推理。

2.模型从[这里](https://huggingface.co/shibing624/macbert4csc-base-chinese) 下载。

3.模型转换见[这里](https://github.com/jiangnanboy/model2onnx) 。

#### 使用
1.sy/MacBert

```
String text = "今天新情很好。";
Pair<BertTokenizer, Map<String, OnnxTensor>> pair = null;
try {
    pair = parseInputText(text);
} catch (Exception e) {
    e.printStackTrace();
}
var predString = predCSC(pair);
List<Pair<String, String>> resultList = getErrors(predString, text);
for(Pair<String, String> result : resultList) {
    System.out.println(text + " => " + result.getLeft() + " " + result.getRight());
}
```

2.result
```
String text = "今天新情很好。";

tokens -> [[CLS], 今, 天, 新, 情, 很, 好, 。, [SEP]]
今天新情很好。 => 今天心情很好。 新,心,2,3

String text = "你找到你最喜欢的工作，我也很高心。";

tokens -> [[CLS], 你, 找, 到, 你, 最, 喜, 欢, 的, 工, 作, ，, 我, 也, 很, 高, 心, 。, [SEP]]
你找到你最喜欢的工作，我也很高心。 => 你找到你最喜欢的工作，我也很高兴。 心,兴,15,16
```

#### 参考
https://github.com/jiangnanboy/model2onnx

https://huggingface.co/shibing624/macbert4csc-base-chinese

https://github.com/jiangnanboy/onnx-java
