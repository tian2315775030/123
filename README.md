# 123
十大算法
冒泡排序
#include "sort_.h"
#include <stdio.h>
 
// 打印数组的函数（已在题目中给出）
void print_array(int *arr, int n) {
    if (n == 0) {
        printf("ERROR: Array length is ZERO\n");
        return;
    }
    for (int i = 0; i < n; i++) {
        printf("%d", arr[i]);
        if (i < n - 1) {
            printf(" ");
        }
    }
    printf("\n");
}
 
// 冒泡排序算法并输出前三次冒泡操作后的序列以及最终的升序序列
void sort_array(int *arr, int n) {
    for (int i = 0; i < n - 1; i++) { // 外层循环，控制冒泡的轮数
        int swapped = 0; // 标志位，用于检测是否发生了交换
 
        for (int j = 0; j < n - 1 - i; j++) { // 内层循环，进行实际的比较和交换操作
            if (arr[j] > arr[j + 1]) {
                // 交换arr[j]和arr[j + 1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
 
                // 设置标志位，表示发生了交换
                swapped = 1;
            }
        }
 
        // 输出当前冒泡操作后的数组状态（前三次）
        if (i < 3) {
            printf("");
            print_array(arr, n);
        }
    }
 
    // 输出最终的升序数组
    printf("");
    print_array(arr, n);
}
 
