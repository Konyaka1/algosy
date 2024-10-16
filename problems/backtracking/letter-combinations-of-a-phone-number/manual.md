### Recursive solution
```java
class Solution {

    final char[][] letters;

    public Solution() {
        letters = new char[8][];
        letters[0] = new char[]{'a', 'b', 'c'};
        letters[1] = new char[]{'d', 'e', 'f'};
        letters[2] = new char[]{'g', 'h', 'i'};
        letters[3] = new char[]{'j', 'k', 'l'};
        letters[4] = new char[]{'m', 'n', 'o'};
        letters[5] = new char[]{'p', 'q', 'r', 's'};
        letters[6] = new char[]{'t', 'u', 'v'};
        letters[7] = new char[]{'w', 'x', 'y', 'z'};
    }

    public List<String> letterCombinations(String digits) {
        int length = digits.length();
        if (length == 0) {
            return Collections.emptyList();
        }
        List<String> res = new ArrayList<>(length * length * length);

        char[] buffer = new char[length];
        iterate(0, buffer, digits, res);

        return res;
    }

    public void iterate(int state, char[] buffer, String digits, List<String> res) {
        if (state == digits.length()) {
            res.add(new String(buffer));
            return;
        }

        char digit = digits.charAt(state);

        for (char curLetter : letters[digit - '2']) {
            buffer[state] = curLetter;
            iterate(state + 1, buffer, digits, res);
        }
    }
}
```
### Time
O(4^n) -- потому что нужно сгенерировать все возможные варианты
### Memory
O(4^n) -- столько памяти для хранения результатов
### Explication
Рекурсивно опускаемся в глубину с текущим перебором. Как только длина равна длине ответа -- добавляем
в результат и выходим из рекурсии.
### Iterative expanding
```java
class Solution {
    
    final char[][] letters;

    public Solution() {
        letters = new char[8][];
        letters[0] = new char[]{'a', 'b', 'c'};
        letters[1] = new char[]{'d', 'e', 'f'};
        letters[2] = new char[]{'g', 'h', 'i'};
        letters[3] = new char[]{'j', 'k', 'l'};
        letters[4] = new char[]{'m', 'n', 'o'};
        letters[5] = new char[]{'p', 'q', 'r', 's'};
        letters[6] = new char[]{'t', 'u', 'v'};
        letters[7] = new char[]{'w', 'x', 'y', 'z'};
    }
    
    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0) return Collections.emptyList();

        List<char[]> prev = new ArrayList<>();

        char[] vars = letters[digits.charAt(0) - '2'];
        for (char var : vars) {
            char[] buffer = new char[digits.length()];
            buffer[0] = var;
            prev.add(buffer);
        }

        for (int i = 1; i < digits.length(); i++) {
            char[] alphabet = letters[digits.charAt(i) - '2'];
            List<char[]> cur = new ArrayList<>();
            for (char var : alphabet) {
                for (char[] tmp : prev) {
                    char[] copy = Arrays.copyOf(tmp, digits.length());
                    copy[i] = var;
                    cur.add(copy);
                }
            }
            prev = new ArrayList<>(cur);
        }

        return prev.stream().map(String::new).toList();
    }
}
```
### Time
O(4^n) -- потому что нужно сгенерировать все возможные варианты
### Memory
O(4^n) -- столько памяти для хранения результатов
### Explication
Перебираем все варианты в цикле. Сначала собираем все варианты в массив,
Затем для каждой новой буквы добавляем ее к каждому элементу в массиве.
### Система счислений #1
```java
class Solution {
    
    final char[][] letters;
    
    public Solution() {
        letters = new char[8][];
        letters[0] = new char[]{'a', 'b', 'c'};
        letters[1] = new char[]{'d', 'e', 'f'};
        letters[2] = new char[]{'g', 'h', 'i'};
        letters[3] = new char[]{'j', 'k', 'l'};
        letters[4] = new char[]{'m', 'n', 'o'};
        letters[5] = new char[]{'p', 'q', 'r', 's'};
        letters[6] = new char[]{'t', 'u', 'v'};
        letters[7] = new char[]{'w', 'x', 'y', 'z'};
    }
    
    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0) {
            return Collections.emptyList();
        }
        
        int[] radix = new int[digits.length()];
        radix[digits.length() - 1] = 1;
        for (int i = digits.length() - 2; i >= 0; i--) {
            int length = this.getAlpabet(i + 1, digits).length;
            
            radix[i] = radix[i + 1] * length;
        }
        
        int resLength = radix[0] * this.getAlpabet(0, digits).length;
        
        List<String> res = new ArrayList<>(resLength);
        for (int i = 0; i < resLength; i++) {
            String str = this.getStrFromNumber(i, radix, digits);
            res.add(str);
        }
        
        return res;
    }
    
    private String getStrFromNumber(int number, int[] radix, String digits) {
        int base = number;
        char[] buffer = new char[digits.length()];
        for (int i = 0; i < digits.length(); i++) {
            int index = base / radix[i];
            buffer[i] = this.getAlpabet(i, digits)[index];
            base = base % radix[i];
        }
        
        return new String(buffer);
    }
    
    private char[] getAlpabet(int i, String digits) {
        char number = digits.charAt(i);
        return letters[number - '2'];
    }
}
```
### Time
O(4^n) -- потому что нужно сгенерировать все возможные варианты
### Memory
O(4^n) -- столько памяти для хранения результатов
### Explication
Мы знаем сколько элементов мы получим. Начинаем итерировать от 0 до размера ответа - 1 и
переводим текущее число в строку, используя систему счисления.
### Система счислений #2
```java
class Solution {

    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0) {
            return Collections.emptyList();
        }

        Number number = new Number(digits);

        int max = number.getMax();

        List<String> res = new ArrayList<>(max);

        for (int i = 0; i < max; i++) {
            number.inc();
            res.add(number.getState());
        }

        return res;
    }

    class Number {

        final char[][] letters;
        final int[] limits;
        final int[] number;
        final String digits;
        final int maxNumber;

        public Number(String digits) {
            this.digits = digits;
            this.number = new int[digits.length()];
            this.number[digits.length() - 1] = -1;

            letters = new char[8][];
            letters[0] = new char[]{'a', 'b', 'c'};
            letters[1] = new char[]{'d', 'e', 'f'};
            letters[2] = new char[]{'g', 'h', 'i'};
            letters[3] = new char[]{'j', 'k', 'l'};
            letters[4] = new char[]{'m', 'n', 'o'};
            letters[5] = new char[]{'p', 'q', 'r', 's'};
            letters[6] = new char[]{'t', 'u', 'v'};
            letters[7] = new char[]{'w', 'x', 'y', 'z'};

            this.limits = new int[digits.length()];
            int max = 1;
            for (int i = 0; i < digits.length(); i++) {
                char lt = digits.charAt(i);
                int curLength = letters[lt - '2'].length;
                max = max * curLength;
                this.limits[i] = curLength;
            }
            this.maxNumber = max;
        }

        public String getState() {
            char[] buffer = new char[digits.length()];
            for (int i = 0; i < digits.length(); i++) {
                char lt = digits.charAt(i);
                char[] variation = letters[lt - '2'];

                buffer[i] = variation[number[i]];
            }
            return new String(buffer);
        }

        public void inc() {
            number[number.length - 1]++;
            checkLimit(number.length - 1);
        }

        public int getMax() {
            return this.maxNumber;
        }

        private void checkLimit(int digit) {
            if (number[digit] == limits[digit]) {
                number[digit] = 0;
                number[digit - 1]++;
                checkLimit(digit - 1);
            }
        }

    }
}
```
Same as previous, but saving curBuffer, instead of creating it from zero.
```java
class Solution {

    final char[][] letters;

    public Solution() {
        letters = new char[8][];
        letters[0] = new char[]{'a', 'b', 'c'};
        letters[1] = new char[]{'d', 'e', 'f'};
        letters[2] = new char[]{'g', 'h', 'i'};
        letters[3] = new char[]{'j', 'k', 'l'};
        letters[4] = new char[]{'m', 'n', 'o'};
        letters[5] = new char[]{'p', 'q', 'r', 's'};
        letters[6] = new char[]{'t', 'u', 'v'};
        letters[7] = new char[]{'w', 'x', 'y', 'z'};
    }

    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0) {
            return Collections.emptyList();
        }

        Number number = new Number(digits, letters);

        int max = number.getMax();

        List<String> res = new ArrayList<>(max);

        for (int i = 0; i < max; i++) {
            number.inc();
            res.add(number.getState());
        }

        return res;
    }

    class Number {

        final char[][] alphabet;
        final int[] limits;
        final int[] number;

        final int maxNumber;
        final char[] curBuffer;

        public Number(String digits, char[][] letters) {
            this.number = new int[digits.length()];
            this.number[digits.length() - 1] = -1;
            this.curBuffer = new char[digits.length()];
            this.alphabet = new char[digits.length()][];
            this.limits = new int[digits.length()];

            int max = 1;
            for (int i = 0; i < digits.length(); i++) {
                char lt = digits.charAt(i);
                char[] vars = letters[lt - '2'];
                this.alphabet[i] = vars;
                this.curBuffer[i] = vars[0];

                this.limits[i] = vars.length;
                max = max * vars.length;
            }
            this.maxNumber = max;
        }

        public String getState() {
            return new String(curBuffer);
        }

        public void inc() {
            number[number.length - 1]++;
            checkLimit(number.length - 1);
        }

        public int getMax() {
            return this.maxNumber;
        }

        private void checkLimit(int digit) {
            int curVal = number[digit];
            if (curVal == limits[digit]) {
                curBuffer[digit] = alphabet[digit][0];
                number[digit] = 0;
                number[digit - 1]++;
                checkLimit(digit - 1);
            } else {
                curBuffer[digit] = alphabet[digit][curVal];
            }
        }

    }
}
```
### Time
O(4^n) -- потому что нужно сгенерировать все возможные варианты
### Memory
O(4^n) -- столько памяти для хранения результатов
### Explication
Создаем класс, который хранит текущее число. По этому числу создаем строку.
