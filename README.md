## DATE:- 05/11/2026

## NAME :- PULLA KAVYA

## REG NUM:- 212225240110

# Implement a Sudoku Solver From Scratch
## Steps to solve the Sudoku Puzzle in Python
<ol>
  <li>In this method for solving the sudoku puzzle, first, we assign the size of the 2D matrix to a variable M (M*M).</li>
 <li>Then we assign the utility function (puzzle) to print the grid.</li>
<li>Later it will assign num to the row and col.</li>
<li>If we find the same num in the same row or same column or in the specific 3*3 matrix, ‘false’ will be returned.</li>
<li>Then we will check if we have reached the 8th row and 9th column and return true for stopping further backtracking.</li>
<li>Next, we will check if the column value becomes 9 then we move to the next row and column.</li>
<li>Further now we see if the current position of the grid has a value greater than 0, then we iterate for the next column.</li>
<li>After checking if it is a safe place, we move to the next column and then assign the num in the current (row, col) position of the grid. Later we check for the next possibility with the next column.</li>
<li>As our assumption was wrong, we discard the assigned num and then we go for the next assumption with a different num value</li>
</ol>


## PROGRAM
```

     import random

            # Generate a complete Sudoku board
    def generate_sudoku():
    board = [[0 for _ in range(9)] for _ in range(9)]

    def solve(board):
        for row in range(9):
            for col in range(9):
                if board[row][col] == 0:
                    nums = list(range(1, 10))
                    random.shuffle(nums)

                    for num in nums:
                        if is_valid(board, row, col, num):
                            board[row][col] = num

                            if solve(board):
                                return True

                            board[row][col] = 0

                    return False
        return True

    solve(board)

    # Remove numbers to create a puzzle
    for _ in range(40):
        row = random.randint(0, 8)
        col = random.randint(0, 8)
        board[row][col] = 0

    return board


    # Check whether a number is valid
    def is_valid(board, row, col, num):

    for i in range(9):
        if board[row][i] == num:
            return False

        if board[i][col] == num:
            return False

    start_row = (row // 3) * 3
    start_col = (col // 3) * 3

    for i in range(3):
        for j in range(3):
            if board[start_row + i][start_col + j] == num:
                return False

    return True


    # Sudoku Solver
    def solve_sudoku(board):

    for row in range(9):
        for col in range(9):

            if board[row][col] == 0:

                for num in range(1, 10):

                    if is_valid(board, row, col, num):

                        board[row][col] = num

                        if solve_sudoku(board):
                            return True

                        board[row][col] = 0

                return False

    return True
    Display Sudoku board
    def display(board):
    for row in board:
        print(" ".join(str(num) if num != 0 else "." for num in row))


    # Main Program
    sudoku = generate_sudoku()

    print("Generated Sudoku Puzzle:")
    display(sudoku)

    print("\nSolved Sudoku Puzzle:")

    If solve_sudoku(sudoku):
    display(sudoku)
    else:
    print("No solution exists.")




## OUTPUT

<img width="366" height="435" alt="image" src="https://github.com/user-attachments/assets/7d5c3e23-dbde-455e-8525-a5318824903e" />

## RESULT
Thus, a Sudoku solver using the backtracking algorithm is implemented for the given Sudoku puzzle.
