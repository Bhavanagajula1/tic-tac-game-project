import java.util.Scanner;

public class TicTacToe {
    static char[][] board = new char[3][3];
    static char currentPlayer = 'X';
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        initializeBoard();
        boolean gameOn = true;

        while (gameOn) {
            displayBoard();
            playerMove();

            if (checkWin()) {
                displayBoard();
                System.out.println(" Player " + currentPlayer + " wins!");
                gameOn = false;
            } else if (isDraw()) {
                displayBoard();
                System.out.println(" It's a Draw!");
                gameOn = false;
            } else {
                switchPlayer();
            }
        }
    }

    static void initializeBoard() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = ' ';
            }
        }
    }

    static void displayBoard() {
        System.out.println("-------------");
        for (int i = 0; i < 3; i++) {
            System.out.print("| ");
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j] + " | ");
            }
            System.out.println("\n-------------");
        }
    }

    static void playerMove() {
        int position;
        boolean valid = false;

        while (!valid) {
            System.out.print("Player " + currentPlayer + ", enter cell (1-9): ");

            while (!scanner.hasNextInt()) {
                System.out.println("Invalid input! Enter number only.");
                scanner.next();
            }

            position = scanner.nextInt();
            if (position >= 1 && position <= 9) {
                int row = (position - 1) / 3;
                int col = (position - 1) % 3;

                if (board[row][col] == ' ') {
                    board[row][col] = currentPlayer;
                    valid = true;
                } else {
                    System.out.println("Cell already filled! Try again.");
                }
            } else {
                System.out.println("Choose a valid cell (1-9).");
            }
        }
    }

    static boolean checkWin() {
        char s = currentPlayer;

        for (int i = 0; i < 3; i++) {
            if ((board[i][0] == s && board[i][1] == s && board[i][2] == s) ||
                (board[0][i] == s && board[1][i] == s && board[2][i] == s)) {
                return true;
            }
        }

        return (board[0][0] == s && board[1][1] == s && board[2][2] == s) ||
               (board[0][2] == s && board[1][1] == s && board[2][0] == s);
    }

    static boolean isDraw() {
        for (char[] row : board) {
            for (char c : row) {
                if (c == ' ') return false;
            }
        }
        return true;
    }

    static void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }
}
