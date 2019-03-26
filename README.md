归并排序

步骤：
1.要求一数组在L到R上有序
eg.2,5,7,1,5,7,4,9
   L             R
2.额外辅助数组，规模和L到R相同
3.整个数组先砍一半
2,5,7,1|5,7,4,9
4.利用递归过程让左边一半和右边一半分别有序
1,2,5,7|4,5,7,9
5.设置两个指针，比较大小
1,2,5,7|4,5,7,9

6.小的数放进辅助数组，并将指针后移；大的数不动；两者一样大，默认左边的数进辅助数组
1,2,5,7|4,5,7,9

辅助数组：1

1,2,5,7|4,5,7,9

辅助数组：1,2

1,2,5,7|4,5,7,9

辅助数组：1,2,4

1,2,5,7|4,5,7,9

辅助数组：1,2,4,5

1,2,5,7|4,5,7,9

辅助数组：1,2,4,5,5

1,2,5,7|4,5,7,9
  越界 
辅助数组：1,2,4,5,5,7

7.直至有一边越界，将没越界的一边剩余的所有数放进辅助数组
1,2,5,7|4,5,7,9
  越界 
辅助数组：1,2,4,5,5,7,7,9

8．用辅助数组覆盖原数组


1）整体就是一个简单递归，左边排好序、右边排好序、让其整体有序
2）让其整体有序的过程里用了排外序方法
3）利用master公式来求解时间复杂度
4）归并排序的实质
时间复杂度O(N*logN)，额外空间复杂度O(N)

public class MergeSort {
      
      public static void mergesort(int[] arr) {
             if (arr == null || arr.length < 2) {
                   return;
             }//无效参数
             mergesort(arr,0,arr.length-1);//调用mergesort方法
      }
      
      public static void mergesort(int[]arr, int L,int R) {
             if (L == R) {
                   return;
             }//只有一个数
             int mid = L + ((R-1)>>1);//防止溢出
             mergesort(arr,L,mid);//左边排好序
             mergesort(arr,mid+1,R);//右边排好序
             merge(arr,L,mid,R);
      }
      
      public static void merge(int[] arr,int L,int M,int R) {
             int[] help = new int[L-R+1];
             int i = 0;
             int p1 = L;
             int p2 = M +1;
             while(p1<=M && p2<=R) {
                   help[i++] = (arr[p1] < arr[p2] ? arr[p1++] : arr[p2++]);
             }
             //虽然两个while顺序排列，但是只会执行其中的一个
             while(p1 <= M) {
                   help[i++] = arr[p1++];
             }
             while(p2<=R) {
                   help[i++] = arr[p2++];
             }
             for (i = 0; i < help.length; i++) {//将arr覆盖
                   arr[L + i] = help[i];
             }
      }
}


