# Team mbahloul001 rrekhis
## myPlayer.py documentation
### myPlayer methods:
- `__init__()` method:

    It sets up the initial state of the game board, initializes the player's color, and sets up some important strategic positions on the board.

- `evaluate(self, board)` method:

    The evaluate function serves as a heuristic that attempts to provide a good estimate of which player is in a better position. The value returned by this function is used by the alphaBeta function to determine which move to make.

    It takes in a board parameter, which represents the current state of the game board, and returns a numerical score indicating the strength of the current position. The higher the score, the stronger the position of the player.

    The score is usually based on the current configuration of the board and the player's overall strategy. In fact, it is calculated based on various factors such as the number of empty cells, the positions of the player's and opponent's groups, the number of liberties each player has, and random noise.

- `alphaBeta(self, board, depth, alpha, beta, startingTime, deadline)` method:

    - Input Parameters:

        board: A Board object representing the current state of the game.

        depth: An integer representing the current depth of the search tree.

        alpha: The current value of the alpha parameter used in the alpha-beta pruning algorithm.

        beta: The current value of the beta parameter used in the alpha-beta pruning algorithm.

        startingTime: A float representing the starting time of the search.

        deadline: A float representing the deadline time for the search.

    - Output:

        The alpha value if it is a player's turn, or the beta value if it is the opponent's turn.

    - Functionality:

        The function uses iterative deepening to progressively search deeper into the game tree until the search time limit is reached. The *alpha* and *beta* parameters are used to determine which branches of the search tree can be pruned, thereby speeding up the search.

- `iterativeDepthSearch(self,board,deadline)` method:

    The iterativeDepthSearch method is responsible for performing an iterative deepening search to find the best move for the current player within a given time constraint. The method takes in a board object and a deadline, which is the maximum time allowed for the search.

    It calls the alphaBeta method with the current depth and a time limit calculated based on the remaining time left from the start time and the deadline.

    If the alphaBeta method returns a value greater than or equal to the pruneScore, the method immediately returns this value as the best move, as it indicates that the search has been pruned. Otherwise, the method sets the result to the value returned by the alphaBeta method and increments the depth. This process continues until the time limit is reached.

- `nextMove(self)` method:

    The nextMove function is responsible for determining the next move that the player should make based on the current state of the game. It uses iterativeDepthSearch() function to search the game tree using alpha-beta pruning with iterative deepening to evaluate the quality of each legal move available, then it selects the move with the highest score as the best move.

### Helper functions:
- `getNeighbors(stone)` function:

    The getNeighbors(stone) function takes an integer stone as input, which represents the position of a stone on the board. It returns a list neigh of integers that represent the positions of the neighboring stones on the board of the given stone.

- `getConnectedStones(board,stone,myColor,done,listStone)` function:

    The getConnectedStones function takes four arguments as input:

    board: A list representing the current state of the game board. Each element of the list can take one of three values: 0 (empty cell), 1 (cell occupied by a black stone), or 2 (cell occupied by a white stone).

    stone: An integer representing the position of a stone on the board. The integer value is obtained by converting the (row, column) coordinate of the stone to a single integer using the formula 9*row + column.

    myColor: An integer representing the color of the player calling the function. 1 represents black and 2 represents white.

    done: A list of integers representing the positions of the stones that have already been processed by the function.

    The function returns a list of integers representing the positions of all the stones of the same color as the input stone that are connected to it.

- `getAllConnections(board,myColor,opColor)` function:

    The getAllConnections function is useful in determining the connected groups of stones for each player on the board, which can be used to determine each player's territory and overall score. It takes in the board, myColor, and opColor as parameters and returns a tuple of two lists: myGroup and opGroup.

    myGroup contains all the groups of stones that belong to the player whose color is myColor. Each group is represented as a list of integers, where each integer is the index of a stone on the board. And opGroup contains all the groups of stones that belong to the opponent of the player whose color is myColor. The format of opGroup is the same as myGroup.

- `getGroupLiberties(board,group)` function:

    The getGroupLiberties function is used to calculate the number of liberties of a given group of stones in the game of Go. It takes in a game board and a list of connected stones (a group) as inputs, and returns the number of liberties (unoccupied adjacent points) of that group.

- `getAllGroupsLiberties(board, groups)` function:

    The getAllGroupsLiberties function is used to calculate the number of liberties for each group of stones on the board. It takes as input a board and a list of groups, where each group is a list of connected stones (represented by their index in the board), and returns a list containing the number of liberties for each group. This information can be useful in determining the strength and vulnerability of each group during gameplay.