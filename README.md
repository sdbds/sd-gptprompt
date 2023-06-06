# sd-gptprompt

下面是命令定义和执行例子。 在语言模型上以模拟方式运行命令定义。 如果理解了，只需回答："明白"。 除了输出外，请用中文回答。

# 命令的定义

以下是三个命令的定义。

##命令 `#2pr`

1. 输入`t2i_prompt`。
2. 如果`t2i_prompt`是中文，将其转换为英文。 (:数字)被保留，因为它代表()所包围的部分的强调值。
3. 根据 "场景"、"环境"等内容，将`t2i_prompt`划分为每个大类的对象，为每个关系设置一个键，将`t2i_prompt`转换为JSON作为值并输出。
4. 基于转换后的JSON，将 "转换后的提示 "作为英文自然语言输出。 如果该值包含一个强调值，该部分将以"(value:强调值) "的格式输出。 强调值的范围是0.5到1.7。
5. 在对象变化的时间点上插入 "BREAK"，并穿插一个新行。 此时不需要对象名称。

##命令`#2db`

1. 输入`t2i_prompt`。
如果`t2i_prompt`是中文，将被转换为英语。 (:数字)被保留，因为它代表()所包围的部分的强调值。
3. 根据 "场景"、"环境 "等内容，将`t2i_prompt`划分为每个大类的对象，为每个关系设置一个键，将`t2i_prompt`转换为JSON作为值并输出。
4. 基于转换后的JSON，输出带有danbooru标签的 "转换后的提示"。 如果该值包含一个强调值，该部分将以"（值：强调值）"的格式输出。 强调值的范围应该在0.5到1.7之间。 将每个元素输出为一个短句或一个单词列表，按元素分组，用逗号隔开。
5. 在对象发生变化的时机插入一个 "BREAK"，中间穿插一个新行。 这时不需要对象名称。

##命令`#rand`

1. 除非输入 "#rand"，否则不会调用这个命令。
2. 任意地只改变预处理的JSON的键而不改变对象，并输出一个 "转换后的提示"。 但是，整体氛围被保留，人物的性别保持不变。
3. 在这种情况下，对每个对象随机强调一个键。 强调值应该在0.5到1.7之间。 强调风格以"（值：强调值）"的形式输出。

##命令`#2cn`

1. 除非输入了`#2cn`，否则不会调用。
2. 输出中文的预处理 "转换后提示"的摘要。


# 执行实例

以下是执行各自命令的例子。

##2pr`命令的执行例子。
输入:
```
#2pr 这是一个故事发生在某个傍晚。一个下人在羅生門下等待雨停。在宽阔的门下，除了这个男人，没有其他人。只有一个丹漆剥落的大圆柱上，停着一只蟋蟀。
```
JSON:
```
{
  "scene": {
	"time": "One day at dusk",
        "location": "under the Rashomon Gate",
        "charactor": "a single kirigirisu",
        "specialCharacter": {
            "type": "human",
            "status": "a servant:1.3"
	},
    }
    "action1": {
        "action charactor": "A servan",
        "action": "waiting for the rain to stop"
    }
    "action2": {
        "action charactor": "a single kirigirisu",
        "action": "perched on a large column"
    }
    "environment": {
	"around1": "There was no one under the wide gate"
	"around2": "large columnthe tan lacquer peeling off"
    }
}
```
输出:
```
One day at dusk, under the Rashomon Gate, a single kirigirisu was present along with (a servant :1.3),
BREAK
The servant was waiting for the rain to stop. 
BREAK
Also, the kirigirisu was perched on a large column.
BREAK
Regarding the environment, there was no one under the wide gate, and the tan lacquer was peeling off the large column.
```

## 命令 `#2db`的执行实例

输入:
```
One day at dusk, under the Rashomon Gate, a single kirigirisu, (a servant :1.3)
BREAK
A servant, waiting for the rain to stop
BREAK
a single kirigirisu, perched on a large column
BREAK
There was no one under the wide gate, large column with the tan lacquer peeling off
```

## 命令 `#rand`的执行实例

输入:
```
#rand
```
JSON:
```
{
    "scene": {
        "time": "A summer afternoon",
        "location": "beneath an ancient monument",
        "character": "a solitary butterfly",
        "specialCharacter": {
            "type": "human",
            "occupation": "a bard:1.2"
        }
    },
    "action1": {
        "actionCharacter": "The bard",
        "action": "composing a ballad"
    },
    "action2": {
        "actionCharacter": "a solitary butterfly",
        "action": "fluttering around the monument:1.5"
    },
    "environment": {
        "surroundings1": "The monument stood alone in the area",
        "surroundings2": "ancient monument, showing signs of weathering"
    }
}
```
输出:
```
On a summer afternoon, beneath an ancient monument, a solitary butterfly was present along with (a bard :1.2), 
BREAK
The bard was composing a ballad.
BREAK
Also, the butterfly was (fluttering around the monument :1.5).
BREAK
Regarding the environment, the monument stood alone in the area, and the ancient monument was showing signs of weathering.
```
