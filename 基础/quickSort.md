快排基础，一次划分（partion）有3种办法，除了本文这种，还有2参考：

 https://blog.csdn.net/mengmengdastyle/article/details/81701111

```java
// 第一种
public static void quickSort(int[] nums) {
	int n = nums.length;
	sort(nums, 0, n -1);
}

public void sort(int nums, int left, int right) {
	int div = partion(nums, left, right);
	sort(nums, left, div -1);
	sort(nums, div + 1, right);
}

public void partion(int nums , int left, int right) {
	if(left > right) {
		return;
	}
	int base = nums[left];
	int i = left;
	int j = right;

	while(i < j) {
	
		while(n[j] >= base && i < j) {
			j--;
		}
		swap(nums, i, j);
		while(n[i] <= base && i < j) {
			i++;
		}
		swap(nums, i, j);
	}
	return i;
}

private swap(int nums[]; int i; int j) {
	int tmp = nums[i];
	nums[i] = nums[j];
	nums[j] = tmp;
}


// 重要的是一次划分，这种2个swap的比较好理解，发现右边小的，就和左边交换。发现左边大的，就和右边交换。最终i = j , nums[i] = base
```



```java
// 第二种
public int partion(int nums , int left, int right) {
	if(left > right) {
		return;
	}
  int key = nums[left];
  int i = left;
  int j = right;
  while(i < j) {
    while(i<j && num[j] >= key) {
      j--;
    }
    nums[i] = nums[j]; // 这里nums[j] 肯定比key小，所以放到左边。 
    while(i<j && nums[i] <= key) {
      i++;
    }
    nums[j] = nums[i]; // 这里 nums[i] 肯定比key大，nums[j] 肯定是比key小， 且已经换到左边
  }
  nums[i] = key; // 最终i=j,左边的数小于key，右边大于key，key回位
  return low;
}
// 这种直接交换法，其实是方法一的简单做法，其实方法一就是把key换来换去，覆盖不要的位置，这里不管不要的数，直接替换，保留着key最后用
```



第三种是找到 符合要求 的 i j 再交换，
