import random

# Constants
PLAYER = 'X'
AI = 'O'
EMPTY = ' '
SIZE = 3

def print_board(board):
    for row in board:
        print('|'.join(row))
        print('-' * SIZE)

def check_winner(board):
    # Check rows, columns, and diagonals for a win
    for i in range(SIZE):
        if board[i][0] == board[i][1] == board[i][2] != EMPTY:
            return board[i][0]
        if board[0][i] == board[1][i] == board[2][i] != EMPTY:
            return board[0][i]
    
    if board[0][0] == board[1][1] == board[2][2] != EMPTY:
        return board[0][0]
    
    if board[0][2] == board[1][1] == board[2][0] != EMPTY:
        return board[0][2]
    
    return None

def check_draw(board):
    return all(cell != EMPTY for row in board for cell in row)

def minimax(board, depth, is_maximizing):
    winner = check_winner(board)
    if winner == AI:
        return 1
    if winner == PLAYER:
        return -1
    if check_draw(board):
        return 0
    
    if is_maximizing:
        best_score = float('-inf')
        for i in range(SIZE):
            for j in range(SIZE):
                if board[i][j] == EMPTY:
                    board[i][j] = AI
                    score = minimax(board, depth + 1, False)
                    board[i][j] = EMPTY
                    best_score = max(score, best_score)
        return best_score
    else:
        best_score = float('inf')
        for i in range(SIZE):
            for j in range(SIZE):
                if board[i][j] == EMPTY:
                    board[i][j] = PLAYER
                    score = minimax(board, depth + 1, True)
                    board[i][j] = EMPTY
                    best_score = min(score, best_score)
        return best_score

def ai_move(board):
    best_score = float('-inf')
    move = (-1, -1)

    for i in range(SIZE):
        for j in range(SIZE):
            if board[i][j] == EMPTY:
                board[i][j] = AI
                score = minimax(board, 0, False)
                board[i][j] = EMPTY
                if score > best_score:
                    best_score = score
                    move = (i, j)

    board[move[0]][move[1]] = AI

def player_move(board):
    while True:
        try:
            move = int(input("Enter your move (1-9): ")) - 1
            row = move // SIZE
            col = move % SIZE
            if board[row][col] == EMPTY:
                board[row][col] = PLAYER
                break
            else:
                print("Invalid move! Try again.")
        except (ValueError, IndexError):
            print("Invalid input! Please enter a number between 1 and 9.")

def play_game():
    board = [[EMPTY for _ in range(SIZE)] for _ in range(SIZE)]
    print("Welcome to Tic-Tac-Toe!")
    print("You are 'X' and the AI is 'O'.")
    print_board(board)

    while True:
        player_move(board)
        print_board(board)
        if check_winner(board):
            print("Congratulations! You win!")
            break
        if check_draw(board):
            print("It's a draw!")
            break
        
        ai_move(board)
        print_board(board)
        if check_winner(board):
            print("AI wins! Better luck next time!")
            break
        if check_draw(board):
            print("It's a draw!")
            break

if __name__ == "__main__":
    play_game()
