![The-N-Queens-Puzzle](https://github.com/aptx4869-sherry/Practice-leetcode-with-me/assets/63852626/b8be6a81-a3d5-41b7-9b57-eeb86e33e716)

```
// Solution using backtracking
var solveNQueens = function (n) {
    // Base case for n=1, the only solution is a single queen
    if (n === 1) {
        return [["Q"]];
    }

    // Base case for n=2 or n=3, there are no solutions
    if (n === 2 || n === 3) {
        return [];
    }
    // Initialize the board with n rows and n columns, all filled with '.'
    let board = Array.from({ length: n }, () => Array(n).fill('.'));
    // This will store all the possible solutions
    let solutions = [];

    // Helper function to solve the problem using backtracking
    function solve(col, left, upperDiagonal, lowerDiagonal) {

        // If we have placed queens in all rows, add the current board configuration to solutions
        if (col === n) {
            solutions.push(board.map(row => row.join('')));
            return;
        }

        // Iterate through each column in the current row
        for (let row = 0; row < n; row++) {
            // Check if the current column or diagonals are already occupied by another queen
            if (left.has(row) || upperDiagonal.has(row - col) || lowerDiagonal.has(row + col)) {
                continue; // Skip this column as it's not safe to place a queen
            }

            // Mark the current column and diagonals as occupied
            left.add(row);
            upperDiagonal.add(row - col);
            lowerDiagonal.add(row + col);
            // Place the queen on the board
            board[row][col] = 'Q';

            // Recursively solve for the next row
            solve(col + 1, left, upperDiagonal, lowerDiagonal);

            // Backtrack: remove the queen and mark the current column and diagonals as unoccupied
            left.delete(row);
            upperDiagonal.delete(row - col);
            lowerDiagonal.delete(row + col);
            board[row][col] = '.';
        }

        // Return the list of solutions
        return solutions;
    }

    // Start solving from the first row with empty sets for columns and diagonals
    return solve(0, new Set(), new Set(), new Set());
};

```
