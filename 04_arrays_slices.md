# Массивы и Слайсы в Go

---

## 📦 Массивы

Массив — набор однотипных элементов **фиксированной длины**.

```go
transactions := [3]int{5, 10, -7}
banks := [2]string{"Alfa", "Sber"}
```

* `[3]int` — массив из 3 элементов типа `int`
* `[2]string` — массив из 2 строк

**Через `var`:**

```go
var transactions [3]int
transactions = [3]int{5, 10, -7}
```

**Пустой массив:**

```go
transactions := [3]int{}    // [0 0 0]
banks := [2]string{}        // [ ]
```

**Обращение по индексу:**

```go
fmt.Println(transactions[1]) // 10
fmt.Println(banks[0])        // Alfa
```

**Диапазон (слайс из массива):**

```go
fmt.Println(transactions[0:2]) // [5 10]
```

**Изменение элемента:**

```go
transactions[0] = 100
banks[1] = "Tinkoff"
```

**Заполнение через цикл:**

```go
for i := 0; i < 3; i++ {
    fmt.Scan(&transactions[i])
}
```

---

## 📊 Слайсы (Slices)

Слайс — это **динамический массив** (без фиксированной длины).

```go
transactions := [5]int{1, 2, 3, 4, 5}
newLine := transactions[1:4] // [2 3 4]
```

**Форматы срезов:**

* `[:3]` — от начала до 3 (не включая)
* `[2:]` — от индекса 2 до конца
* `[:]` — весь массив

**Слайсы ссылаются на ту же память, что и массив:**

```go
transactionsPar := transactions[:]
transactionsPar[0] = 9
// Меняется и transactions
```

---

## 📏 `len()` и `cap()`

```go
trNew := transactions[1:4]
fmt.Println(len(trNew)) // 3
fmt.Println(cap(trNew)) // 4
```

* `len()` — количество элементов
* `cap()` — вместимость до конца массива

---

## ➕ Добавление элементов: `append()`

```go
tr := []int{1, 2, 3}
tr = append(tr, 4)              // [1 2 3 4]
tr = append(tr, 5, 6, 7)        // [1 2 3 4 5 6 7]
```

**Объединение слайсов:**

```go
tr1 := []int{1, 2}
tr2 := []int{3, 4}
tr1 = append(tr1, tr2...)       // [1 2 3 4]
```

---

## 🔁 Циклы с `range`

```go
for i, v := range sl1 {
    fmt.Println(i, v)
}

for _, v := range sl1 {
    fmt.Println(v)
}

for i := range 3 {
    fmt.Println(sl1[i])
}
```

**Сумма всех элементов:**

```go
sum := 0
for _, v := range nums {
    sum += v
}
fmt.Println(sum)
```

---

## 🧱 `make()` — создание слайсов

**Пустой слайс + `append()`:**

```go
nums1 := []int{}
nums1 = append(nums1, 5, 10, 15)
fmt.Println(nums1)      // [5 10 15]
fmt.Println(cap(nums1)) // 3
```

**Слайс фиксированной длины:**

```go
nums2 := make([]int, 3)
nums2 = append(nums2, 5, 10, 15)
fmt.Println(nums2)      // [0 0 0 5 10 15]
fmt.Println(cap(nums2)) // 6
```

**Слайс с нулевой длиной и ёмкостью 5:**

```go
nums3 := make([]int, 0, 5)
nums3 = append(nums3, 5, 10, 15)
fmt.Println(nums3)      // [5 10 15]
fmt.Println(cap(nums3)) // 5
```

**Авторасширение ёмкости:**

```go
nums3 = append(nums3, 20, 25, 30)
fmt.Println(nums3)      // [5 10 15 20 25 30]
fmt.Println(cap(nums3)) // 10
```

---

## 📌 Вывод

Ты изучил:

* Что такое массивы — фиксированной длины и однотипные элементы
* Как создавать и использовать массивы, обращаться по индексам, изменять элементы
* Что такое слайсы — динамические массивы без фиксированной длины
* Как брать слайсы из массивов с помощью срезов `[start:end]`
* Разницу между `len()` и `cap()` для слайсов и массивов
* Добавление элементов в слайсы с помощью `append()`
* Использование циклов `for` с `range` для обхода слайсов
* Как объединять слайсы через распаковку `...`
* Оптимизацию памяти с помощью функции `make()` для предварительного выделения ёмкости слайса
* Поведение `cap()` при добавлении элементов сверх выделенной емкости (авторасширение)
