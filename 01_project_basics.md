# Создание проекта и основы Go

---

## 🚀 Инициализация проекта

1. **Переход в нужную директорию:**

```bash
cd ~/Documents
```

2. **Создание новой папки для проекта:**

```bash
mkdir go-demo
cd go-demo
```

3. **Инициализация Go-модуля:**

```bash
go mod init go-demo
```

> 💬 Вывод: `go: creating new go.mod: module go-demo`

4. **Открытие проекта в VS Code:**

```bash
code .
```

5. **Создание файла `main.go`:**

```go
package main

import "fmt"

func main() {
    fmt.Printf("Hello!")
}
```

6. **Запуск программы:**

```bash
go run main.go
```

---

## 📦 Структура пакетов и импортов

Go-приложение может состоять из нескольких пакетов:

```
[ваше приложение]
├── [package main]          // точка входа
├── [package services]      // собственные модули
├── [package fmt]           // стандартный пакет
└── [package github.com/x]  // внешние зависимости
```

* `main` — точка входа в приложение.
* `fmt` — стандартный пакет для вывода в консоль.
* `github.com/...` — внешние зависимости.

Пример:

```go
package main

import "fmt"

func main() {
    fmt.Printf("Hello!")
}
```

---

## 📁 Go Build

* Для создания бинарного файла используем:

```bash
go build
```

> 📦 Будет создан файл `go-demo`, который можно запустить как:
>
> ```bash
> ./go-demo
> ```

* Чтобы исключить бинарник из коммитов, создаём `.gitignore`:

```text
go-demo
```

Теперь в репозитории сохраняются только исходники и go.mod.

---

## 🧮 Переменные и типы

Объявление переменной с автоматическим определением типа:

```go
var userHeight = 1.86
```

* `var` — ключевое слово для объявления переменных.
* Тип (например, `float64`) определяется автоматически.

### ❗ Ошибка типов:

```go
var userHeight = 1.86
var userWeight = 80
var IMT = userWeight / userHeight // Ошибка: int / float64
```

### ✅ Решение — указание типа:

```go
var userHeight = 1.86
var userWeight float64 = 80
var IMT = userWeight / userHeight
```

### ✅ Или — конвертация типа:

```go
var userHeight = 1.86
var userWeight = 80
var IMT = float64(userWeight) / userHeight
```

---

## 🧠 Возведение в степень с math.Pow

Для возведения числа в степень:

```go
import "math"

math.Pow(a, b) // a^b
```

Пример — расчёт ИМТ (индекса массы тела):

```go
package main

import (
    "fmt"
    "math"
)

func main() {
    var userHeight = 1.86
    var userWeight float64 = 80
    var IMT = userWeight / math.Pow(userHeight, 2)
    fmt.Print(IMT)
}
```

---

## 📝 Синтаксис переменных

### 🔹 Короткое объявление (`:=`):

```go
userHeight := 1.86
```

* Используется в теле функции.
* Нельзя указать явный тип: `userHeight float64 := 1.86` — ❌ ошибка.

### 🔹 Объявление без инициализации:

```go
var userWeight float64
userWeight = 80
```

> ❗ Тип обязателен, иначе ошибка компиляции.

### 🔹 Ошибочный пример:

```go
var userWeight
userWeight = 80
```

> ❌ Ошибка: `syntax error: unexpected newline, expected type`

### 🔹 Множественное объявление:

```go
var userHeight, userWeight float64 = 1.86, 100
```

Или коротко:

```go
userHeight, userWeight := 1.86, 100
```

> В этом случае `userHeight` будет `float64`, `userWeight` — `int` (если явно не указать тип).

### 📌 Стандарты:

* `var x float64` — указание типа, без значения.
* `var x float64 = 80` — указание типа и значения.
* `x := 80.0` — автоматическое определение типа.

---

## 🔒 Константы

* Объявляются через `const`, значение изменить нельзя.

Пример:

```go
const degreeTwo = 2

userHeight := 1.86
userWeight := 80.0
IMT := userWeight / math.Pow(userHeight, degreeTwo)
```

> 📌 Константы нестрого типизированы (`untyped`), если не указать тип явно.

---

## 📌 Вывод

Ты умеешь:

* создавать Go-проекты и запускать их;
* использовать модули и собирать бинарники;
* работать с переменными, типами, константами;
* подключать пакеты и использовать `math.Pow`.
