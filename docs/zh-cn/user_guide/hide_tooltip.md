# 分部分控制枪械的文本提示

鉴于目前枪械文本提示内容庞杂，我们学习 Mojang，引入了 NBT 控制的文本提示隐藏方法。服务器腐竹可以通过此方法自定义枪械的文本提示隐藏部分！

## 控制值（掩码）

要定制枪械的文本提示，首先需要计算出控制值。  
我们将枪械的文本提示拆分成了如下的 6 个部分，其中每个部分可以单独隐藏和显示：  

![](/user_guide/tooltip_part.png)  

其中，每个框起来的部分都是一个可以单独隐藏的部分，它右侧的数字是这个部分的数值，将所有需要 **隐藏** 的部分的数值加和，就得到了我们需要的控制值
如我们想隐藏第一、二、三栏，那么这三栏数值加和是 `1+2+4=7`，则我们需要的控制值就是7，效果如下  

![img](/user_guide/hided.png)

:::tip
事实上，控制值是一个**二进制掩码**，每一位代表一个部分，1 代表隐藏，0 代表显示，从低位到高位分别代表第一到第六个部分  
:::

## 通过附加NBT标签控制文本提示
控制值以NBT标签的形式保存在枪械上，所以你可以直接通过为物品附加NBT标签 `HideFlags`（整型）来为枪械启用它。
以下是一个示例的 `give` 指令，用于获取一把上例中隐藏了第一、二、三栏的 M4A1：

```
/give @s tacz:modern_kinetic_gun{GunId:"tacz:m4a1",GunFireMode:"SEMI",HideFlags:7}
```

## 使用指令修改物品的文本提示

TACZ 内置了一个指令，可用于快速为一把枪械附加文本提示隐藏标签，语法如下：

```
/tacz hide_tooltip_part <players> <mask>
```

其中，`<players>` 为目标玩家选择器，`<mask>` 为指定的控制值。这个指令将会为目标玩家手持的枪械附加指定的文本提示隐藏标签。