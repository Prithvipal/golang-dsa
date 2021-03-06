# Union if Two Sorted Array

**Input:** a[] = {13, 15, 18} </br>
b[] = {12, 18, 19, 20, 25} </br>
**Output:** c[] = {12, 13, 15, 18, 19, 20, 25}

**Input:** a[] = {12, 13, 13, 13, 14,  14} </br>
b[] = {14, 14} </br>
**Output:** c[] = {12, 13, 14}

## Naive Approach

```golang
package main

import (
	"fmt"
	"sort"
)

func main() {
	a := []int{3, 5, 10, 10, 10, 15, 15, 20}
	b := []int{5, 10, 10, 15, 30}
	res := union(a, b)
	fmt.Println(res) //[3 5 10 15 20 30]
}

func union(a, b []int) (res []int) {
	c := make([]int, len(a)+len(b))
	for i := 0; i < len(a); i++ {
		c[i] = a[i]
	}
	m := len(a)
	for j := 0; j < len(b); j++ {
		c[m+j] = b[j]
	}
	sort.Ints(c)
	for i := 0; i < len(c); i++ {
		if i == 0 || c[i] != c[i-1] {
			res = append(res, c[i])
		}
	}
	return res
}

```

**Time Complexity:** O((m+n)*log(m+n))

**Dry Run:** </br>
a[] = {3, 5, 5} </br>
b[] = {1, 5, 7, 7} </br>

After 1st loop: c[] = {3, 5, 5, _, _, _, _} </br>
After 2nd loop: c[] = {3, 5, 5, 1, 5, 7, 7} </br>
After sorting: c[] = {1, 3, 5, 5, 5, 7, 7} </br>
3rd loop: res[] = {1, 3, 5, 7} </br>

## Efficient Solution

### Implementation Idea

![](resources/union_sorted_array.png)

if i > 0 && a[i] == a[i-1] { i++; continue; } </br>
if j > 0 && b[j] == b[j-1] { j++; continue; } </br>
if a[i] < b[j] { c=append(c,a[i]); i++ } </br>
if a[i] > b[j] { c=append(c,b[j]); j++ } </br>
if a[i] == b[j] { c=append(c,a[i]); i++; j++ } </br>

### Implementation

```
package main

import (
	"fmt"
)

func main() {
	a := []int{3, 5, 10, 10, 10, 15, 15, 20}
	b := []int{5, 10, 10, 15, 30}
	res := union(a, b)
	fmt.Println(res) //[3 5 10 15 20 30]
}

func union(a, b []int) (res []int) {
	m := len(a)
	n := len(b)
	i, j := 0, 0
	for i < m && j < n {
		if i > 0 && a[i] == a[i-1] {
			i++
			continue
		}
		if j > 0 && b[j] == b[j-1] {
			j++
			continue
		}
		if a[i] < b[j] {
			res = append(res, a[i])
			i++
		} else if a[i] > b[j] {
			res = append(res, b[j])
			j++
		} else {
			res = append(res, a[i])
			i++
			j++
		}
	}
	for i < m {
		if i == 0 || a[i] != a[i-1] {
			res = append(res, a[i])
		}
		i++
	}
	for j < n {
		if j == 0 || b[j] != b[j-1] {
			res = append(res, b[j])
		}
		j++
	}
	return
}

```

**Dry Run**

a[] = {12, 20, 30, 30} </br>
b[] = {13, 30, 40} </br>
i=0; j=0; </br>
1st Iteration: c[] = {12}, i=1 </br>
2nd Iteration: c[] = {12, 13}, j=1 </br>
3rd Iteration: c[] = {12, 13, 20}, i=2 </br>
4th Iteration: c[] = {12, 13, 20, 30}, i=3, j=2 </br>
5th Iteration: c[] = {12, 13, 20, 30}, i=4 </br>
Next Loop `for(j < n)`: c[] = {12, 13, 20, 30, 40}, j=3 </br>

