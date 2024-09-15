### Solution
```java
class UserData {
    String userId;
    int steps;
}

class Result {
    List<String> userIds = new LinkedList<>();
    int steps;
}

class StepsAndDays {
    int steps;
    int day;
}

class Solution {

    public Result findWinners(UserData[][] statistic) {
        Result result = new Result();

        Map<String, StepsAndDays> map = new HashMap<>();

        for (UserData stat : statistic[0]) {
            StepsAndDays entry = new StepsAndDays();
            entry.steps = stat.steps;
            entry.day = 1;
            map.put(stat.userId, entry);
        }

        for (int i = 1; i < statistic.length; i++) {
            for (UserData stat : statistic[i]) {
                StepsAndDays old = map.get(stat.userId);

                if (old == null) {
                    continue;
                }

                if (old.day != i) {
                    map.remove(stat.userId);
                    continue;
                }

                old.steps = stat.steps + old.steps;
                old.day++;
            }
        }

        int max = -1;
        for (StepsAndDays value : map.values()) {
            if (value.day == statistic.length && value.steps > max) {
                max = value.steps;
            }
        }

        result.steps = max;
        for (Map.Entry<String, StepsAndDays> entry : map.entrySet()) {
            if (entry.getValue().steps == max) {
                result.userIds.add(entry.getKey());
            }
        }
        return result;
    }
}
```

### Time
O(N * M) -- Проходим по всем входным данным. N -- кол-во дней, M -- кол-во пользователей
### Memory
O(N * M) -- Кол-во уникальных пользователей, в худшем случае может быть m пользователей каждый новый день.
### Explication
1. Собираем всех пользователей в мапу, где ключ это айди, а значение это количество шагов и количество дней.
2. Далее находим максимальное кол-во шагов среди тех, кто имеет кол-во дней равное кол-ву дней во входных данных.
3. Далее собираем в ответ те, у кого шаги равны кол-ву максимальных шагов.