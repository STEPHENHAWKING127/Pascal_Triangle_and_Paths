
# --------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                         "
  "                                                                                                                         "
  "              -------------------------- GROUP 8 -------------------------------                                         "
  "                                                                                                                         "
  "                                                                                                                         "
# ---------------------------------------------------------------------------------------------------------------------------


# --------------------------------------------------------------------------------------------------------------------------- 
                       ------------------------ PASCAL TRIANGLES -------------------------------   
# --------------------------------------------------------------------------------------------------------------------------- 


# Project 8: Pascal's Triangle and Paths

## What the program does

The code is in `project.py` (run it with `python project.py`) and in the notebook
`Project_08_Pascal_s_Triangle_and_Paths.ipynb`. Both contain the same functions.


# --------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                         "
  "                                                                                                                         "
  "                                     Function : What it does                                                             "
  "                                                                                                                         "
  "                                                                                                                         "
# ---------------------------------------------------------------------------------------------------------------------------

 `pascal_row(n)`: Returns row `n` of Pascal's triangle as a list. Each row is made from the row before: it starts and ends with 1, and each number inside is the sum of the two numbers above it. 

 `grid_paths(rows, cols)` : Returns the number of paths from `(0, 0)` to `(rows, cols)` going only right or down. It fills a list of lists `ways` with `ways[i][j] = ways[i-1][j] + ways[i][j-1]`, with 1 in the first row and the first column. 

 `grid_paths_blocked(rows, cols, blocked)` : Same as `grid_paths`, but a blocked cell has 0 paths. A cell gets the paths from the cell above and from the cell on the left (when they exist).




 `count_odd(row)` :Counts the odd numbers in a row (for the *Think* question).


 `print_odd_triangle(n_rows)` :  Prints the triangle with `*` for odd numbers and a space for even numbers.

# ------------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                             "
  "                                                                                                                             "
  " Task 2 prints rows 0 to 7, then checks that `sum(pascal_row(n)) == 2 ** n` for `n` from 0 to 10. All 11 checks print `True`
  "                                                                                                                             "
  "                                                                                                                             "
# -------------------------------------------------------------------------------------------------------------------------------   

# ------------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                             "
  "                                                                                                                             "
  "                                                 ## Example results
  "                                                                                                                             "
  "                                                                                                                             "
# -------------------------------------------------------------------------------------------------------------------------------  



** ------------Example 1---------------------
 Row 5 of Pascal's triangle**

```
>>> pascal_row(5)
[1, 5, 10, 10, 5, 1]
```

**------------Example 2------------------------
 Paths in a 3 x 3 grid**

```
>>> grid_paths(3, 3)
20
```

**--------------Example 3-----------------------

4 x 4 grid with `blocked = [(1, 2), (2, 1)]`**

```
>>> grid_paths_blocked(4, 4, [(1, 2), (2, 1)])
10
```
The `ways` table (0 = blocked cell or a cell that no path can reach):

```
1 1 1 1 1
1 2 0 1 2
1 0 0 1 3
1 1 1 2 5
1 2 3 5 10
```

Without blocked cells the answer would be `grid_paths(4, 4) = 70`.

**--------------End Example----------------------

# ------------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                             "
  "                                                                                                                             "
  "                                                 ## Think and explain: odd numbers in each row
  "                                                                                                                             "
  "                                                                                                                             "
# -------------------------------------------------------------------------------------------------------------------------------  



Number of odd numbers in rows 0 to 15:

```
[1, 2, 2, 4, 2, 4, 4, 8, 2, 4, 4, 8, 4, 8, 8, 16]
```

What we see:

- Every count is a power of 2 (1, 2, 4, 8 or 16).
- In rows 1, 3, 7 and 15 (one less than a power of 2), every number is odd, so the count is `n + 1`.
- The list repeats and doubles: rows 8 to 15 have twice the counts of rows 0 to 7
  (`2, 4, 4, 8, 4, 8, 8, 16` = 2 x `1, 2, 2, 4, 2, 4, 4, 8`). In the same way, rows 4 to 7 are twice rows 0 to 3.
- Rule: write `n` in binary. If it has `b` ones, row `n` has `2 ** b` odd numbers.
  For example `13 = 1101` has three 1s, so row 13 has `2 ** 3 = 8` odd numbers.

  We have the division 16 in the binary system:
 
| Étape | Division | Quotient | Reste |
|-------|----------|----------|-------|
| 1     | 16 ÷ 2   | 8        | 0     |
| 2     | 8 ÷ 2    | 4        | 0     |
| 3     | 4 ÷ 2    | 2        | 0     |
| 4     | 2 ÷ 2    | 1        | 0     |
| 5     | 1 ÷ 2    | 0        | 1     |

**So WE HAVE ** `16 = 10000` in binary has only one 1, so we guess `2 ** 1 = 2`.
**Check:** `count_odd(pascal_row(16))` gives `2`. Row 16 is `1, 16, 120, 560, ..., 16, 1`, and only the two 1s at the ends are odd.

# --------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                         "
  "                                                                                                                         "
  "                                     Extra: odd numbers as stars                                                         "
  "                                                                                                                         "
  "                                                                                                                         "
# ---------------------------------------------------------------------------------------------------------------------------

## Extra: odd numbers as stars

```
               *
              * *
             *   *
            * * * *
           *       *
          * *     * *
         *   *   *   *
        * * * * * * * *
       *               *
      * *             * *
     *   *           *   *
    * * * *         * * * *
   *       *       *       *
  * *     * *     * *     * *
 *   *   *   *   *   *   *   *
* * * * * * * * * * * * * * * *
```
The shape is the **Sierpinski triangle**: a big triangle made of three smaller copies of itself
with an empty triangle in the middle, and each copy is made the same way.
It also explains the doubling in the *Think* question: rows 8 to 15 contain two copies of rows 0 to 7.
