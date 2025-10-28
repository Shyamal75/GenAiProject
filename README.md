int_to_move = dict(zip(move_to_int.values(), move_to_int.keys()))


def predict_next_move(board):
    board_matrix = Board_To_Matrix(board).reshape(1, 8, 8, 12)
    predictions = model.predict(board_matrix)[0]
    legal_moves = list(board.legal_moves)
    legal_moves_uci = [move.uci() for move in legal_moves]
    sorted_indices = np.argsort(predictions)[::-1]
    for move_index in sorted_indices:
        move = int_to_move[move_index]
        if move in legal_moves_uci:
            return move
    return None





    
    # Create a chess board (start position)
board = Board()


# Display the board before prediction
print("Board before prediction:")
board
**

# Predict and make the move
next_move = predict_next_move(board)
board.push_uci(next_move)

# Display the board after prediction
print("\nPredicted move:", next_move)
print("Board after prediction:")
board
print(str(pgn.Game.from_board(board)))
