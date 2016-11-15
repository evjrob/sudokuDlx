# sudokuDlx
sudokuDLX is a go package for solving sudoku puzzles using Donald Knuth's dancing links agorithm. It accepts sudokus of varying dimensions in the form of a square 2D int slice along with the x and y dimesnions of a single block in the provied sudoku.

A sudoku can be solved using the method: Solve(puzzle [][]int, blockXDim, blockYDim int) ([][]int , bool) which will return the solution and a boolean indicator of success.

## examples
The dashes, vertical lines, and plus cells below are not part of the int slice, but included for the sake of visualizaton.

To solve a standard sudoku stored in a variable named puzzle:
| | | || | | || | | |
|-|-|-|-|-|-|-|-|-|-|-|
|3| | |\|| |8| |\|| | | |
| | | |\||7| | |\|| | |5|
|1| | |\|| | | |\|| | | |
|-|-|-|+|-|-|-|+|-|-|-|
| | | |\|| | | |\||3|6| |
| | |2|\|| | |4|\|| | | |
| |7| |\|| | | |\|| | | |
|-|-|-|+|-|-|-|+|-|-|-|
| | | |\|| |6| |\||1|3| |
| |4|5|\||2| | |\|| | | |
| | | |\|| | | |\||8| |

```
solution, success := sudokuDlx.Solve(puzzle, 3, 3)
```

Which will return success = true with the solution:
| | | || | | || | | |
|-|-|-|-|-|-|-|-|-|-|-|
|3|5|4|\||1|8|6|\||9|2|7|
|2|9|8|\||7|4|3|\||6|1|5|
|1|6|7|\||9|5|2|\||4|8|3|
|-|-|-|+|-|-|-|+|-|-|-|
|9|3|2|\||6|1|4|\||5|7|8|
|4|8|1|\||5|2|7|\||3|6|9|
|5|7|6|\||3|9|8|\||2|4|1|
|-|-|-|+|-|-|-|+|-|-|-|
|7|2|9|\||8|6|5|\||1|3|4|
|8|4|5|\||2|3|1|\||7|9|6|

To solve a non standard dimension sudoku like this 7x2 puzzle:
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|  | 1|  |  | 2|10| 7|\||  |  |  |  |  |  |11|
|12|  |  |  |  |  | 6|\||10|  |  | 4| 2|  |  |
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
| 4|10|  |12|13|  |  |\||  |14|11|  | 1|  |  |
|11| 6|  |  | 1| 7|14|\||  |12|  |  |  |  |  |
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
|  |  | 6|  |  |  | 4|\||  |  |  |  |  |  | 3|
|  | 3|10|13| 8| 1| 2|\||  | 9|  |  |  | 6|  |
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
|  | 7|  |10| 4|  |13|\||  | 5|  |11| 8|12|  |
|  |11| 8|14|  | 9|  |\|| 3|  | 2|10|  | 4|  |
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
|  |14|  |  |  |11|  |\|| 7| 1| 6| 2|10|13|  |
| 6|  |  |  |  |  |  |\|| 5|  |  |  |12|  |  |
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
|  |  |  |  |  |14|  |\||13| 8|12|  |  |11| 5|
|  |  | 5|  | 7|12|  |\||  |  | 9| 1|  |14| 6|
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
|  |  |13| 7|  |  |12|\|| 6|  |  |  |  |  | 2|
|14|  |  |  |  |  |  |\||12| 3| 7|  |  | 8|  |

```
solution, success := sudokuDlx.Solve(puzzle, 3, 3)
```

Which will return success = true with the solution:


|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
|13| 1|14| 4| 2|10| 7|\|| 8| 6| 3|12| 5| 9|11|
|12| 5|11| 9| 3| 8| 6|\||10|13|14| 4| 2| 7| 1|
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
| 4|10| 3|12|13| 2| 8|\|| 9|14|11| 6| 1| 5| 7|
|11| 6| 9| 5| 1| 7|14|\|| 4|12|10| 3|13| 2| 8|
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
| 9|12| 6|11|14| 5| 4|\|| 1| 2|13| 8| 8|10| 3|
| 7| 3|10|13| 8| 1| 2|\||11| 9| 4| 5|14| 6|12|
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
| 3| 7| 2|10| 4| 6|13|\||14| 5| 1|11| 8|12| 9|
| 1|11| 8|14|12| 9| 5|\|| 3| 7| 2|10| 6| 4|13|
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
| 5|14|12| 8| 9|11| 3|\|| 7| 1| 6| 2|10|13| 4|
| 6| 4| 7| 2|10|13| 1|\|| 5|11| 8| 9|12| 3|14|
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
| 2| 9| 4| 1| 6|14|10|\||13| 8|12| 7| 3|11| 5|
| 8|13| 5| 3| 7|12|11|\|| 2|10| 9| 1| 4|14| 6|
|--|--|--|--|--|--|--| +|--|--|--|--|--|--|--|
|10| 8|13| 7|11| 3|12|\|| 6| 4| 5|14| 9| 1| 2|
|14| 2| 1| 6| 5| 4| 9|\||12| 3| 7|13|11| 8|10|
