归并排序采用的是分治(divide-and-conquer)法思想。

（1）基本思想：将待排序元素分成大小大致相同的2个子集合，分别对2个子集合进行排序，最终将排好序的子集合合并成为所要求的排好序的集合。

```java
// 分治思想，

public class Main {
 
	public static void main(String[] args) {
		int[] arr = {11,44,23,67,88,65,34,48,9,12};
		int[] tmp = new int[arr.length];    //新建一个临时数组存放
		mergeSort(arr,0,arr.length-1,tmp);
		for(int i=0;i<arr.length;i++){
			System.out.print(arr[i]+" ");
		}
	}
	
	public static void merge(int[] arr,int low,int mid,int high,int[] tmp){
		int i = 0;
		int j = low,k = mid+1;  //左边序列和右边序列起始索引
		while(j <= mid && k <= high){
			if(arr[j] < arr[k]){
				tmp[i++] = arr[j++];
			}else{
				tmp[i++] = arr[k++];
			}
		}
		//若左边序列还有剩余，则将其全部拷贝进tmp[]中
		while(j <= mid){    
			tmp[i++] = arr[j++];
		}
		
		while(k <= high){
			tmp[i++] = arr[k++];
		}
		
		for(int t=0;t<i;t++){
			arr[low+t] = tmp[t];
		}
	}
 
	public static void mergeSort(int[] arr,int low,int high,int[] tmp){
		if(low<high){
			int mid = (low+high)/2;
			mergeSort(arr,low,mid,tmp); //对左边序列进行归并排序
			mergeSort(arr,mid+1,high,tmp);  //对右边序列进行归并排序
			merge(arr,low,mid,high,tmp);    //合并两个有序序列
		}
	}
}
```

