## Простые алгоритмы
#### 1) Простой поиск

Перебор массива осуществляется до нахождения нужного элемента.
Для 99 элемента из 100, потребуется 99 шагов;
**Количество шагов**: n
**Время выполнения**: линейное время O(n)

#### 2) Бинарный поиск

Каждый раз  выбирается элемент в середине диапазона и исключается половина элементов, которая не подходит.
**Время выполнения**: логарифмическое время O(log n) //  по основанию 2

[Код](https://repl.it/@NimfaMargo/binary-search)
```
const binarySearch = (arr, item) => {
 let low = 0; // верхняя граница части списка
 let high = arr.length - 1; // нижняя граница

 while (low <= high) { // пока эта часть не сократиться до одного элемента
   const middle = Math.round((low + high) / 2);
   const guess = arr[middle];
   if (guess === item) {
     return middle;
   } else if (guess > item) {
     high = middle - 1;
   } else if (guess < item) {
     low = middle + 1;
   } else {
     return null;
   }
 }
}
binarySearch([1, 2, 3, 6, 8, -1], 2)
```
