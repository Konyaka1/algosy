### Solution
```java
 class Trip {
    String from;
    String to;

    public Trip(String from, String to) {
        this.from = from;
        this.to = to;
    }
}

class Solution {

    public Trip[] getSortedTrips(Trip[] trips, String start) {
        Map<String, String> fromTo = new HashMap<>();

        for (Trip trip : trips) {
            fromTo.put(trip.from, trip.to);
        }

        Trip[] result = new Trip[trips.length];

        String curStart = start;
        for (int i = 0; i < trips.length; i++) {
            String dest = fromTo.get(curStart);
            result[i] = new Trip(curStart, dest);
            curStart = dest;
        }

        return result;
    }
}
```

### Time
O(N) -- потому что проходим через все входные данные 
### Memory
O(N) -- потому что создаем мапу для хранеиния входных, плюс размер ответа
### Explication
Создаем мапу с ключ отправление, значение прибытие.
Создаем массив для ответа равный длине входных данных.
Создаем ссылку `curStart` чтобы хранить текущую стартовую точку, и обновляем ее в цикле.
В цикле находим точку прибытия для `curStart` и создаем эту пару и добавляем в ответ.