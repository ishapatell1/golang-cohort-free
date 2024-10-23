## We started from the next slide:  https://go.dev/tour/basics/15

# Topics Covered : 
1. [Constants](https://go.dev/tour/basics/15)
- Constants are declared using `const` keyword, which can be character, string, boolean or numeric values.
- Constants cannot be declared using the := syntax. 
- Constants can be declared with or without a type in Go.

``` 
package main

import "fmt"

func main() {
	const message = "You are Learning Go!"
	const time = 07
	const Truth = true
	fmt.Println("Hello,This is Team Shiksha and", message,"which starts at",time ,"?", Truth )
}
```
- You can also avoid using multiple const keyword and wrap it around brackets. 
```
package main

import "fmt"

func main() {
	const (message = "You are Learning Go!"
		   time = 07
		   Truth = true)
	fmt.Println("Hello,This is Team Shiksha and", message,"which starts at",time ,"?", Truth )
}
```
- Try Changing the value of `07` to `0700` or `070` and observe the difference in outputs. Can you explain why?

2. [Numeric Constants](https://go.dev/tour/basics/16)
- Numeric constants are high-precision values. They can be categorized into two types - untyped and typed. 
```
const untypedInteger = 134
const untypedPi = 3.141592

const typedInteger int = 134
const typedPi float64 = 3.141592
```
- An untyped constant takes the type needed by its context, So When an untyped constant is assigned to a variable, the variable inherits the default type of the constant.

3. [For](https://go.dev/tour/flowcontrol/1)
- Go has only one looping construct, the `for` loop.
- for loop has three components, each separated by a semicolon `;` - init,condition,post.
```
message := " We are learning for loop"
for i := 0; i < 3; i++ {fmt.Println(i,message)}
```
- The init and post statements are optional. But parentheses are always required. Check out this [For continued](https://go.dev/tour/flowcontrol/1)
```
package main

import "fmt"

func main() {
	 i := 1
	
	for ; i < 3; {
		message := " We are learning for loop"
		fmt.Println(i, message) 
		i+=i
	}
}
```
4. [For is Go's "while"](https://go.dev/tour/flowcontrol/3)
- As init and post statements are optional, for loop can also work as while loop.

5. [Forever](https://go.dev/tour/flowcontrol/4)
- In this, we create an infinite loop. 

6. [If](https://go.dev/tour/flowcontrol/5)
- the expression need not be surrounded by parentheses ( ) but the braces { } are required.
```
package main

import (
	"fmt"
	"math"
)
//To Find Squareroot
func sqrt(x float64) string {
	if x < 0 { //if x is less than 0
		return "\nless than 0"
	}
	return fmt.Sprint("Square root of " , x ," is ", math.Sqrt(x))
}

func main() {
	fmt.Println(sqrt(9), sqrt(-4))
}
```

7. [If with a short statement](https://go.dev/tour/flowcontrol/6)
- We can also write and declare variables before condition.
- Variables declared by the statement are only in scope until the end of the if.

8. [If and else](https://go.dev/tour/flowcontrol/7)
- Variables declared inside an if short statement are also available inside any of the else blocks.

9. [Exercise: Loops and Functions](https://go.dev/tour/flowcontrol/8)
- We implemented a square root function to find the number z for which z² is most nearly x.

10. [Switch](https://go.dev/tour/flowcontrol/9)
- Go only runs the selected case, not all the cases that follow. Break is implemented automatically.
-  It runs the first case whose value is equal to the condition expression.

11. [Switch evaluation order](https://go.dev/tour/flowcontrol/10)
- Switch cases evaluate cases from top to bottom, stopping when a case succeeds.


## References 
- We Paused on https://go.dev/tour/flowcontrol/10

## Optional - Setup Go in your local machine