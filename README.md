- 👋 Hi, I’m @Shrijalagasti
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Shrijalagasti/Shrijalagasti is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
# Define a class to represent the game board
class GameBoard:
  def __init__(self):
    # Initialize the game board with empty positions for the goats and tigers
    self.board = [[' ' for i in range(8)] for j in range(8)]
    # Keep track of the number of goats and tigers on the board
    self.num_goats = 0
    self.num_tigers = 0
  
  # Function to check if a given position on the board is empty
  def is_empty(self, row, col):
    return self.board[row][col] == ' '
  
  # Function to add a goat or tiger to the board at a given position
  def add_piece(self, piece, row, col):
    # Check if the given position is empty
    if self.is_empty(row, col):
      # If it is, add the piece to the board and update the count of goats and tigers
      self.board[row][col] = piece
      if piece == 'G':
        self.num_goats += 1
      else:
        self.num_tigers += 1
  
  # Function to move a piece from one position to another on the board
  def move_piece(self, start_row, start_col, end_row, end_col):
    # Check if the starting position is occupied and the ending position is empty
    if not self.is_empty(start_row, start_col) and self.is_empty(end_row, end_col):
      # If they are, move the piece from the starting position to the ending position
      piece = self.board[start_row][start_col]
      self.board[start_row][start_col] = ' '
      self.board[end_row][end_col] = piece
  
  # Function to check if a given move is valid according to the game rules
  def is_valid_move(self, start_row, start_col, end_row, end_col):
    # Get the piece at the starting position
    piece = self.board[start_row][start_col]
    # Check if the starting and ending positions are adjacent
    if abs(start_row - end_row) <= 1 and abs(start_col - end_col) <= 1:
      # If they are, check if the piece is a tiger
      if piece == 'T':
        # If it is, check if the ending position is occupied by a goat
        if self.board[end_row][end_col] == 'G':
          # If it is, the move is valid
          return True
        # If the ending position is not occupied by a goat, check if there is an empty space beyond the ending position
        elif self.is_empty(end_row + (end_row - start_row), end_col + (end_col - start_col)):
          # If there is, the move is valid
          return True
        else:
          # If there is not, the move is not valid
          return False
      # If the piece is a goat, check if all goats have been placed on the board
      elif piece == 'G' and self.num_goats == 20:

