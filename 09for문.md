# for문

## for문 동작 원리

‣ 기본 형태
``` go
for 초기문; 조건문; 후처리 {
    코드 블록
}
```

‣ for문 동작 예제
``` go
package main

import "fmt"

func main() {
    for i := 0; i < 10; i++ {
        fmt.Print(i, ", ")
    }
}
```
```
0, 1, 2, 3, 4, 5, 6, 7, 8, 9,
```

### 초기문 쌩략
``` go
for ; 조건문; 후처리 {
    코드 블록
}
```

### 후처리 생략
``` go
for 초기문; 조건문; {
    코드 블록
}
```

### 조건문만 있는 경우
``` go
for ; 조건문; {
    코드 블록
}
```

### 무한 루프
``` go
for true {
    코드 블록
}
```
``` go
for {
    코드 블록
}
```

‣ 1초마다 한 번씩 1씩 증가하는 숫자를 무한히 출력하는 예제
``` go
package main

import (
	"fmt"
	"time"
)

func main() {
	i := 1
	for {
		time.Sleep(time.Second)
		fmt.Println(i)
		i++
	}
}
```
```
1
2
3
...
```

## continue와 break
- continue : 이후 코드 블록을 수행하지 않고 곧바로 후처리를 하고 조건문 검사부터 다시 함
- break : for문에서 바로 빠져나옴

‣ continue와 break를 이용한 예제
``` go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	stdin := bufio.NewReader(os.Stdin)
	for {
		fmt.Println("입력하세요")
		var number int
		_, err := fmt.Scanln(&number)
		if err != nil {
			fmt.Println("숫자를 입력하세요")

			stdin.ReadString('\n')
			continue
		}
		fmt.Printf("입력하신 숫자는 %d입니다\n", number)
		if number%2 == 0 {
			break
		}
	}
	fmt.Println("for문이 종료되었습니다.")
}
```
```
입력하세요.
ff
숫자를 입력하세요.
입력하세요.
31
입력하신 숫자는 31입니다.
입력하세요.
32
입력하신 숫자는 32입니다.
for문이 종료되었습니다.
```

## 중첩 for문
‣ 중첩된 for문 예제
``` go
package main

import "fmt"

func main() {
    for i := 0; i < 3; i++ {
        for j := 0; j < 5; j++ {
            fmt.Print("*")
        }
        fmt.Println()
    }
}
```
```
*****
*****
*****
```

‣ 이중 for문 예제
``` go
package main

import "fmt"

func main() {
    for i := 0; i < 5; i++ {
        for j := 0; j < i+1; j++ {
            fmt.Print("*")
        }
        fmt.Println()
    }
}
```
```
*
**
***
****
*****
```

‣ 중첩 for문에서 break와 continue를 사용하는 예제
``` go
package main

import "fmt"

func main() {
	dan := 2
	b := 1
	for {
		for {
			fmt.Printf("%d * %d = %d\n", dan, b, dan*b)
			b++
			if b == 10 {
				break
			}
		}
		b = 1
		dan++
		if dan == 10 {
			break
		}
	}
	fmt.Println("for문이 종료되었습니다.")
}
```
```
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
... 중략 ...
9 * 7 = 63
9 * 8 = 72
9 * 9 = 81
for문이 종료되었습니다.
```

## 중첩 for문과 break, 레이블
‣ 불리언 변수를 사용하는 예제
``` go
package main

import "fmt"

func main() {
	a := 1
	b := 1

	found := false
	for ; a <= 9; a++ {
		for b = 1; b <= 9; b++ {
			if a*b == 45 {
				found = true
				break
			}
		}
		if found {
			break
		}
	}
	fmt.Printf("%d * %d = %d\n", a, b, a*b)
}
```
```
5 * 9 = 45
```

‣ 레이블을 이용한 예제
``` go
package main

import "fmt"

func main() {
	a := 1
	b := 1

OuterFor:
	for ; a <= 9; a++ {
		for b = 1; b <= 9; b++ {
			if a*b == 45 {
				break OuterFor
			}
		}
	}
	fmt.Printf("%d * %d = %d\n", a, b, a*b)
}
```
```
5 * 9 = 45
```

‣ 함수를 사용하여 반복문 중첩과 레이블이 없는 예제
``` go
package main

import "fmt"

func find45(a int) (int, bool) {
	for b := 1; b <= 9; b++ {
		if a*b == 45 {
			return b, true
		}
	}
	return 0, false
}

func main() {
	a := 1
	b := 0

	for ; a <= 9; a++ {
		var found bool
		if b, found = find45(a); found {
			break
		}
	}
	fmt.Printf("%d * %d = %d\n", a, b, a*b)
}
```
```
5 * 9 = 45
```