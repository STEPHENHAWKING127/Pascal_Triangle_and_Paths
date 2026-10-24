# Reflection


# --------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                         "
  "                                                                                                                         "
  "                                                          MEMBERS                                                        "
  "                                                                                                                         "
  "                                                                                                                         "
# ---------------------------------------------------------------------------------------------------------------------------

# --------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                         "
  "                                                                                                                         "
  "        1- ANON NDA GUY SIMON STEPHANE                                                                                   "
  "        2- N'TCHA TAKOUASSEMA Gael Josaphat                                                                              "
  "        3- RAZAN SALAH MOHAMMED SALIH MANSOUR                                                                            "
  "        4- FATIM SECK
  "        5-KOUMBA DIENG                                                                                                   "
  "                                                                                                                         "
  "                                                                                                                         "
# ---------------------------------------------------------------------------------------------------------------------------
## Who did what

| Member | Work |

| Name 5  Task 1: `pascal_row(n)` |
| Name 4  Task 2: printing rows 0 to 7 and checking `sum == 2 ** n` |
| Name 3  Task 3: `grid_paths(rows, cols)` |
| Name 1 and 2  Task 4: `grid_paths_blocked(rows, cols, blocked)` |
| Name 1 and 2 *Think* question, *Extra* triangle, `README.md` |



# --------------------------------------------------------------------------------------------------------------------------- 
  "                                                                                                                         "
  "                                                                                                                         "
  "                            # bug we had, and how we fixed it                                                       "
  "                                                                                                                         "
  "                                                                                                                         "
# ---------------------------------------------------------------------------------------------------------------------------


**The bug.** Our first version of `grid_paths_blocked` copied `grid_paths`: it filled the first row
and the first column with 1, then set the blocked cells to 0. This works for the example
`grid_paths_blocked(2, 2, [(1, 1)])` (answer 2), so at first we did not see the bug.
It breaks when a blocked cell is in the first row or the first column. With `blocked = [(0, 1)]`:

```
wrong table      correct table
1 0 1            1 0 0
1 1 2            1 1 1
1 2 4            1 2 3
```

The cell `(0, 2)` still had 1 path, but you can only reach it by going through `(0, 1)`, which is blocked.
The wrong version returned 4 instead of 3.

**The fix.** We stopped filling the first row and column with 1. Now only the start `(0, 0)` gets 1, and
every other cell adds the paths from above (if `i > 0`) and from the left (if `j > 0`).
A blocked cell in the first row now gives 0 to all the cells after it.
We checked that `grid_paths_blocked(2, 2, [(0, 1)])` gives 3, and that with no blocked cells
`grid_paths_blocked` gives the same answers as `grid_paths`.

**Second bug: mapping the grid to Pascal's triangle**

The difficulty was understanding how the values in the grid correspond to Pascal's triangle. To solve it, we translated the grid formula:

`ways[i][j] = ways[i-1][j] + ways[i][j-1]`

into the Pascal's triangle formula:

`T[n][k] = T[n-1][k-1] + T[n-1][k]`

using the change of variables `n = i + j` and `k = j`. Therefore, `ways[i][j] = T[i+j][j] = C(i+j, j)`.