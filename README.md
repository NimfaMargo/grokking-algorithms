[Простые алгоритмы](#простые-алгоритмы)   
[O-большое](#время-выполнения-o-большое)   
[Массивы и связанные списки](#массивы-и-связанные-списки)  
[Сортировка выбором](#сортировка-выбором)   
[Рекурсия и Стек](#рекурсия-и-стек)
[Быстрая сортировка](#быстрая-сортировка)

## Простые алгоритмы
### 1) Простой поиск

Перебор массива осуществляется до нахождения нужного элемента.  
Для 99 элемента из 100, потребуется 99 шагов;  
**Количество шагов**: n  
**Время выполнения**: линейное время O(n)  

### 2) Бинарный поиск

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
## Время выполнения, O-большое  
O-большое определяет время выполнения в худшем случае  
### Примеры О-большого  
- O(log n) бинарный поиск
- O(n) простой поиск
- O(n*log n) быстрая сортировка (быстро)
- О(n^2) сортировка выбором (медленно)
- О(n!) задача о коммивояжере (очень медленно)   

***Основное***:   
1. Скорость алгоритмов измеряется не в секундах, а в темпе роста количества операций
2. Время выполнения алгоритмов выражается как О-большое
3. Бинарный поиск намного быстрее простого
4. Время выполнения O(log n) быстрее O(n) с увеличением размера списка оно становится намного быстрее
5. Константы в О-большом иногда могут иметь значение. По этой причине быстрая сортировка O(n log n) быстрее сортировки слиянием O(n log n).
6. При сравнении бинарной и простой сортировки константа не играет роли, потому что O(log n) сильно превосходит O(n).   

## Массивы и связанные списки
- Память компьютера - огромный шкаф с ящиками
- Чтобы сохранить набор элементов используются массивы и списки
- В массиве все элементы хранятся рядом друг с другом
- В списке элементы распределяются в произвольных местах памяти, при этом в одном элементе храниться адрес следующего.
- Массивы обеспечивают быстрое чтение
- Списки обеспечивают быструю вставку и удаление
- Все элементы массива должны быть однотипными  

![](/images/table.png)

## Сортировка выбором
Чтобы найти наименьший элемент в массиве, необходимо проверить каждый элемент  за O(n) -  и эту операцию нужно выполнить n раз. ***O(n * n) = O(n^2)***  
#### Алгоритм
1. Найти наименьший элемент в массиве.  
2. Повторить для всех элементов.   

[Код](https://repl.it/@NimfaMargo/selectionSort)
```
const findSmallest = (arr) => {
 let smallestIndex = 0;
 const smallestItem = arr[smallestIndex];
 for (let i = 1; i < arr.length; i++) {
   if (arr[i] < smallestItem) {
     smallestIndex = i
   }
 }
 return smallestIndex;
};

const selectionSort = (arr) => {
 const newArr = [];
 const range = arr.length
 for (let i = 0; i < range; i++) {
   const smallestIndex = findSmallest(arr);  // n - раз выполнить операцию c O(n)
   newArr.push(arr[smallestIndex]);
   arr.splice(smallestIndex, 1);
 }
 return newArr;
}
selectionSort([1, 3, 7, 2, -1])
```    

## Рекурсия и Стек
- Когда функция вызывает саму себя - это рекурсия.
- В каждой рекурсивной ф-ии должно быть два случая: базовый и рекурсивный
- Стек поддерживает две операци: занесение и извлечение элементов
- Все вызовы функций сохраняются в стеке вызовов
- Если стек вызовов станет очень большим, он займет слишком много памяти.

## Быстрая сортировка
Алгоритм быстрой сортировки уникален тем, что его скорость зависит от выбора опорного элемента.    
- В худшем случае  - O(n^2)  
- В среднем - O(n log n)  
#### В основе стратегия “Разделяй и властвуй”
1. Сначала определяем базовый случай -  простейший из всех возможных
2. Задача делится или сокращается до тех пор, пока не будет сведена к базовому случаю.
#### Алгоритм
1. Выбрать опорный элемент
Разделить массив на два подмассива: элементы, меньшие опорного и элементы большие опорного;
2. Рекурсивно применить быструю сортировку к двум подмассивам;

[Код](https://repl.it/@NimfaMargo/quickSort)

```
const quickSort = (arr) => {
 if (arr.length < 2) {
   return arr;
 }
 const pivot = arr[0];  // опорный элемент
 const less = arr.filter(el => el < pivot);
 const greater = arr.filter(el => el > pivot);
 return [...quickSort(less), pivot, ...quickSort(greater)]
}
quickSort([1, 3, 7, 2, -1, 10])

```
#### Худший и средний случай  
- На завершение каждого уровня сортировки требуется времени **O(n)**, так как выбирается опорный элемент, а потом перебираются все оставшиеся элементы.   
- Высота стека вызовов равна **O(log n)**, тк каждый уровень занимает **O(n)**:
- Весь алгоритм:  **O(n) * O(log n) = O(n log n)** -  лучший случай
- В худшем случае высота равна **O(n)** уровней : **O(n) * O(n) = O(n^2)**
- Если всегда выбирать опорным случайный элемент в массиве, быстрая сортировка в среднем завершится за время **O(n log n)**.
