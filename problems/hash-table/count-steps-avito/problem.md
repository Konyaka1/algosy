Мы в Авито любим проводить соревнования. Недавно мы устраивали
чемпионат по шагам и вот настало время подводить итоги!

Необходимо определить userIds участников, которые прошли 
наибольшее количество шагов steps за все дни, не пропустив ни одного дня соревнований
```
Ввод:
statistics = [
    [{ userId: 1, steps: 1000}, { userId: 2, steps: 1500 }],
    [{ userId: 2, steps: 1000}]
]
Вывод:
{ userIds: [2], steps: 2500}
```
```
Ввод:
statistics = [
    [{ userId: 1, steps: 1000}, { userId: 2, steps: 1500 }],
    [{ userId: 2, steps: 1000}, { userId: 1, steps: 1500}]
]
Вывод:
{ userIds: [1,2], steps: 2500}
```
```
Ввод:
statistics = [
    [{ userId: 1, steps: 1000}, { userId: 2, steps: 1500 }],
    [{ userId: 2, steps: 1000}, { userId: 1, steps: 1800}]
]
Вывод:
{ userIds: [1], steps: 2800}
```