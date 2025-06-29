# Map — работа с ключами и значениями в Go

---

## 📝 Что такое Map?

Map — это структура данных, которая хранит пары **ключ-значение**.

Пример создания и использования:

```go
func main() {
    m := map[string]string{
        "GitHub": "https://github.com/",
    }

    fmt.Println(m)           // Вывод: map[GitHub:https://github.com/]
    fmt.Println(m["GitHub"]) // Вывод: https://github.com/
}
```

* `map` — ключевое слово для создания отображения.
* `[string]` — тип ключа.
* `string` — тип значения.
* `"GitHub"` — ключ.
* `"https://github.com/"` — значение.
* Пары ключ-значение разделяются запятыми.

---

## ✏️ Изменение Map

### Изменение значения по ключу

```go
func main() {
    m := map[string]string{
        "GitHub": "https://github.com/",
    }

    fmt.Println(m)  // Вывод: map[GitHub:https://github.com/]

    m["GitHub"] = "github.com" // Изменяем значение

    fmt.Println(m)  // Вывод: map[GitHub:github.com]
}
```

### Добавление новой пары ключ-значение

```go
func main() {
    m := map[string]string{
        "GitHub": "github.com",
    }

    m["Google"] = "google.com"  // Добавляем новую пару

    fmt.Println(m)  // Вывод: map[GitHub:github.com Google:google.com]
}
```

---

## ❌ Удаление элементов из Map

Для удаления пары ключ-значение используется функция `delete()`:

```go
func main() {
    m := map[string]string{
        "GitHub": "github.com",
        "Google": "google.com",
        "Yandex": "yandex.ru",
    }
    fmt.Println(m)  // Вывод: map[GitHub:github.com Google:google.com Yandex:yandex.ru]

    delete(m, "Yandex")          // Удаляем ключ "Yandex"
    fmt.Println(m)  // Вывод: map[GitHub:github.com Google:google.com]
}
```

---

## 🔄 Итерация по Map

Обход всех пар ключ-значение в Map происходит через `for range`:

```go
func main() {
    m := map[string]int{"a": 1, "b": 2, "c": 3}

    for k, v := range m {
        fmt.Println("Ключ:", k, "Значение:", v)
    }
}
```

**Пример вывода:**

```
Ключ: a Значение: 1
Ключ: b Значение: 2
Ключ: c Значение: 3
```

---

## 🎯 Управление потоком с Label и break

Пример меню с Map и выбором действий:

```go
func main() {
    var choice int
    m := map[string]string{}
    fmt.Println("Добро пожаловать!")

    for {
        fmt.Println("Выберете действие:\n1 - Список закладок\n2 - Добавить\n3 - Удалить\n0 - Выход")
        fmt.Scan(&choice)

        if choice == 1 {
            mapPrint(m)
        } else if choice == 2 {
            mapAppend(m)
        } else if choice == 3 {
            mapDel(m)
        } else if choice == 0 {
            break
        }
    }
}
```

* `break` завершает ближайший внешний цикл `for`.

---

### ❓ Особенности break в switch

```go
func main() {
    var command int
    for {
        fmt.Print("Введите команду 1 - start, 2 - stop, 3 - exit: ")
        fmt.Scanln(&command)

        switch command {
        case 1:
            fmt.Println("Запуск системы...")
        case 2:
            fmt.Println("Остановка системы...")
        case 3:
            fmt.Println("Выход из программы.")
            break Menu // Завершает switch, но не цикл for
        }
    }
}
```

---

### 🏷️ Использование label для break цикла

Для выхода из внешнего цикла `for` изнутри `switch` используем метки:

```go
func main() {
    var command int
Menu:
    for {
        fmt.Print("Введите команду 1 - start, 2 - stop, 3 - exit: ")
        fmt.Scanln(&command)

        switch command {
        case 1:
            fmt.Println("Запуск системы...")
        case 2:
            fmt.Println("Остановка системы...")
        case 3:
            fmt.Println("Выход из программы.")
            break Menu // Завершает цикл с меткой Menu
        }
    }
}
```

* `Menu:` — метка для цикла `for`.
* `break Menu` — прерывает цикл с меткой `Menu`.

---

## 🆕 Type Alias — создание псевдонимов типов

Чтобы сократить часто используемый тип `map[string]string`, создаём псевдоним:

```go
type Smap = map[string]string
```

Теперь вместо полного типа можно использовать `Smap`:

```go
func main() {
    m := Smap{}
}
```

И функции:

```go
func mapPrint(m Smap) { /* ... */ }
func mapAppend(m Smap) { /* ... */ }
func mapDel(m Smap) { /* ... */ }
```

---

## 🛠️ Реализация функций для работы с Map

```go
func mapPrint(m Smap) {
    if len(m) == 0 {
        fmt.Println("Список пуст!")
        return
    }
    for k, v := range m {
        fmt.Println("Название:", k, "URL:", v)
    }
}

func mapAppend(m Smap) {
    var name, url string
    fmt.Println("Введите название")
    fmt.Scan(&name)
    fmt.Println("Введите ссылку")
    fmt.Scan(&url)
    m[name] = url
}

func mapDel(m Smap) {
    var name string
    fmt.Println("Введите название, которое хотите удалить")
    fmt.Scan(&name)
    delete(m, name)
}
```

---

## 🚀 Создание Map с помощью make()

```go
type Smap = map[string]string

func main() {
    m := make(Smap, 5) // Создаём Map с выделением памяти под 5 элементов

    m["a"] = "1"
    m["b"] = "2"
    m["c"] = "3"

    fmt.Println("Длина:", len(m)) // Вывод: Длина: 3
}
```

---

### 📊 Сравнение make и обычного объявления Map

```go
func main() {
    m1 := make(map[int]string, 1000) // с hint (предварительной памятью)
    m2 := map[int]string{}            // без hint

    for i := 0; i < 1000; i++ {
        m1[i] = "value"
    }

    for i := 0; i < 1000; i++ {
        m2[i] = "value"
    }
}
```

* Map, созданный с помощью `make` и выделением памяти, заполняется примерно на 15-20% быстрее, чем обычный `map`.

---

## 📌 Вывод

Ты изучил:

* Что такое Map — структура данных ключ-значение.
* Создание Map и обращение к элементам.
* Изменение, добавление и удаление пар ключ-значение.
* Итерацию по Map через `for range`.
* Использование меток (labels) для управления циклом.
* Создание псевдонимов типов через `type Alias`.
* Использование `make()` для создания Map с выделением памяти.
* Особенности производительности при создании Map с `make()`.
