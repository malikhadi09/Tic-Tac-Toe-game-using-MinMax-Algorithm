# Tic-Tac-Toe-game-using-MinMax-Algorithm

# Explanation of the code:

import sys

def game_end(game_board):
    
    rows = [game_board[row] for row in range(3)]
    cols = [[game_board[row][col] for row in range(3)] for col in range(3)]
    diags = [[game_board[i][i] for i in range(3)], [game_board[i][2-i] for i in range(3)]]

    for line in rows + cols + diags:
        if line[0] != " " and all(cell == line[0] for cell in line):
            return True

    
    return all(cell != " " for row in game_board for cell in row)

This is a Python function called game_end that takes a 2D list game_board as input, which represents a tic tac toe game board. The function game_end is defined, which takes a 2D list game_board as input. In the block of the function there are three lists rows, cols, and diags. The rows list is created by iterating over the rows of the game_board list, and the cols list is created by iterating over the columns of the game_board list. The diags list contains two lists, one representing the diagonal from top-left to bottom-right, and the other representing the diagonal from top-right to bottom-left. The code iterates over each line in the rows, cols, and diags lists. It checks if the first cell in the line is not empty (" ") and if all cells in the line have the same value. If this condition is met, the function returns True, indicating that the game has ended with a winner. If no winner has been found in the previous step, this line of code checks if all cells in the game_board list have been filled means the cells are not empty. If all cells have been filled, the function returns True, indicating that the game has ended in a tie. If not all cells have been filled, the function returns False, indicating that the game is still in progress.
def actions(game_board):
    for player in ["X", "O"]:
      
        for row in range(3):
            if all(cell == player for cell in game_board[row]):
                return 1 if player == "X" else -1
       
        for col in range(3):
            if all(game_board[row][col] == player for row in range(3)):
                return 1 if player == "X" else -1
     
        if all(game_board[i][i] == player for i in range(3)):
            return 1 if player == "X" else -1
        if all(game_board[i][2-i] == player for i in range(3)):
            return 1 if player == "X" else -1
 
    return 0

This function called “actions” takes in a game board as input, which is represented as a list of lists of strings. Each string in the game board represents a cell, and is either "X", "O", or " " (empty).
The purpose of this function is to check if the game has ended and who has won and return a score accordingly. The function starts by looping through the two possible players in the game, "X" and "O". The function then checks if the current player has won horizontally by checking if all cells in a row contain the current player's symbol. If so, the function returns 1 if the current player is "X", indicating a win for "X", and -1 otherwise, indicating a win for "O". The function then checks if the current player has won vertically by checking if all cells in a column contain the current player's symbol. If so, the function returns 1 or -1 as before. Finally, the function checks if the current player has won diagonally. The first condition checks the diagonal from top-left to bottom-right, and the second condition checks the diagonal from top-right to bottom-left. If none of the previous conditions have been met, the function returns 0, indicating that the game has not ended yet or that it has ended in a draw.
def print_board(game_board):
    for row in game_board:
        row_str = ""
        for cell in row:
            row_str += " " + cell + " |"
        print(row_str[:-1])
        print("__________")

This function called “print_board” takes a single parameter game_board representing the current state of the Tic Tac Toe game board. When the function is called with a 3x3 Tic Tac Toe game board, it will output a grid of cells, separated by vertical bars and with horizontal lines to indicate the separation of rows.
def max_value(game_board):
    if game_end(game_board):
        return actions(game_board)
    maxx = -sys.maxsize
    for row in range(3):
        for col in range(3):
            if game_board[row][col] == " ":
                game_board[row][col] = "X"
                maxx = max( maxx, min_value(game_board))
                game_board[row][col] = " "
    return maxx

This function called the “min_value” takes a game_board argument. If the game has ended, either player has won or the board is full, the function returns the result of the actions function called with the game_board argument.
 Initializes the variable minn with the maximum integer value supported by the system.
Afterwards there is a loop that Iterates through every empty cell on the board and tries to make a move by placing an "O" at that cell. It then calls the max_value function with the updated board and updates the minn variable with the minimum value returned by max_value. It then restores the board by removing the "O" from the cell. This essentially simulates the game for every possible move by the opponent. In the last it returns the minimum value that the opponent can achieve after the current player makes their move.
def minmax(game_board):
    bestvalue = float('-inf')
    bestmove = (-1, -1)
    
    for row in range(3):
        for col in range(3):
            if game_board[row][col] == " ":
                game_board[row][col] = "X"
                value_move = min_value(game_board)
                game_board[row][col] = " "
                if value_move> bestvalue:
                    bestvalue = value_move
                    bestmove = (row, col)
    return bestmove


This code implements the Minimax algorithm to determine the best move for the computer player in a Tic Tac Toe game. The algorithm works by exploring all possible future game states for the current board configuration, assigning a score to each possible move based on the assumption that the opponent will always play optimally, and choosing the move with the highest score. The algorithm recursively alternates between two functions, max_value and min_value, which simulate the player's turn and the opponent's turn, respectively. minmax iterates through each empty cell on the board, simulates the computer player making a move, and calls min_value to evaluate the expected outcome of the game. The bestmove variable is updated with the move that results in the highest score, which is then returned.
def main():
    
    print("WELCOME TO :")
    print("\n")
    print("TIC TAC TOE GAME :")
    print("___________________")
    print("\n")
    player_no_1 = input("Please, enter the first player name: ")
    player_no_2 = input("Please, enter the second player name: ")
    game_board = []
    for i in range(3):
        row = []
        for j in range(3):
            row.append(" ")
        game_board.append(row)
    total_players = { player_no_1: "X",  player_no_2: "O"}
   
    current_player =  player_no_1

    while not game_end(game_board):
        print_board(game_board)
        print("\n")
        print("hey,")
        print("Total Rows => 0 ,1, 2")
        print("Total Columns => 0, 1 ,2")
        row = int(input("please "f"{current_player}, enter your move from row from mentioned above indexes : "))
        col = int(input("please "f"{current_player}, enter your move from column from mentioned above indexes : "))
        
        if game_board[row][col] == " ":
            game_board[row][col] = total_players[current_player]
            if current_player == player_no_1:
                current_player = player_no_2
            else:
                current_player = player_no_1
        else:
            print("Sorry you have done an invalid move, Try again!!!!!!!!!")
            continue

    print_board(game_board)

    result = actions(game_board)
    if result == 0:
        print("it is a draw match.")
    elif result == 1:
        print("Congratsss, "f"{ player_no_1} you have won the game!!!!")
    else:
        print("Congratsss, "f"{ player_no_2}you have won the game!!!!")

This code is the main function that runs a game of Tic Tac Toe. It starts by welcoming the players and creating an empty game board. The players are prompted to enter their names and assigned X or O as their respective symbols. The game loop starts, where each player takes a turn to enter their move by selecting a row and column index on the game board. If the chosen cell is empty, it is filled with the player's symbol and the turn is passed to the next player. If the cell is already occupied, the player is prompted to try again. The game continues until either the board is full or one of the players has won. Once the game ends, the final board state is displayed, and the winner or draw is announced. The outcome of the game is determined by the actions function, which returns a value of 1 if player 1 wins, -1 if player 2 wins, or 0 if it's a draw.
if __name__ == "__main__":
    main()

And in the last we called main function.

# OUTPUT:
![image](https://user-images.githubusercontent.com/92660593/227267121-56a323ed-f367-44cc-aa56-140691fec29f.png)
![image](https://user-images.githubusercontent.com/92660593/227267163-7f13d6e0-ce33-4555-b0af-73faa7235e91.png)

