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
 
选择排序
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
 
// 选择排序算法并输出前三次选择操作后的序列以及最终的升序序列
void sort_array(int *arr, int n) {
    for (int i = 0; i < n - 1; i++) { // 外层循环，控制选择的轮数
        int min_idx = i; // 假设当前元素为最小值
 
        // 在剩余未排序部分找到最小值的索引
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
 
        // 交换找到的最小值和当前元素
        if (min_idx != i) {
            int temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
        }
 
        // 输出当前选择操作后的数组状态（前三次）
        if (i < 3) {
            printf("");
            print_array(arr, n);
        }
    }
 
    // 输出最终的升序数组
    printf("");
    print_array(arr, n);
}
插入排序
#include <stdio.h>
 
void print_array(int *arr, int n) {
    for (int i = 0; i < n; i++) {
        printf("%d", arr[i]);
        if (i < n - 1) {
            printf(" ");
        }
    }
    printf("\n");
}
 
void sort_array(int *arr, int n) {
    int print_count = 0; // 打印计数器
 
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
 
        // 将大于key的元素向后移动
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key; // 插入key
 
        // 如果打印次数少于3次，则打印当前数组
        if (print_count < 3) {
            print_array(arr, n);
            print_count++;
        }
    }
 
  
    print_array(arr, n);
}
 希尔排序
 #include "sort_.h"

void print_array(int *arr, int n) {
    if (n == 0) {
        printf("ERROR: Array length is ZERO\n");
        return;
    }
    printf("%d", arr[0]);
    for (int i = 1; i < n; i++) {
        printf(" %d", arr[i]);
    }
    printf("\n");
}

void sort_array(int *arr, int n) {
    int gaps[] = {5, 2, 1}; // 前三次的增量序列
    int gap_count = 3;

    for (int k = 0; k < gap_count; k++) {
        int d = gaps[k];
        if (d > n) continue; // 如果增量大于数组长度，跳过

        for (int i = d; i < n; i++) {
            int temp = arr[i];
            int j = i;
            while (j >= d && arr[j - d] > temp) {
                arr[j] = arr[j - d];
                j -= d;
            }
            arr[j] = temp;
        }
        print_array(arr, n);
    }
    // 输出最终的升序序列
    print_array(arr, n);
}
归并排序
#include "sort_.h"
#include <stdlib.h>

void print_array(int *arr, int n) {
    if (n == 0) {
        printf("ERROR: Array length is ZERO\n");
        return;
    }
    printf("%d", arr[0]);
    for (int i = 1; i < n; i++) {
        printf(" %d", arr[i]);
    }
    printf("\n");
}

int* merge_array(int *arr1, int n1, int *arr2, int n2) {
    int *result = (int *)malloc((n1 + n2) * sizeof(int)); // 分配合并后的数组空间
    int i = 0, j = 0, k = 0;

    // 双指针法合并两个有序数组
    while (i < n1 && j < n2) {
        if (arr1[i] < arr2[j]) {
            result[k++] = arr1[i++];
        } else {
            result[k++] = arr2[j++];
        }
    }

    // 将剩余部分复制到结果数组
    while (i < n1) {
        result[k++] = arr1[i++];
    }
    while (j < n2) {
        result[k++] = arr2[j++];
    }

    return result;
}

int* merge_sort(int *arr, int n) {
    if (n <= 1) {
        int *result = (int *)malloc(n * sizeof(int));
        if (n > 0) result[0] = arr[0]; // 处理 n=1 的情况
        return result;
    }

    int mid = n / 2; // 找到中间位置
    int *left = merge_sort(arr, mid); // 递归排序左半部分
    int *right = merge_sort(arr + mid, n - mid); // 递归排序右半部分

    int *result = merge_array(left, mid, right, n - mid); // 合并两部分

    free(left); // 释放左半部分内存
    free(right); // 释放右半部分内存

    return result;
}

