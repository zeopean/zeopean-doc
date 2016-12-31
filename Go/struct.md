

#### 定义struct
```
package main

import "fmt"

type struct1 struct {
	i1 int
	f1 float64
	str string
}

func main() {

	ms := new(struct1)
	ms.i1 = 10
	ms.f1 = 1.2
	ms.str = "zeopean"

	fmt.Println(ms)
	fmt.Println(ms.i1)
	fmt.Println(ms.f1)
	fmt.Println(ms.str)
}


```

#### struct 与 面向对象
```
package main

import (
	"strings"
	"fmt"
)

type Person struct {
	firstName string
	lastName  string
}

func upPerson(p *Person){
	p.firstName = strings.ToUpper(p.firstName)
	p.lastName  = strings.ToUpper(p.lastName)
}

func main() {
	//实例化对象1
	var person Person
	person.firstName = "zeopean"
	person.lastName  = "Dave"
	upPerson(&person)           //传入对象地址
	fmt.Printf("The name of the person is  %s %s \n",person.firstName,person.lastName)

	//实例化对象2
	person2 := new(Person)
	person2.firstName = "laosd"
	person2.lastName  = "dave"
	(*person2).lastName = "Damw"
	upPerson(person2)
	fmt.Printf("The name of the person is  %s %s \n",person2.firstName,person2.lastName)


	//实例化对象3
	person3 := &Person{"daming","DAew"}
	upPerson(person3)
	fmt.Printf("The name of the person is  %s %s \n",person3.firstName,person3.lastName)

}



```


#### 带便签的结构体

```

package main

import (
	"reflect"
	"fmt"
)

type TagType struct{
	field1 bool "tag1"  //"tag1" 为便签
	field2 string "tag2"
	field3 int "tag3"
}
func main() {
	tt := TagType{true,"daming",234}
	for i := 0 ; i < 3; i++ {
		refTag(tt,i)
	}
}

func refTag(tt TagType , ix int){
	ttType := reflect.TypeOf(tt)
	ixField := ttType.Field(ix)
	fmt.Printf("%v \n" , ixField .Tag)
}



```

#### struct 匿名字段

```

package main

import "fmt"

type innerS struct {
	int1 int
	int2 int
}

type outerS struct {
	b int
	c int
	int         //匿名字段
	innerS
}
func main() {
	outer := new(outerS)
	outer.b = 1
	outer.c = 3
	outer.int1 = 23
	outer.int2 = 34
	outer.int = 2		//该字段为匿名字段

	fmt.Println(outer)

	fmt.Printf("outer.b is: %d\n", outer.b)
	fmt.Printf("outer.c is: %d\n", outer.c)
	fmt.Printf("outer.int is: %d\n", outer.int)
	fmt.Printf("outer.in1 is: %d\n", outer.int1)
	fmt.Printf("outer.in2 is: %d\n", outer.int2)

}



```


#### 继承

```
package main

import "fmt"
type Camera struct {

}

func (c *Camera) TakeAPicture() string{
	return "Click"
}

type Phone struct {

}
func (p *Phone) Call() string{
	return "Ring Ring"
}

type CameraPhone struct {
	Camera
	Phone
}
func main() {
	cp := new(CameraPhone)
	fmt.Println("Our new CameraPhone exhibits multiple behaviors...")
	fmt.Println("It exhibits behavior of a Camera: ", cp.TakeAPicture())
	fmt.Println("It works like a Phone too: ", cp.Call())
}



```

#### 继承 self 的使用

```
package main

import "fmt"

type Base struct{}

func (Base) Magic(){
	fmt.Println("base magic")
}

func (self Base) MoreMagic(){
	self.Magic()
	self.Magic()
}

type Voodoo struct {
	Base
}

func (Voodoo) Magic(){
	fmt.Println("voodoo magic")
}


func main() {
	v := new(Voodoo)
	v.Magic()
	v.MoreMagic()
}

#输出
voodoo magic
base magic
base magic      //self 表示Base

```








