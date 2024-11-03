```markdown
# 题目来源
* 《C程序设计语言》第二版，新版，练习 1-13（1）

## 题目描述
* 编写一个程序，打印输入中水平方向的单词长度的直方图

## 代码实现

```c
#include <stdio.h>

#define MAX_LENGTH 10 // 假设单词的最大长度为10

int main() {
    int c, length = 0;
    int word_lengths[MAX_LENGTH + 1] = {0}; // 记录每个长度的单词数量

    while ((c = getchar()) != EOF) {
        if (c == ' ' || c == '\n' || c == '\t') { // 遇到空格、换行或制表符，表示一个单词结束
            if (length > 0 && length <= MAX_LENGTH) {
                word_lengths[length]++; // 记录该长度的单词数量
            }
            length = 0; // 重置单词长度计数
        } else {
            length++; // 增加当前单词的长度计数
        }
    }
    
    // 输出水平方向的直方图
    printf("Word Length Histogram:\n");
    for (int i = 1; i <= MAX_LENGTH; i++) {
        printf("%2d: ", i); // 输出单词长度
        for (int j = 0; j < word_lengths[i]; j++) {
            printf("*"); // 根据单词数量打印 *
        }
        printf("\n"); // 换行显示下一个长度
    }

    return 0;
}
```

### 对于代码的思考

**将程序分为两个部分：输入部分和输出部分**。输入部分将单词长度记录到 `word_lengths[]` 数组中，输出部分通过读取该数组的数据并生成直方图。

#### 输入部分

* **单词判断**：通过检测空格、换行符和制表符来判断单词的结束。
* **计数实现**：在遇到空白字符时，通过 `if` 语句判断并记录单词长度。`word_lengths[]` 数组中的每个元素记录特定长度的单词数量。
* **特殊点**：`word_lengths[]` 数组用于存储不同单词长度的出现次数，数组大小为 `MAX_LENGTH + 1`。如果 `MAX_LENGTH` 设置得很大（如 100），直方图将展示 1 到 100 的单词长度分布。在声明时，`{0}` 初始化 `word_lengths[]` 数组，以确保每个长度的计数从 0 开始。[关于数组初始化的详细讨论在这里](./知识类&非习题内容/对于数组初始化的不同方案.md)
* **长度记录**：`if (length > 0 && length <= MAX_LENGTH) { word_lengths[length]++; length = 0; }` 语句确保每次输入一个完整单词后，`length` 的值存入对应长度的计数位置，并重置 `length` 以准备记录下一个单词。

#### 输出部分

* **直方图生成**：外层 `for` 循环遍历从 1 到 `MAX_LENGTH` 的长度值。`printf("%2d: ", i);` 输出当前长度，内层 `for` 循环根据 `word_lengths[i]` 的值打印 `*` 。
* **使用 `MAX_LENGTH`**：整个代码通过 `MAX_LENGTH` 设置数组范围和直方图显示范围，输出部分基于 `MAX_LENGTH` 控制输出的行数。