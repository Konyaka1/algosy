[Link](https://codeforces.com/problemset/problem/1408/C?locale=ru)
### Solution - iterative
```java
import java.util.Scanner;

public class Solution2 {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            int k = sc.nextInt();
            int length = sc.nextInt();
            int[] flags = new int[k];
            for (int j = 0; j < k; j++) {
                flags[j] = sc.nextInt();
            }
            solve(length, flags);
        }
    }

    private static void solve(int length, int[] flags) {
        int vl = 1;
        int vr = 1;

        double timeL = 0;
        double timeR = 0;


        int left = 0;
        int right = flags.length - 1;

        int prevL = left;
        int prevR = length;
        while (right - left >= 0) {
            double newTimeL = timeL + (double) (flags[left] - prevL) / vl;
            double newTimeR = timeR + (double) (prevR - flags[right]) / vr;
            if (newTimeL < newTimeR) {
                prevL = flags[left];
                timeL = newTimeL;
                left++;
                vl++;
            } else {
                prevR = flags[right];
                timeR = newTimeR;
                right--;
                vr++;
            }
        }

        double distance;
        if (right == -1) {
            distance = flags[0];
        } else if (left == flags.length) {
            distance = length - flags[right];
        } else {
            distance = flags[left] - flags[right];
        }
        if (timeL < timeR) {
            distance = distance - (timeR - timeL) * vl;
        } else {
            distance = distance - (timeL - timeR) * vr;
        }
        int speed = vl + vr;
        double result = distance / speed + Math.max(timeL, timeR);
        System.out.println(result);
    }
}
```
### Time
O(N) -- проходим по всем флагам, ищем слот, в котором они пересекутся
### Memory
O(1) -- не используется доп память
### Solution - true bin search
```java
import java.util.Scanner;

public class Solution {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            int k = sc.nextInt();
            int length = sc.nextInt();
            int[] flags = new int[k];
            for (int j = 0; j < k; j++) {
                flags[j] = sc.nextInt();
            }
            solve(length, flags);
        }
    }

    private static void solve(int length, int[] flags) {
        double l = 0;
        double r = (double) length / 2;

        double accuracy = Math.pow(10, -7);
        while (r - l > accuracy) {
            double m = l + (r - l) / 2;

            double posL = leftPosAtTime(length, flags, m);
            double posR = rightPosAtTime(length, flags, m);

            if (posL <= posR) {
                l = m;
            } else {
                r = m;
            }
        }

        System.out.println(l);
    }

    private static double leftPosAtTime(int length, int[] flags, double t) {
        double curTime = 0;
        int i = 0;
        int prevPoint = 0;
        int vl = 1;
        while (i < flags.length) {
            int dist = flags[i] - prevPoint;
            double time = (double) dist / vl;
            if (curTime + time > t) {
                double delta = t - curTime;
                return prevPoint + delta * vl;
            } else {
                curTime += time;
                prevPoint = flags[i];
                vl++;
                i++;
            }
        }
        int dist = length - prevPoint;
        double time = (double) dist / vl;
        if (curTime + time > t) {
            double delta = t - curTime;
            return prevPoint + delta * vl;
        } else {
            return length + 1;
        }
    }

    private static double rightPosAtTime(int length, int[] flags, double t) {
        double curTime = 0;
        int i = flags.length - 1;
        int prevPoint = length;
        int vr = 1;
        while (i >= 0) {
            int dist = prevPoint - flags[i];
            double time = (double) dist / vr;
            if (curTime + time > t) {
                double delta = t - curTime;
                return prevPoint - delta * vr;
            } else {
                curTime += time;
                prevPoint = flags[i];
                vr++;
                i--;
            }
        }
        int dist = prevPoint;
        double time = (double) dist / vr;
        if (curTime + time > t) {
            double delta = t - curTime;
            return prevPoint - delta * vr;
        } else {
            return -1;
        }
    }
}
```
### Time
O(N * log (1 / epsilon)) -- Запускаем бинарный поиск
### Memory
O(1) -- не используется доп память
### Explication
