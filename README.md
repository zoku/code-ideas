# Code Ideas
## Tools
### Library Index
Make a collection of your favourite books.
- Sort them by author, series, IBAN etc.
- Group and sort by meta data (e.g. order of books in a series)

## Games
### Guess a number
- The program generates a number between 1 and 10
- User inputs a number
- The program tells the user if their number is greater, smaller or equal to the generated number
- If the user's number equals the programs number, the game is over

Extra 1: When the user guesses correctly, the program tells them how many tries they needed to do so

Extra 2: When the user guesses correctly, they can start a new round

### Tic Tac Toe
- Render a Tic Tac Toe board
- Ask players to enter coordinates to place their game piece
- Check if placement is valid
- Check if anyone has won

```
  |---|---|---|
A | X |   | O |
  |---|---|---|
B |   | O |   |
  |---|---|---|
C | O | X |   |
  |---|---|---|
    1   2   3
```

<details>
  <summary>Hint 1</summary>
  
  Use a single list to represent the game board.
</details>

<details>
  <summary>Hint 2</summary>
  
  Use two nested for-loops to render the game board (x- and y-coordinates).
</details>

<details>
  <summary>Hint 3</summary>

  You can map the index of a list to 2-dimensional coordinates by splitting it into four components:

  - Width ($w$)
  - Height ($h$)
  - X-coordinate ($x$)
  - Y-coordinate ($y$)

  So the calculation of a cell is:

  $f(x,y) = y \times w + x$
</details>

<details>
  <summary>Solution</summary>
  
  The gameboard has a size of 3x3 cells so the size of the list / array is $x \times y = 9$.
  
  `gameboard = ["", "", "", "", "", "", "", "", ""]`

  To represent a game piece, set the appropriate index to "O" or "X". The list index of $x$- and $y$-coordinates can be calculated with $y \times W + x$ where $W$ is the width of the game board.
  
  `gameboard[y * 3 + x] = "O"`
  
  Use a function with the signature `putPiece(type: string, x: int, y: int): boolean` to do this.

  Inside this function, check if cell is already occupied or invalid. Return false for errors and show a message to the player.
  
  ```
  function putPiece(type: string, x: int, y: int): boolean {
    if (x < 0 || x > 2) return false
    if (gameboard[y * 3 + x] != "") return false
    gameboard[y * 3 + x] = "O"
    return true
  }
  ```
  
  Render the game board with two nested for-loops.
  
  ```
  for (y = 0; y < 3; y++) {
    for (x = 0; x < 3; x++) {
      write(gameboard[y * 3 + x]) // write current x-coordinate
    }
    write("\n") // write a newline before y-coordinate change
  }
  ```

  Use a function to check neighbors of a game piece.
  
  ```
  function checkWin(player: string): boolean { // Takes "O" or "X" and returns true if player has won
    // Check horizontal lines
    for (x = 0; x < 3; x++) {
      if (gameboard[x] == player && gameboard[3 + x] == player && gameboard[6 + x] == player) return true
    }

    // Check vertical lines
    for (y = 0; y < 3; y++) {
      if (gameboard[y * 3] == player && gameboard[y * 3 + 1] == player && gameboard[y * 3 + 2] == player) return true
    }

    // Check diagonals
    if (gameboard[0] == player && gameboard[4] == player && gameboard[8] == player) return true
    if (gameboard[2] == player && gameboard[4] == player && gameboard[6] == player) return true
  }
  ```
</details>

<details>
  <summary>Additional ideas</summary>
  
  - Render the game board with [box-drawing characters](https://www.utf8icons.com/subsets/box-drawing)
  - Make the game board bigger
  - Add more pieces in one line needed to win (e.g. four in a row)
  - Highlight the winning row with color or formatting
  - Add a high-score list
</details>
