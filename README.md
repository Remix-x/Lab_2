# Lab_2  
**Cranopol Andrei, I2502**

---

## 1. Создание функции для вывода массива

Создаем функцию `print`, которая выводит элементы массива в консоль:

```js
function print(array) {
    for (let i = 0; i < array.length; i++) {
        console.log(`Element ${i}: ${array[i]}`);
    }
}
```
![alt text](/images/image.png)

1.1 Функция printArray1, котрая выводит массив:

```js
function printArray1(array) {
    for (let i = 0; i < array.length; i++) {
        console.log(` ${i}: ${array[i]}`);
    }
}
```
## 2. Реализовать функцию forEach

Функция forEach принимает массив и callback-функцию, применяя callback к каждому элементу массива:

```js
function forEach (array, callback) {
    for (let i = 0; i < array.length; i++) {
        callback(array[i], i, array);
    }
}

forEach([1, 2, 3], (element, index, array) => {
    console.log(`Element: ${element}, Index: ${index}, Array: ${array}`);
});
```
![alt text](/images/image-1.png)

## 3. Реализовать функцию map
Функция map принимает массив и callback-функцию,  применяя callback к каждому элементу массив и возвращает в новый массив `result`:

```js
function map(array, callback) {
    let result = [];
    for (let i = 0; i < array.length; i++) {
        result[i] = callback(array[i]);
    }
    return result;
}
const numbers = [2,4,6]
const squared = map(numbers, (element) => {
    return element * element;
});
console.log(squared);
```
![alt text](/images/image-2.png)

## 4. Реализовать функцию filter
Функция filter применяет callback к каждому элементу массива и возвращает новый массив result с элементами, которые удовлетворяют условию:
```js
function filter(array, callback){
    let result = [];
    for(let i = 0; i < array.length; i++){
        result[i] = callback(array[i]);
    }
    return result;
}

const newNumbers = [19, 2 , 3 , 5 ,12];
const filtered = filter(newNumbers, (element) => {
    if (element % 2 == 0) {
        return element;
    }
});
console.log(filtered);
```
![alt text](/images/image-3.png)

## 5. Реализовать функцию find
Функция find возвращает первый элемент, который удовлетворяет условию callback:
```js
function find(array, callback) {
    let result;
    for (let i = 0; i < array.length; i++) {
        if (callback(array[i])) {
            result = array[i];
            break;
        }
    }
    return result;
}

const cisla = [1, 3, 4, 5, 6];
const found = find(cisla, (element) => {
    return element % 2 == 0;
});
console.log('Функция find вернула:', found);
```
![alt text](/images/image-4.png)


## 6. Реализовать функцию some
Функция some проверяет, есть ли хотя бы один элемент, удовлетворяющий условию callback, и возвращает true или false:

```js
function some(array, callback) {
    for (let i = 0; i < array.length; i++) {
        if (callback(array[i])) {
            return true;
        }
    }
    return false;
}

const nums = [1, 2, 30, 44, 53];
const hasEven = some(nums, (element) => {
    return element % 2 == 0;
});
console.log('Функция some вернула:', hasEven);
```
![alt text](/images/image-5.png)

## 7. Реализовать функцию every
Функция every проверяет, удовлетворяют ли все элементы массива условию callback:

```js
function every(array, callback){
    for (let i = 0; i < array.length; i++) {
        if(!callback(array[i])){
            return false;
        }
    }
    return true;
}

const num = [2, 4, 6, 8, 9];
const allEven = every(num, (element) => {
    return element % 2 == 0;
});
console.log('Функция every вернула:', allEven);
```
![alt text](/images/image-6.png)

## 8. Реализовать функцию reduce
Функция reduce применяет callback к каждому элементу массива, используя initialValue как стартовое значение аккумулятора, и возвращает итоговое значение:

```js
function reduce(array, callback, initialValue) {
    let accumulator = initialValue;
    for (let i = 0; i < array.length; i++) {
        accumulator = callback(accumulator, array[i]);

    }
    return accumulator;
}
//num = [2, 4, 6, 8, 9];
const sum = reduce(num, (accumulator, current) => {
    return accumulator + current;
}, 0);
console.log('Сумма элементов массива:', sum);git commit -m "update lab2"
```
![alt text](/images/image-7.png)

## Контрольные вопросы

### 1. В чём преимущества использования колбэк-функций при работе с массивами?

- Позволяют **универсально обрабатывать массивы** без дублирования кода.  
- Делают код **коротким и читаемым**, так как логику обработки можно вынести в callback.  
- Легко создавать **кастомные функции** для разных задач.  
- Упрощают **композицию операций**, например, последовательное использование `map`, `filter`, `reduce`.

---

### 2. Какие проблемы могут возникнуть при использовании колбэков и как их избежать?

- **Неправильное использование элементов массива**: если колбэк изменяет исходный массив, это может привести к неожиданным результатам.  
  - Решение: не изменять исходный массив внутри колбэка, использовать новый массив (например, `map` или `filter` возвращают новые массивы).  

- **Ошибка в логике колбэка**: если колбэк возвращает неверное значение, функции вроде `filter`, `some`, `every` будут работать неправильно.  
  - Решение: проверять, что колбэк возвращает `true`/`false` там, где это требуется, или правильное значение для `map`/`reduce`.  

- **Пропуск элементов**: неправильно написанный цикл в колбэке может пропустить элементы массива.  
  - Решение: использовать правильный индекс и всегда проходить по всему массиву.
---

### 3. Как реализовать функции `map`, `filter`, `find`, `some`, `every` и `reduce` без использования встроенных методов массивов?

- Использовать **цикл `for`** для обхода массива.  
- Для каждого элемента вызывать **callback-функцию**.  
- Для `map` и `filter` — создавать новый массив и добавлять результаты.  
- Для `find` — возвращать **первый элемент**, удовлетворяющий условию.  
- Для `some` — возвращать **true**, как только найден подходящий элемент; иначе `false`.  
- Для `every` — возвращать **false**, как только найден неподходящий элемент; иначе `true`.  
- Для `reduce` — хранить **аккумулятор**, обновлять его на каждом шаге и возвращать итоговое значение.
