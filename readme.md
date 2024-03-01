# Kiwi 数据科学家校招岗位第二轮笔试题——模拟掉落

## 考察目的
本地用于考察候选人在偏真实的场景下的工程实现能力，与leetcode算法题不太一样。候选人需要根据需求实现一段 C/C++ 代码，并设计一些测试用例通过 python 进行测试。  
题目可以用一周左右的时间（非硬性要求）在家完成，完成后将结果通过邮件发送给我（huzhongmin@chaofanhy.cn），并抄送hr。提交形式可以是github地址，或直接打包。提交后安排终面。

## 背景描述
我们用一个二维矩阵来表示游戏盘面的信息，二维矩阵中，0表示空位，1表示不可移动的障碍物，其他正整数表示可以移动的物体。   
因为这是一个竖直摆放的盘面，盘面上的物体会因为重力向下掉落，直到被障碍物、底部或其他物品挡住。此外，物体还可以向斜下方侧滑。  
请实现一个simulate_drop函数，用于模拟这个掉落的过程，并返回盘面稳定后的结果。

## 掉落规则
1. 盘面的遍历顺序为从左下往右上。
2. 当物体下方格子为空位时，物体向下掉落一格。
3. 如果物体下方不是空位，则判断左下方是否是空位，如果是，则侧滑至左下方一格的位置。
4. 如果物体下方、左下方均不是空位，则判断右下方是否是空位，如果是，则侧滑至右下方一格的位置。
5. 重复上面的过程，直到物体无法下落或侧滑为止。
6. 对所有物体执行上述下落操作，直到盘面稳定。

## 相关信息和要求
1. simulate_drop.c 中实现主体部分。
2. 需要编译成可以被其他语言（例如C#、python）调用的动态库。这里是python。
3. test_dll.ipynb notebook中对你设计的多个测试用例展示效果。
4. 虽然我们用二维矩阵来表示游戏盘面的信息，但为了外部语言调用动态库传参方便，一般会扁平化为一维数组。一维数组的坐标规则为：index = col*height + row. row=0表示最下方, index=0的坐标在盘面左下角。
5. utils.py 中是一些工具类或函数，例如将一维数组展示成盘面信息的函数等。
6. 测试用例需要涵盖不同的情形，以充分测试代码在不同情况下的表现。
7. 从性能角度，建议模拟掉落的操作通过指针做内存映射完成，即让外部调用动态库的语言和C代码操作同一块内存。python的ctypes调用c代码时提供了这种机制。
8. 如果可能，代码的时间和空间复杂度可以做一些优化。性能也是考察的一个方面。
9. 项目中提供了一个简单的示例countOnes，计算盘面中的障碍数量。simulate_drop函数的输入同countOnes函数示例。notebook中提供了python通过ctypes调用countOnes的示例。