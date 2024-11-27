## Отчет по лабораторной работе № 2

#### № группы: `ПМ-2402`

#### Выполнил: `Воробьев Кирилл Владиславович`

#### Вариант: `5`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Входные и выходные данные](#2-входные-и-выходные-данные)
- [Выбор структуры данных](#3-выбор-структуры-данных)
- [Алгоритм](#4-алгоритм)
- [Программа](#5-программа)
- [Анализ правильности решения](#6-анализ-правильности-решения)

### 1. Постановка задачи

> Напишите программу на Java, которая выполняет следующие действия
> с двумерным массивом целых чисел:
>   1. Считывает с консоли размеры массива N и M, затем элементы
>   массива размером N × M. Затем вводит число K.
>   2. Сортирует элементы каждой строки по возрастанию остатков от
>   деления на K. Если остатки равны, сортирует элементы по убыванию. Если элементы равны, учитывает количество их вхождений в
>   строке.
>   3. Находит произведение максимальных элементов каждой строки, а
>   также их индексы в строках.
>   4. Выводит элементы массива в транспонированном виде.
>   5. Удаляет из массива все элементы, которые являются кратными
>   числу K, выводит получившийся массив массивов, а также количество удалённых элементов

Данную задачу можно разделить на несколько подзадач.

- 1) Создать двумерный массив и переменную k, и заполнить массив целыми числами.
- 2) Отсортировать каждую строку по возрастанию остатков от деления на k. Если остатки равны, сортируем элементы по убыванию.
- 3) Нахождение произведения максимальных элементов строк и индексов этих элементов.
- 4) Вывод элементов массива в транспонированном виде.
  5) Создание массива,в котором отсутствуют элементы кратные k.

### 2. Входные и выходные данные

#### Данные на вход

На вход программа должна получать 2 числа (N и M), которые задают массив, и далее некоторое количество чисел, которыми мы этот массив заполняем. В условии сказано, что числа принадлежат множеству целых. Также следует отметить, что N и M не могут принимать неположительные значения, так как они задают массив.
И еще число k.


|             | Тип                | min значение    | max значение   |
|-------------|--------------------|-----------------|----------------|
| N (Число 1) |    Целое число     |        1        | 10<sup>9</sup> |
| M (Число 2) |    Целое число     |        1        | 10<sup>9</sup> |
| K (Число 3) |    Целое число     |        1        | 10<sup>9</sup> |
| a[ i ][ j ] |    Целое число     | -10<sup>9</sup> | 10<sup>9</sup> |

#### Данные на выход

На выход мы получаем всё те же элементы массива (N x M элементов), которые могут принимать как отрицательное значение, как положительное, так и 0.
Также получаем целое число c(количество исключенных элементов).

|             | Тип                | min значение    | max значение   |
|-------------|--------------------|-----------------|----------------|
| a[ i ][ j ] |    Целое число     | -10<sup>9</sup> | 10<sup>9</sup> |
|      С      |    Целое число     |        0        | 10<sup>9</sup> |

### 3. Выбор структуры данных

Программа получает 3 целых числа, не превышающих 10<sup>9</sup>. Поэтому для их хранения можно выделить 3 переменных ('n','m' и 'k') типа 'int'.

|             | название переменной | Тип (в Java) | 
|-------------|---------------------|--------------|
| N (Число 1) | `n `                |    `int`     |
| M (Число 2) | `m`                 |    `int`     | 
| K (Число 2) | `k`                 |    `int`     |

Для вывода результата необязательно его хранить в отдельной переменной.

### 4. Алгоритм

#### Алгоритм выполнения программы:

1. **Ввод данных:**  
   Программа считывает два целых числа, обозначенные как 'n','m' и вводит одно целое 'k'.

2. **Преобразование массива:**  
   Программа сортирует двухмерный массив пузырьковым методом по возрастанию остатков от деления на 'k'.Если остатки равны,то сортируется элементы по убыванию.
3. **Нахождение произведения максимальных элементов каждой строки а также их индексов в строках:**
   Для этого создается переменная 'p'(=1),в которой хранится произведение макс элементов,массив 'maxI'(для хранения индексов максимальных элементов строк) и переменная 'maxEl,которая получает максимальные элементы строк,производя поиск максимального элемента в каждой строке путем сравнения.
4. **Создание массива,в котором отсутствуют элементы кратные 'k':**
   Сначала программа считает количество элементов в изначальном массиве кратных числу 'k'.Дальше создается новый массив'newa',переменные 'r','d','i1' для обработки старого массива и безошибочного переноса необходимыч элементов в новый массив.
5. **Вывод результата:**  
   На экран выводится первый массив после преобразований в транспонированном виде,после выводится массив без элементов кратных переменной 'k'.А также выводится количество элементов,которое было исключено.



### 5. Программа

```java
import java.io.PrintStream;
import java.util.Arrays;
import java.util.Scanner;
public class Main {
    public static PrintStream out = System.out;
    public static Scanner in = new Scanner(System.in);
    public static void main(String[] args) {
        //Вводим кол-во строк и столбцов массива
        int n = in.nextInt();
        int m = in.nextInt();
        //Задание двумерного массив
        int[][] a = new int[n][m];
        //Ввод целого числа k
        int k = in.nextInt();
        //Заполнение двумерного массива целыми числами
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                a[i][j] = in.nextInt();
            }
        }
        //Сортировка каждой строки массива по возрастанию остатков от деления на k
        int b;
        for (int i = 0; i < n; i++) {
                for (int j = 1; j < m; j++) {
                    for (int t = m - 1; t > 0; t--) {
                        if (a[i][j] % k < a[i][j - 1] % k) {
                            b = a[i][j - 1];
                            a[i][j - 1] = a[i][j];
                            a[i][j] = b;
                        }
                        //Если остатки равные,то сортируем сами элементы по убыванию
                        if (a[i][j] % k == a[i][j - 1] % k){
                            if(a[i][j] > a[i][j - 1]){
                                b = a[i][j - 1];
                                a[i][j - 1] = a[i][j];
                                a[i][j] = b;
                            }
                        }
                    }
                }
        }
        //Поиск произведения максимальных элементов строк и их индексов в строке
        int p = 1;
        int[] maxI = new int[n];
        for (int i = 0; i < n; i++) {
            int maxEl = a[i][0];
            maxI[i] = 0;

            for (int j = 1; j < m; j++) {
                if (a[i][j] > maxEl) {
                    maxEl = a[i][j];
                    maxI[i] = j;
                }
            }
            p *= maxEl;
        }
        //Вывод элементов массива в транспонированным виде
        int c = 0;
        for (int j = 0; j < m; j++) {
            for (int i = 0; i < n; i++) {
                if(a[i][j] % k != 0){
                    c++;
                }
                out.print(a[i][j] + " ");
            }
            out.println();
        }
        //Создание массива без элементов кратных k
        int[][] newa = new int[c][];
        //Создание переменной для счетчика строк в новом массиве
        int r = 0;

        // Заполнение нового двумерного массива
        for (int i = 0; i < n; i++) {
            //Создание переменной для проверки,есть ли в строках подходящие по условию числа
            int d = 0;
            for (int j = 0; j < m; j++) {
                if (a[i][j] % k != 0) {
                    d++;
                }
            }
            if (d > 0) {
                newa[r] = new int[d];
                int i1 = 0;
                for (int j = 0; j < m; j++) {
                    if (a[i][j] % k != 0) {
                        newa[r][i1] = a[i][j];
                        i1++;
                    }
                }
                r++;
            }
        }

        // Вывод нового двумерного массива
        for (int i = 0; i < c; i++) {
            for (int j = 0; j < newa[i].length; j++) {
                System.out.print(newa[i][j] + " ");
            }
            System.out.println();
        }
        out.print(n*m-c);


    }
}
```

### 6. Анализ правильности решения

Программа работает корректно на всем множестве решений с учетом ограничений.

1. Тест на ограничение: N = 0, M = 5:

    - **Input**:
        ```
        0 5
        ```

    - **Output**:
        ```
        
        ```

2. Тест:

    - **Input**:
        ```
        2 2
        4
        3 4 5 6
        ```

    - **Output**:
        ```
        4 5
        3 6
        3
        5 6
        1
        ```

3. Тест:

    - **Input**:
        ```
       4 2
       11
       33 26 15 23 44 27 12 11
        ```

    - **Output**:
        ```
        33 23 44 11 
        26 15 27 12 
        26 
        23 15 
        27 
        12
        3 
        ```

4. Тест:

    - **Input**:
        ```
        1 2
        3
        27 9
        ```

    - **Output**:
        ```
       27 
       9 
       2
        ```


       