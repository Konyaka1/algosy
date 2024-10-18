### Solution
```java
import java.io.*;
import java.util.*;

class Solution {

    public static void main(String[] args) {
        try (BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
             BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out))) {
            int n = Integer.parseInt(in.readLine());

            SpecialFifo queue = new SpecialFifo();

            while (n > 0) {
                String cmd = in.readLine();

                processCommand(queue, cmd, out);

                n = n - 1;
            }

            out.flush();
        } catch (Exception ignored) {

        }
    }

    private static void processCommand(SpecialFifo queue, String cmd, BufferedWriter out) throws IOException {
        if (cmd.charAt(0) == '-') {
            String res = queue.pop();
            out.write(res);
            out.newLine();
            return;
        }
        String val = cmd.substring(2);
        if (cmd.charAt(0) == '+') {
            queue.pushRegular(val);
        } else {
            queue.pushSpecial(val);
        }
    }

    static class SpecialFifo {

        final Deque<String> first = new ArrayDeque<>();
        final Deque<String> second = new ArrayDeque<>();

        public void pushRegular(String val) {
            second.offerLast(val);

            this.balance();
        }

        public void pushSpecial(String val) {
            second.offerFirst(val);

            this.balance();
        }

        public String pop() {
            String val = first.pollFirst();

            this.balance();

            return val;
        }

        private void balance() {
            if (first.size() < second.size()) {
                String val = second.pollFirst();
                first.offerLast(val);
            }
        }
    }
}
```
### Time
O(1) -- Для всех операций.
### Memory
O(N) -- Для хранения всех элементов
### Explication
По условию задачи, шаманы сразу становятся в середину очереди. При четной длине, они становятся на нечетный индекс,
а при нечетной длине -- становятся на четную позицию сразу за центром.
```text
1 2 3 4 5           1 2 3 4
adding shaman to both cases
1 2 3 NEW 4 5       1 2 NEW 3 4
```
Гоблин всегда добавляется в конец. Уходит из очереди всегда первый

Для решения задачи заводим две деки, которые отвечают за две половины очереди.
* При добавлении гоблина (regular) мы всегда добавляем его в конец второй очереди и делаем балансировку.
* При добавлении шамана (special) мы всегда добавляем его в начало второй очереди и делаем балансировку.
* При удалении существа мы всегда достаем из начала первой очереди и делаем балансировку.
* Балансировка нужна только в том случае, когда вторая очередь по размеру больше чем первая. Для этого
мы достаем элемент из начала второй и добавляем в конец первой.

Таким образом первая дека отвечает за `n / 2 с округлением вврх` и вторая очередь
отвечает за `n / 2 с округлением вниз`. 