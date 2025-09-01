코테 후기 (단어 개수 세기)
=====

저번과 같게 GPT에게 문제를 내주라고 하였다. 

### 문제
 // 7. 단어 빈도 세기
 
  //문자열을 입력받아 공백 기준으로 단어를 나누고, 각 단어가 몇 번 나왔는지 세어 출력하세요.

  단어의 개수, 빈도 수를 세고 나타내는 방법은 여러가지 있지만 나는 배열을 사용하여 하는 게 좋을 것 같다는 생각을 하게 되어 배열을 사용하였다.

아래에는 실제 내가 모르는 부분은 찾아보며 짜본 코드이다.

  ```
 System.out.print("문자열 입력하세요 : ");
        String ch = scanner.nextLine();

        String[] words = ch.split("\\s+");

        Map<String, Integer> wordCount = new HashMap<>();

        for (String word : words) {
            word = word.toLowerCase(); // 소문자로 구분해야 편하다고 함
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }

        System.out.println("\n단어 빈도:");
        for (Map.Entry<String, Integer> entry : wordCount.entrySet()) {
            System.out.println(entry.getKey() + " : " + entry.getValue() + "번");
        }
```

words 라는 문자열 배열을 사용했고 입력받은 문자열에서 ("\\s+") 라는 것을 나타내며 공백을 기준으로 단어를 나눌 수 있게 하였다.



```
  Map<String, Integer> wordCount = new HashMap<>();
```

이 코드는 단어별 빈도를 저장할 수 있는 HashMap이라는 클래스를 활용했다.
키와 값을 동시에 저장할 수 있기 때문에 단어에 빈도 수를 나타낼 때 많이 사용되어 사용했다.


```
  for (String word : words) {
            word = word.toLowerCase(); // 소문자로 구분해야 편하다고 함
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }
```

이 코드는 words 배열에 있는 모든 문자를 하나씩 꺼내서 반복하는 것이다. 
또한 대문자와 소문자를 그대로 받아들이게 됐을 때 혼란이 생길 수 있다고 하 모두 소문자로 바꾸는 코드를 넣었다.
이전에 단어가 있는 지 확인하여 있는 경우에는 
