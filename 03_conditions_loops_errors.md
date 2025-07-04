# Условия, циклы и ошибки в Go

---

## ✅ Условия `if`

### Вариант 1 — простое условие:

```go
if IMT < 16 {
    fmt.Println("Недостаток веса")
}
```

### Вариант 2 — через промежуточную переменную:

```go
isLean := IMT < 16
if isLean {
    fmt.Println("Недостаток веса")
}
```

* Подходит для сложных выражений или читаемости.

---

## 📐 Множественные условия `if / else if / else`

```go
if IMT < 16 {
    fmt.Println("\nСильный дефицит массы тела")
} else if IMT >= 16 && IMT < 18.5 {
    fmt.Println("\nДефицит массы тела")
} else if IMT >= 18.5 && IMT < 25 {
    fmt.Println("\nНорма")
} else if IMT >= 25 && IMT < 30 {
    fmt.Println("\nИзбыточная масса")
} else if IMT >= 30 && IMT < 35 {
    fmt.Println("\n1-я степень ожирения")
} else if IMT >= 35 && IMT < 40 {
    fmt.Println("\n2-я степень ожирения")
} else {
    fmt.Println("\n3-я степень ожирения")
}
```

### Более лаконичный вариант:

```go
if IMT < 16 {
    fmt.Println("\nСильный дефицит массы тела")
} else if IMT < 18.5 {
    fmt.Println("\nДефицит массы тела")
} else if IMT < 25 {
    fmt.Println("\nНорма")
} else if IMT < 30 {
    fmt.Println("\nИзбыточная масса")
} else if IMT < 35 {
    fmt.Println("\n1-я степень ожирения")
} else if IMT < 40 {
    fmt.Println("\n2-я степень ожирения")
} else {
    fmt.Println("\n3-я степень ожирения")
}
```

> ⛔ Проверяется только первое подходящее условие.

---

## 🔀 Switch

Альтернатива `if/else`:

```go
switch {
case IMT < 16:
    fmt.Println("\nСильный дефицит массы тела")
case IMT < 18.5:
    fmt.Println("\nДефицит массы тела")
case IMT < 25:
    fmt.Println("\nНорма")
case IMT < 30:
    fmt.Println("\nИзбыточная масса")
case IMT < 35:
    fmt.Println("\n1-я степень ожирения")
case IMT < 40:
    fmt.Println("\n2-я степень ожирения")
default:
    fmt.Println("\n3-я степень ожирения")
}
```

---

## 🔁 Циклы `for`

### Классическая форма:

```go
for i := 0; i < 3; i++ {
    fmt.Println(i)
}
```

> `i++` = `i = i + 1`

### Альтернативный вывод:

```go
fmt.Printf("%d\n", i)
```

### С внешним счётчиком:

```go
count := 0
for count < 3 {
    fmt.Println("Hello!")
    count++
}
```

### Бесконечный цикл:

```go
count := 0
for {
    fmt.Println(count)
    count++
}
```

### Всё в одной строке:

```go
for count := 1; ; count++ {
    fmt.Println(count)
}
```

---

## ⛔ `break` и `continue`

```go
count := 10
for {
    if count == 8 {
        count--
        continue
    } else if count == 5 {
        break
    } else {
        fmt.Printf("%d\n", count)
        count--
    }
}
```

Вывод:

```
10
9
7
6
```

* `continue` — пропускает текущую итерацию.
* `break` — завершает цикл.

---

## ❗ Обработка ошибок (error)

### Создание ошибки:

```go
import "errors"

func calculateIMT(height, weight float64) (float64, error) {
    if height <= 0 || weight <= 0 {
        return 0, errors.New("Указан не верный вес/рост")
    }
    IMT := weight / math.Pow(height/100, 2)
    return IMT, nil
}
```

### Использование:

```go
IMT, err := calculateIMT(userHeight, userWeight)
if err != nil {
    fmt.Println(err)
    continue
}
```

> `_` — позволяет проигнорировать ошибку:

```go
IMT, _ := calculateIMT(userHeight, userWeight)
```

---

## 💥 Panic

`panic` завершает выполнение программы с сообщением об ошибке:

```go
if err != nil {
    panic("Некорректный ввод")
}
```

Вывод:

```
panic: Некорректный ввод

main.main()
    /path/to/main.go:18 +0x11f
exit status 2
```

* `main.main()` — функция, где произошла ошибка.
* `:18` — номер строки.
* `exit status 2` — код завершения.

> Используй `error` для ожидаемых ошибок и `panic` для критических случаев.

---

## 📌 Вывод

Ты изучил:

* Условия: `if`, `else if`, `switch`
* Циклы: `for`, с условиями, счётчиком, бесконечные
* Управление потоком: `break`, `continue`
* Обработка ошибок через `error` и `panic`
