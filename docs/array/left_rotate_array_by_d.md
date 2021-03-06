# Left Rotate Array by d

**Input:** </br>
arr[] = {11, 22, 33, 44, 55} </br>
d = 2 </br>
**Output:** </br> 
arr[] = {33, 44, 55, 11, 22}

**Input:** </br>
arr[] = {11, 15, 33, 19} </br>
d = 3 </br>
**Output:** </br>
arr[] = {19, 11, 15, 33}


- We may assume that d <= No of elements in array
- If d > no of elements in array then we can simply d = d-n 
## Naive Approach

```
package main

import (
	"fmt"
)

func main() {
	// arr := []int{11, 22, 33, 44, 55} // [33 44 55 11 22]
	// leftRotate(arr, 2)
	// fmt.Println(arr)

	arr := []int{11, 15, 33, 19} // [19 11 15 33]
	leftRotate(arr, 3)
	fmt.Println(arr)

}
func leftRotate(arr []int, d int) {
	for i := 0; i < d; i++ {
		leftRotateOne(arr)
	}
}

func leftRotateOne(arr []int) {
	temp := arr[0]
	for i := 1; i < len(arr); i++ {
		arr[i-1] = arr[i]
	}
	arr[len(arr)-1] = temp
}
```

**Time Complexity:** &theta;(n * d) <br>
**Aux Space:** &theta;(1)

## Better Approach

```
package main

import (
	"fmt"
)

func main() {
	arr := []int{11, 22, 33, 44, 55} // [33 44 55 11 22]
	leftRotate(arr, 2)
	fmt.Println(arr)

	// arr := []int{11, 15, 33, 19} // [19 11 15 33]
	// leftRotate(arr, 3)
	// fmt.Println(arr)

}

func leftRotate(arr []int, d int) {
	var temp []int
	for i := 0; i < d; i++ {
		temp = append(temp, arr[i])
	}
	for i := d; i < len(arr); i++ {
		arr[i-d] = arr[i]
	}
	for i := range temp {
		arr[len(arr)-d+i] = temp[i]
	}
}
```

**Time Complexity:** &theta;(d+ (n-d) + d)
= &theta;(n+d)
= &theta;(n) </br>
d is smaller than n so ignore d

**Aux Space:** &theta;(d)


## Best Approach

```
package main

import (
	"fmt"
)

func main() {
	// arr := []int{11, 22, 33, 44, 55} // [33 44 55 11 22]
	// leftRotate(arr, 2)
	// fmt.Println(arr)

	arr := []int{11, 15, 33, 19} // [19 11 15 33]
	leftRotate(arr, 3)
	fmt.Println(arr)

}
func reverve(arr []int, low, high int) {
	for low < high {
		temp := arr[low]
		arr[low] = arr[high]
		arr[high] = temp
		low++
		high--
	}
}

func leftRotate(arr []int, d int) {
	reverve(arr, 0, d-1)
	reverve(arr, d, len(arr)-1)
	reverve(arr, 0, len(arr)-1)
}
```

**Time Complexity:** &theta;(d + (n-d) + n)
= &theta;(2n)
= &theta;(n)

**Aux Space:** &theta;(1)
