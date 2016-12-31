#### 关键字
```
delete(map1, key1)  //删除

mapCreated = make(map[string]float64) //创建

 sort.Strings(keys) //排序
```


#### 创建map

```
package main

import "fmt"

func main() {
	var mapList map[string]int      //☝定义
	var mapAssigned map[string]int
	var mapCreated map[string]float64
	
	mapList = map[string]int{"one":1 , "two":2}
	mapCreated = make(map[string]float64) //创建
	mapAssigned = mapList
	
	mapCreated["key1"] = 4.5
	mapCreated["key2"] = 3.1415926
	mapAssigned["two"] = 3
	
	fmt.Printf("Map literal at 'one' is : %d \n " , mapList["one"])
	fmt.Printf("Map created at 'key2' is : %f \n " , mapCreated["key2"])
	fmt.Printf("Map assigned at 'two' is : %d \n " , mapAssigned["two"])
	fmt.Printf("Map literal at 'ten' is : %d \n " , mapList["ten"])
}


```

#### 排序

```

package main

import (
	"fmt"
	"sort"
	"strings"
)

var (
	barVal = map[string]int{"alpha": 34, "bravo": 56, "charlie": 23,
		"delta": 87, "echo": 56, "foxtrot": 12,
		"golf": 34, "hotel": 16, "indio": 87,
		"juliet": 65, "kili": 43, "lima": 98}
)

func main() {
	fmt.Println("unsorted:")
	for key,val := range barVal {
		fmt.Printf("key: %v, value : %v \n",key ,val)
	}
	keys := make([]string , len(barVal))
	i := 0
	for k , _ := range barVal {
		keys[i] = k
		i++
	}

	sort.Strings(keys)
	fmt.Println(strings.Repeat("--*--",10))
	fmt.Println("sorted:")

	for _ , k := range keys {
		fmt.Printf("key: %v,value:%v \n",k,barVal[k])
	}
}


```