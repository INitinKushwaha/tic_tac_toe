# tic_tac_toe
using System;

class Program
{
    static char[,] board = new char[3, 3]; // Represents the game board
    static char currentPlayer = 'X'; // X starts the game

    static void Main(string[] args)
    {
        InitializeBoard();

        bool gameEnded = false;
        int turns = 0;

        while (!gameEnded)
        {
            DrawBoard();

            // Get player's move
            Console.WriteLine($"Player '{currentPlayer}', enter your move (row[1-3] column[1-3]):");
            string[] input = Console.ReadLine().Split(' ');
            int row = int.Parse(input[0]) - 1;
            int col = int.Parse(input[1]) - 1;

            // Check if the move is valid
            if (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row, col] == ' ')
            {
                board[row, col] = currentPlayer;
                turns++;

                // Check if the current player wins
                if (CheckWin(row, col))
                {
                    gameEnded = true;
                    Console.WriteLine($"Player '{currentPlayer}' wins!");
                }
                // Check if it's a tie
                else if (turns == 9)
                {
                    gameEnded = true;
                    Console.WriteLine("It's a tie!");
                }
                else
                {
                    // Switch player
                    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
                }
            }
            else
            {
                Console.WriteLine("Invalid move! Please try again.");
            }
        }

        DrawBoard();
    }

    static void InitializeBoard()
    {
        // Fill the board with empty spaces
        for (int i = 0; i < 3; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                board[i, j] = ' ';
            }
        }
    }

    static void DrawBoard()
    {
        Console.WriteLine("  1 2 3");
        for (int i = 0; i < 3; i++)
        {
            Console.Write(i + 1 + " ");
            for (int j = 0; j < 3; j++)
            {
                Console.Write(board[i, j] + " ");
            }
            Console.WriteLine();
        }
        Console.WriteLine();
    }

    static bool CheckWin(int row, int col)
    {
        // Check row
        if (board[row, 0] == currentPlayer && board[row, 1] == currentPlayer && board[row, 2] == currentPlayer)
            return true;
        // Check column
        if (board[0, col] == currentPlayer && board[1, col] == currentPlayer && board[2, col] == currentPlayer)
            return true;
        // Check diagonal
        if ((board[0, 0] == currentPlayer && board[1, 1] == currentPlayer && board[2, 2] == currentPlayer) ||
            (board[0, 2] == currentPlayer && board[1, 1] == currentPlayer && board[2, 0] == currentPlayer))
            return true;
        return false;
    }
}

