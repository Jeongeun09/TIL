코테 후기(소수 판별)
====
GPT에게 코테 문제를 짜주라고 하여 인텔리제이에서 직접 코드를 짜보고 실행해보았다.

### 문제
// 6. 소수 판별하기
//사용자로부터 정수 N을 입력받아 소수(prime number) 인지 판별하는 프로그램을 작성하세요.

소수를 판별하는 코드를 main 함수에도 써도 되지만 메서드를 사용하여 호출해서 하는 게 main 함수가 활동하는 양을 줄일 것 같아 메서드를 짜는 형식으로 하게 되었다.

#### 소수란?
: 1과 자신 이외의 나누어 떨어질 수 없는 수를 말한다.

---

- 처리 메서드
``` 
public class Check {
        public static boolean Prime_num(int number) {
            if (number < 2) {
                return false;
            }
            for (int i = 2; i < Math.sqrt(number); i++) {
                if (number % i == 0) {
                    return false;
                }
            }
            return true;
        }
    }
```
소수를 판별하기 위한 메서드이다. boolean을 사용하여 진실인 지 거짓인 지 구별할 수 있게 했다.
2 미만 숫자, 나누어 떨어지는 숫자는 소수가 아니기 때문에 false를 반환했다. 
그리고 두 가지 경우도 아닐 경우에는 소수이기 때문에 true를 반환했다.


----

- main 함수

```
 public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("정수를 입력해주세요 : ");
        int N = scanner.nextInt();

        if (Check.Prime_num(N)) {
            System.out.println(N + "는 소수입니다.");
        } else {
            System.out.println(N + "는 소수가 아닙니다.");
        }
    }
```
메서드를 사용함으로써
main 함수에서는 코드가 줄어들고 호출만 하여 판별한 후 결과를 출력하는 로직만 들어있게 되었다.
