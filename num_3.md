### 面试题3：二维数组中的查找

<!---->

> 题目：在一个二维数组中，每一行都按照从左到右递增的顺序排列，每一列都按照从上到下递增的顺序排列。请完成这样一个函数，输入这样一个二维数组和整数，判断数组中是否含有该整数。

分析：假设给定的数字为num，与数组第一个数字a[0][0]比较，若num较大，则num有可能出现在数组当前位置的右侧或者下侧。这样查找的区域就会有所重叠，并且数组的前进有两个方向。此时，如果将一个方向固定：将最开始比较的数字定在数组的右上角或左下角，此时数组的前进方向就会只剩下一个。比如选左下角，如果num较大，则num只会出现在数组的右侧，当前列不需要再考虑了；如果num较小，则num只会出现在数组的上侧，当前行中不可能存在num。这样，每一次比较都可以缩小一行或者一列。代码如下：

<pre>
bool find(int *array, int rows, int columns, int num) {
    int row = rows - 1, column = 0;
    int tmp;
    
    if (array == NULL || rows <= 0 || columns <= 0) {
        return false;
    }
    
    while (row >= 0 && column < columns) {
        tmp = *array + columns * row + column;
        if (num == tmp) {
            return true;
        } else if (num > tmp) {
            column++;
        } else {
            row--;
        }
    }
    
    return false;
}
</pre>

