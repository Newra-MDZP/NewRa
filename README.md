def print_board(board):
    print("-------------")
    for row in board:
        print("|", end=" ")
        for cell in row:
            print(cell, "|", end=" ")
        print()
        print("-------------")

def check_win(board, player):
    # Periksa baris
    for row in board:
        if all(cell == player for cell in row):
            return True
    # Periksa kolom
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    # Periksa diagonal
    if all(board[i][i] == player for i in range(3)):
        return True
    if all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

def is_board_full(board):
    for row in board:
        for cell in row:
            if cell == " ":
                return False
    return True

def play_tic_tac_toe():
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"

    while True:
        print_board(board)
        print(f"Pemain {current_player}, giliran Anda.")

        try:
            row = int(input("Masukkan nomor baris (1-3): ")) - 1
            col = int(input("Masukkan nomor kolom (1-3): ")) - 1

            if not (0 <= row <= 2 and 0 <= col <= 2):
                raise ValueError("Input tidak valid. Masukkan angka antara 1 dan 3.")
            if board[row][col] != " ":
                raise ValueError("Kotak sudah terisi. Pilih kotak lain.")

            board[row][col] = current_player

            if check_win(board, current_player):
                print_board(board)
                print(f"Pemain {current_player} menang!")
                break
            elif is_board_full(board):
                print_board(board)
                print("Permainan seri!")
                break

            current_player = "O" if current_player == "X" else "X"

        except ValueError as e:
            print(e)

if __name__ == "__main__":
    play_tic_tac_toe()

