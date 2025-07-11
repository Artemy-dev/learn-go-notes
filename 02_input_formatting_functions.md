# Ввод, форматирование и функции в Go

---

## 📥 Ввод данных

Ввод значений осуществляется через `fmt.Scan()` с использованием указателей:

```go
package main

import (
    "fmt"
    "math"
)

func main() {
    const degreeTwo = 2
    var userHeight float64
    var userWeight float64

    fmt.Print("Введите Рост: ")
    fmt.Scan(&userHeight)
    fmt.Print("Введите Вес: ")
    fmt.Scan(&userWeight)

    IMT := userWeight / math.Pow(userHeight, degreeTwo)
    fmt.Print(IMT)
}
```

* `&` — указатель на переменную (для записи значения).
* `fmt.Scan()` — читает данные из стандартного ввода.

---

## 🎨 Форматирование вывода

* `fmt.Println()` — вывод строки с переносом.
* `fmt.Printf()` — форматированный вывод.

```go
fmt.Printf("Индекс массы тела: %.2f", IMT)
```

* `%v` — универсальное представление значения.
* `%.2f` — число с двумя знаками после запятой (тип float).

---

## 🧾 Многострочные строки

Для вывода многострочных сообщений можно использовать обратные кавычки:

```go
fmt.Print(`=== Калькулятор ИМТ ===
Введите Рост: `)
```

Это удобно при создании приветствий и инструкций.

---

## 💾 Сохранение отформатированной строки

Иногда нужно не просто вывести строку, а сохранить её в переменной:

```go
res := fmt.Sprintf("Индекс массы тела: %.2f", IMT)
fmt.Print(res)
```

* `fmt.Sprintf()` возвращает строку, а не выводит её напрямую.

---

## 🔧 Создание функций

Функции в Go позволяют выносить логику и переиспользовать код.

### 📌 Синтаксис:

```go
func имя(аргумент тип, ...) типВозврата {
    // тело
    return значение
}
```

Если аргументы одного типа, можно указать тип один раз:

```go
func calculateIMT(height, weight float64) float64 {
    return weight / math.Pow(height, 2)
}
```

---

## 🔁 Использование функции внутри main

```go
func main() {
    var userHeight float64
    var userWeight float64

    fmt.Println("=== Калькулятор ИМТ ===")
    fmt.Print("Введите Рост: ")
    fmt.Scan(&userHeight)
    fmt.Print("Введите Вес: ")
    fmt.Scan(&userWeight)

    IMT := calculateIMT(userHeight, userWeight)
    getResult(IMT)
}

func calculateIMT(height, weight float64) float64 {
    return weight / math.Pow(height, 2)
}

func getResult(index float64) {
    res := fmt.Sprintf("Индекс массы тела: %.2f", index)
    fmt.Print(res)
}
```

---

## 🔁 Несколько возвращаемых значений

Go позволяет возвращать несколько значений из функции:

```go
func userInput() (float64, float64) {
    var height, weight float64
    fmt.Print("Введите Рост: ")
    fmt.Scan(&height)
    fmt.Print("Введите Вес: ")
    fmt.Scan(&weight)
    return height, weight
}
```

> Типы всех возвращаемых значений указываются явно.

---

## 🔁 Именованные возвращаемые значения

Можно указать имя возвращаемой переменной:

```go
func calculateIMT(height, weight float64) (IMT float64) {
    IMT = weight / math.Pow(height, 2)
    return
}
```

* Такая запись может повысить читаемость.
* Можно использовать `return` без указания переменной.

---

## 📌 Обозначения

* `:=` — создание новой переменной и присваивание значения.
* `=` — присваивание значения существующей переменной.

---

## 📌 Вывод

Ты изучил:

* Как считывать пользовательский ввод.
* Как форматировать вывод и сохранять строку.
* Как создавать и вызывать функции.
* Как использовать возвращаемые значения (в том числе множественные).
