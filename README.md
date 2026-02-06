# Tic Tac Toe Game

"""
A simple command-line Tic Tac Toe game for two players.
"""

def print_board(board):
    """Print the current board state."""
    for row in board:
        print(" | ".join(row))
        print("---------")  # Print separator


def check_winner(board):
    """Check the board for a winner."""
    # Check rows, columns, and diagonals
    for i in range(3):
        if board[i][0] == board[i][1] == board[i][2] != ' ':  # Check rows
            return board[i][0]
        if board[0][i] == board[1][i] == board[2][i] != ' ':  # Check columns
            return board[0][i]
    if board[0][0] == board[1][1] == board[2][2] != ' ':  # Check diagonal
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != ' ':  # Check reverse diagonal
        return board[0][2]
    return None  # No winner yet


def is_board_full(board):
    """Check if the board is full."""
    return all(cell != ' ' for row in board for cell in row)


def play_game():
    """Main function to play the game."""
    board = [[' ' for _ in range(3)] for _ in range(3)]  # Initialize a 3x3 board
    current_player = 'X'  # X always goes first

    while True:
        print_board(board)  # Print current board state
        print(f"Player {current_player}, enter your move (row and column): ")
        try:
            row, col = map(int, input().split())
            if board[row][col] != ' ':
                print("This cell is already taken. Try again.")
                continue  # Skip to next iteration
            board[row][col] = current_player  # Make the move
        except (ValueError, IndexError):
            print("Invalid input. Please enter row and column as two numbers from 0 to 2.")
            continue

        winner = check_winner(board)  # Check for a winner
        if winner:
            print_board(board)  # Print final board state
            print(f"Player {winner} wins!")
            break
        if is_board_full(board):  # Check for a draw
            print_board(board)  # Print final board state
            print("It's a draw!")
            break

        current_player = 'O' if current_player == 'X' else 'X'  # Switch players


if __name__ == '__main__':
    play_game()  # Start the game
