
#### 初始化

```

package main

import "fmt"

type Shaper interface {
	Area() float64
}

type Square struct {
	side float64
}

func (sq *Square) Area() float64{
	return sq.side * sq.side
}

type Rectangle struct {
	length , width float64
}

func (r Rectangle) Area() float64{
	return r.length * r.width
}


func main() {
	r := Rectangle{5,3}
	q := &Square{5}

	shapes := []Shaper{Shaper(r),Shaper(q)}
	fmt.Println("Loopign through shapes for area ... ")

	for n , _ := range shapes{
		fmt.Println("Shape details: " , shapes[n])
		fmt.Println("Area of this shape is:" , shapes[n].Area())
	}
}



```