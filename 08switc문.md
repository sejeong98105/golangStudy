# Switch

## Switch문 동작 원리
``` go
switch 비굣값 {
    case 값1:
      문장
    case 값2:
      문장
    default:        // default는 생략 가능
      문장
}
```

‣ switch문 동작 원리 예제
```go
package main

import "fmt"

func main() {
    a := 3

    switch a {
    case 1:
      fmt.Println("a == 1")
    case 2:
      fmt.Println("a == 2")
    case 3:
      fmt.Println("a == 3")
    case 4:
      fmt.Println("a == 4")
    default:
      fmt.Println("a > 4")
    }
}
```
```
a == 3
```

## switch문을 언제 쓰는가?
- 복잡한 if else 문을 보기 좋게 정리 할 수 있음

‣ if else문을 이용한 예제
``` go
package main

import "fmt"

func main() {
    day := 3

    if day == 1 {
        fmt.Println("첫째 날입니다.")
        fmt.Println("오늘은 팀미팅이 있습니다.")
 	} else if day == 2 {
		fmt.Println("둘째 날입니다")
		fmt.Println("새로운 팀원 면접이 있습니다.")
	} else if day == 3 {
		fmt.Println("셋째 날입니다.")
		fmt.Println("설계안을 확정하는 날입니다.")
	} else if day == 4 {
		fmt.Println("넷째 날입니다.")
		fmt.Println("예산을 확정하는 날입니다.")
	} else if day == 5 {
		fmt.Println("다섯째 날입니다.")
		fmt.Println("최종 계약하는 날입니다.")
	} else {
		fmt.Println("프로젝트를 진행하세요")
	}  
}
```
```
셋째 날입니다.
설계안을 확정하는 날입니다.
```

‣ switch문을 이용한 예제
``` go
package main

import "fmt"

func main() {

	day := 3

	switch day {
	case 1:
		fmt.Println("첫째 날입니다")
		fmt.Println("오늘은 팀미팅이 있습니다.")
	case 2:
		fmt.Println("둘째 날입니다")
		fmt.Println("오늘은 면접이 있습니다.")
	case 3:
		fmt.Println("셋째 날입니다.")
		fmt.Println("설계안을 확정하는 날입니다.")
	case 4:
		fmt.Println("넷째 날입니다.")
		fmt.Println("예산을 확정하는 날입니다.")
	case 5:
		fmt.Println("다섯째 날입니다.")
		fmt.Println("최종 계약하는 날입니다.")
	default:
		fmt.Println("프로젝트를 진행하세요")
	}
}
```
```
셋째 날입니다.
설계안을 확정하는 날입니다.
```

## 다양한 switch문 형태

### 한 번에 여러 값 비교

‣ 한 번에 여러 값 비교하는 예제
``` go
package main

import "fmt"

func main() {
    day := "thursday"

    switch day {
    case "monday", "tuesday":
      fmt.Println("월, 화요일은 수업 가는 날입니다.")
    case "wednesday", "thursday", "friday":
      fmt.Println("수, 목, 금요일은 실습 가는 날입니다.")
    }
}
```
```
수, 목, 금요일은 실습 가는 날입니다.
```

### 조건문 비교
‣ 온도에 따라 다른 메시지를 출력하는 예제
``` go
package main

import "fmt"

func main() {
	temp := 18

	switch true {
	case temp < 10 || temp > 30:
		fmt.Println("바깥 활동하기 좋은 날씨가 아닙니다.")
	case temp >= 10 && temp < 20:
		fmt.Println("약간 추울 수 있으니 가벼운 겉옷을 준비하세요")
	case temp >= 15 && temp < 25:
		fmt.Println("야외활동 하기 좋은 날씨입니다")
	default:
		fmt.Println("따뜻합니다.")
	}    
}
```
```
약간 추을 수 있으니 가벼운 겉옷을 준비하세요.
```
→ case의 조건문이 true가 되는 경우 실행

### switch 초기문
‣ 형식
``` go
switch 초기문; 비굣값 {
case 값1:
  ...
case 값2:
  ...
default:
}
```

‣ switch 초기문 예제
``` go
package main

import "fmt"

func getMyAge() int {
    return 22
}

func main() {
    switch age := getMyAge(); true {
    case age < 10:
      fmt.Println("Child")
    case age < 20:
      fmt.Println("Teenager")
    case age < 30:
      fmt.Println("20s")
    default:
      fmt.Println("My age is", age)
    }
}
```
```
20s
```

## const 열거값과 switch
``` go
package main

import "fmt"

type ColorType int // 별칭 ColorType을 선언하고 Const 열거값 정의
const (
	Red ColorType = iota
	Blue
	Green
	Yellow
)

// 각 ColorType 열거값에 따른 문자열을 반환하는 함수
func colorToString(color ColorType) string {
	switch color {
	case Red:
		return "Red"
	case Blue:
		return "Blue"
	case Green:
		return "Green"
	case Yellow:
		return "Yellow"
	default:
		return "Undefined"
	}
}

func getMyFavoriteColor() ColorType {
	return Blue
}

func main() {
	fmt.Println("My favorite color is", colorToString(getMyFavoriteColor()))
}
```
```
My favorite color is Blue
```

## break와 fallthrough 키워드
‣ break 사용하는 case 예제
``` go
package main

import "fmt"

func main() {

	a := 3

	switch a {
	case 1:
		fmt.Println("a == 1")
		break
	case 2:
		fmt.Println("a == 2")
		break
	case 3:
		fmt.Println("a == 3")
	case 4:
		fmt.Println("a == 4")
	default:
		fmt.Println("a > 4")
	}
}
```
```
a == 3
```

‣ fallthrough 키워드 동작 확인
``` go
package main

import "fmt"

func main() {

	a := 3

	switch a {
	case 1:
		fmt.Println("a == 1")
		break
	case 2:
		fmt.Println("a == 2")
	case 3:
		fmt.Println("a == 3")
		fallthrough
	case 4:
		fmt.Println("a == 4")
	case 5:
		fmt.Println("a == 5")
	default:
		fmt.Println("a > 4")
	}
}
```
```
a == 3
a == 4
```