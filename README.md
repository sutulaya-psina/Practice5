# Practice5
1. Напишите функцию, которая проверяет, является ли переданное число простым. Ваша программа должна использовать циклы для проверки делителей, и если число не является простым, выводить первый найденный делитель.
```
package main

import (
 "fmt"
)

func isPrime(n int) bool {
 if n <= 1 {
  return false
 }
 for i := 2; i*i <= n; i++ {
  if n%i == 0 {
   fmt.Printf("Первый делитель числа %d: %d\n", n, i)
   return false
  }
 }
 return true
}

func main() {
 var number int
 fmt.Print("Введите число для проверки: ")
 fmt.Scanf("%d", &number)

 if isPrime(number) {
  fmt.Println("Число", number, "является простым.")
 } else {
  fmt.Println("Число", number, "не является простым.")
 }
}
```
2. Напишите программу для нахождения наибольшего общего делителя (НОД) двух чисел с использованием алгоритма Евклида. Используйте цикл `for` для вычислений. Листинг:
```
package main

import (
 "fmt"
)

func gcd(a int, b int) int {
 for b != 0 {
  a, b = b, a%b
 }
 return a
}

func main() {
 var num1, num2 int

 fmt.Print("Введите первое число: ")
 fmt.Scan(&num1)

 fmt.Print("Введите второе число: ")
 fmt.Scan(&num2)

 result := gcd(num1, num2)

 fmt.Printf("Наибольший общий делитель (%d, %d) = %d\n", num1, num2, result)
}
```
3. Реализуйте сортировку пузырьком для списка целых чисел. Программа должна выполнять сортировку на месте и выводить каждый шаг изменения массива.
```
package main

import (
 "fmt"
)

func bubbleSort(arr []int) {
 n := len(arr)

 for i := 0; i < n-1; i++ {
  swapped := false 
  for j := 0; j < n-i-1; j++ {
   if arr[j] > arr[j+1] {
    arr[j], arr[j+1] = arr[j+1], arr[j] // Обмен значений
    swapped = true
   }
  }

  if !swapped {
   break
  }

  fmt.Println("Шаг", i+1, ": ", arr) 
 }
}

func main() {
 arr := []int{64, 34, 25, 12, 22, 11, 90}
 fmt.Println("Исходный массив:", arr)

 bubbleSort(arr)

 fmt.Println("Отсортированный массив:", arr)
}
```
4.Напишите программу, которая выводит таблицу умножения в формате матрицы 10x10. Используйте циклы для генерации строк и столбцов.
```
package main

import (
 "fmt"
 "strings"
)

func main() {
 const size = 10
 var table [size][size]int

 for i := 0; i < size; i++ {
  for j := 0; j < size; j++ {
   table[i][j] = (i + 1) * (j + 1)
  }
 }

 for i := 0; i < size; i++ {
  row := make([]string, size)
  for j := 0; j < size; j++ {
   row[j] = fmt.Sprintf("%3d", table[i][j])
  }
  fmt.Println(strings.Join(row, " "))
 }
}
```
5. Напишите функцию для вычисления числа Фибоначчи с использованием мемоизации (сохранение ранее вычисленных результатов). Программа должна использовать рекурсию и условные операторы.
```
package main

import (
 "fmt"
)

var fibMemo = map[int]int{
 0: 0,
 1: 1,
}

func fibonacci(n int) int {
 if val, ok := fibMemo[n]; ok {
  return val
 }

 fibN := fibonacci(n-1) + fibonacci(n-2)
 fibMemo[n] = fibN
 return fibN
}

func main() {
 var input int
 fmt.Print("Введите номер числа Фибоначчи: ")
 fmt.Scanf("%d", &input)

 result := fibonacci(input)
 fmt.Printf("Число Фибоначчи для %d: %d\n", input, result)
}
```
6. Напишите программу, которая принимает целое число и выводит его в обратном порядке. Например, для числа 12345 программа должна вывести 54321. Используйте цикл для обработки цифр числа.
```
package main

import (
 "fmt"
 "strconv"
)

func reverseNumber(n int) string {
 reversed := ""

 for n != 0 {
  lastDigit := n % 10
  reversed += strconv.Itoa(lastDigit)
  n /= 10
 }

 return reversed
}

func main() {
 var number int
 fmt.Print("Введите целое число: ")
 fmt.Scanln(&number)

 reversed := reverseNumber(number)
 fmt.Printf("Обратное число: %s\n", reversed)
}
```
7. Напишите программу, которая выводит треугольник Паскаля до заданного уровня. Для этого используйте цикл и массивы для хранения предыдущих значений строки треугольника. 
```
package main

import (
 "fmt"
)

func factorial(n int) int {
 if n == 0 || n == 1 {
  return 1
 }
 result := 1
 for i := 2; i <= n; i++ {
  result *= i
 }
 return result
}

func binomialCoefficient(n, k int) int {
 return factorial(n) / (factorial(k) * factorial(n-k))
}

func pascalTriangle(level int) {
 for row := 0; row < level; row++ {
  for space := 0; space < level-row; space++ {
   fmt.Print(" ")
  }
  
  for col := 0; col <= row; col++ {
   coef := binomialCoefficient(row, col)
   fmt.Printf("%4d", coef)
  }
  fmt.Println()
 }
}

func main() {
 var level int
 fmt.Print("Введите уровень треугольника Паскаля: ")
 fmt.Scan(&level)
 pascalTriangle(level)
}
```
8. Напишите программу, которая проверяет, является ли число палиндромом (одинаково читается слева направо и справа налево). Не используйте строки для решения этой задачи — работайте только с числами.
```
package main

import (
 "fmt"
)

func getLengthOfNumber(n int) int {
 length := 0
 for n > 0 {
  n /= 10
  length++
 }
 return length
}

func getFirstDigit(n int) int {
 firstDigit := n
 for firstDigit >= 10 {
  firstDigit /= 10
 }
 return firstDigit
}

func getLastDigit(n int) int {
 return n % 10
}

func isPalindrome(n int) bool {
 length := getLengthOfNumber(n)

 for length > 1 {
  firstDigit := getFirstDigit(n)
  lastDigit := getLastDigit(n)

  if firstDigit != lastDigit {
   return false
  }

  digitsToRemove := firstDigit * (int)(pow(10, float64(length-1)))
  n -= digitsToRemove
  n /= 10
  length -= 2
 }

 return true
}

func pow(base float64, exponent float64) float64 {
 return float64(int(math.Pow(base, exponent)))
}

func main() {
 var number int
 fmt.Print("Введите число: ")
 fmt.Scan(&number)

 if isPalindrome(number) {
  fmt.Println("Число является палиндромом.")
 } else {
  fmt.Println("Число не является палиндромом.")
 }
}
```
9. Напишите функцию, которая принимает массив целых чисел и возвращает одновременно максимальный и минимальный элемент с использованием одного прохода по массиву.
```
package main

import (
 "fmt"
)

func findMinMax(arr []int) (min, max int) {
 min = arr[0]
 max = arr[0]

 for _, value := range arr[1:] {
  if value < min {
   min = value
  }
  if value > max {
   max = value
  }
 }

 return min, max
}

func main() {
 arr := []int{23, -17, 43, 5, -29, 78, 102, -51}
 min, max := findMinMax(arr)
 fmt.Printf("Минимальное значение: %d\nМаксимальное значение: %d\n", min, max)
}
```
10. Напишите программу, которая загадывает случайное число от 1 до 100, а пользователь пытается его угадать. Программа должна давать подсказки "больше" или "меньше" после каждой попытки. Реализуйте ограничение на количество попыток.
```
package main

import (
 "fmt"
 "math/rand"
 "time"
)

const maxTries = 6

func main() {
 rand.Seed(time.Now().UnixNano())
 target := rand.Intn(100) + 1 

 fmt.Println("Добро пожаловать в игру 'Угадай число'!")
 fmt.Println("Я загадал число от 1 до 100. У вас есть 6 попыток, чтобы его угадать.")

 var guess int
 tries := 0

 for tries < maxTries {
  fmt.Print("\nВаша попытка: ")
  fmt.Scanf("%d", &guess)

  if guess < target {
   fmt.Println("Загаданное число больше.")
  } else if guess > target {
   fmt.Println("Загаданное число меньше.")
  } else {
   fmt.Println("Верно! Вы угадали число.")
   break
  }

  tries++
 }

 if tries == maxTries {
  fmt.Println("\nК сожалению, вы исчерпали все попытки. Правильный ответ был:", target)
 }
}
```
11. Напишите программу, которая проверяет, является ли число числом Армстронга (число равно сумме своих цифр, возведённых в степень, равную количеству цифр числа). Например, 153 = 1³ + 5³ + 3³.
```
package main

import (
 "fmt"
 "math"
)

func countDigits(n int) int {
 count := 0
 for n > 0 {
  n /= 10
  count++
 }
 return count
}

func sumOfPoweredDigits(n, power int) int {
 sum := 0
 temp := n
 for temp > 0 {
  digit := temp % 10
  sum += int(math.Pow(float64(digit), float64(power)))
  temp /= 10
 }
 return sum
}

func isArmstrongNumber(n int) bool {
 digitsCount := countDigits(n)
 sum := sumOfPoweredDigits(n, digitsCount)
 return n == sum
}

func main() {
 var number int
 fmt.Print("Введите число: ")
 fmt.Scan(&number)

 if isArmstrongNumber(number) {
  fmt.Println("Да, это число Армстронга.")
 } else {
  fmt.Println("Нет, это не число Армстронга.")
 }
}
```
12. Напишите программу, которая принимает строку и выводит количество уникальных слов в ней. Используйте `map` для хранения слов и их количества.
```
package main

import (
 "fmt"
 "strings"
)

func main() {
 var inputString string
 fmt.Print("Введите строку: ")
 fmt.Scanln(&inputString)

 wordsMap := make(map[string]bool)
 uniqueWordsCount := 0

 words := strings.Fields(inputString)

 for _, word := range words {
  wordLowerCase := strings.ToLower(word)

  if _, exists := wordsMap[wordLowerCase]; !exists {
   wordsMap[wordLowerCase] = true
   uniqueWordsCount++
  }
 }

 fmt.Printf("Количество уникальных слов: %d\n", uniqueWordsCount)
}
```
13. Реализуйте клеточный автомат "Жизнь" Конвея для двухмерного массива. Каждая клетка может быть либо живой, либо мертвой. На каждом шаге состояния клеток изменяются по следующим правилам:
   - Живая клетка с двумя или тремя живыми соседями остаётся живой, иначе умирает.
   - Мёртвая клетка с тремя живыми соседями оживает.
   Используйте циклы для обработки клеток.
```
package main

import (
 "fmt"
 "math/rand"
 "os"
 "os/exec"
 "time"
)

const (
 width  = 50
 height = 30
)

type cellState byte

const (
 dead cellState = iota
 alive
)

type grid [][]cellState

func newGrid() grid {
 g := make(grid, height)
 for i := range g {
  g[i] = make([]cellState, width)
  for j := range g[i] {
   if rand.Float64() < 0.2 {
    g[i][j] = alive
   } else {
    g[i][j] = dead
   }
  }
 }
 return g
}

func copyGrid(g grid) grid {
 newG := make(grid, height)
 for i := range g {
  newG[i] = make([]cellState, width)
  copy(newG[i], g[i])
 }
 return newG
}

func countLiveNeighbors(g grid, x, y int) int {
 count := 0
 for i := -1; i <= 1; i++ {
  for j := -1; j <= 1; j++ {
   if i == 0 && j == 0 {
    continue
   }
   xi := (x + i + width) % width
   yi := (y + j + height) % height
   if g[yi][xi] == alive {
    count++
   }
  }
 }
 return count
}

func updateCell(g grid, x, y int) cellState {
 liveNeighbors := countLiveNeighbors(g, x, y)
 cell := g[y][x]
 switch cell {
 case alive:
  if liveNeighbors < 2 || liveNeighbors > 3 {
   return dead
  }
  return alive
 case dead:
  if liveNeighbors == 3 {
   return alive
  }
  return dead
 default:
  panic("Invalid cell state")
 }
}

func step(g grid) grid {
 nextGen := copyGrid(g)
 for y := 0; y < height; y++ {
  for x := 0; x < width; x++ {
   nextGen[y][x] = updateCell(g, x, y)
  }
 }
 return nextGen
}

func render(g grid) {
 clearScreen()
 for y := 0; y < height; y++ {
  for x := 0; x < width; x++ {
   if g[y][x] == alive {
    fmt.Print("*")
   } else {
    fmt.Print(" ")
   }
  }
  fmt.Println()
 }
 time.Sleep(200 * time.Millisecond)
}

func clearScreen() {
 cmd := "clear"
 if os.Getenv("GOOS") == "windows" {
  cmd = "cls"
 }
 c := exec.Command(cmd)
 c.Stdout = os.Stdout
 c.Run()
}

func main() {
 rand.Seed(time.Now().UnixNano())
 grid := newGrid()

 for {
  render(grid)
  grid = step(grid)
 }
}
```
14. Напишите программу, которая вычисляет цифровой корень числа. Цифровой корень — это рекурсивная сумма цифр числа, пока не останется только одна цифра. Например, цифровой корень числа 9875 равен 2, потому что 9+8+7+5=29 → 2+9=11 → 1+1=2.
```
package main

import (
 "fmt"
 "strconv"
)

func digitalRoot(n int) int {
 root := n
 for root >= 10 {
  tmp := 0
  for n > 0 {
   tmp += n % 10
   n /= 10
  }
  root = tmp
  n = root
 }
 return root
}

func main() {
 var numberStr string
 fmt.Print("Введите число: ")
 fmt.Scanln(&numberStr)

 number, _ := strconv.Atoi(numberStr)
 root := digitalRoot(number)

 fmt.Printf("Цифровой корень числа %d равен %d.\n", number, root)
}
```
15. Напишите функцию, которая преобразует арабское число (например, 1994) в римское (например, "MCMXCIV"). Программа должна использовать циклы и условные операторы для создания римской записи.
```
package main

import (
 "fmt"
 "strings"
)

func arabicToRoman(num int) string {
 roman := []string{"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"}
 arabic := []int{1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1}

 var romanNum string
 for i := 0; i < len(roman); i++ {
  for num >= arabic[i] {
   romanNum += roman[i]
   num -= arabic[i]
  }
 }

 return romanNum
}

func main() {
 var num int
 fmt.Print("Введите арабское число: ")
 fmt.Scan(&num)

 roman := arabicToRoman(num)
 fmt.Printf("Римский эквивалент числа %d: %s\n", num, roman)
}
```
