# SUDUKU
//If there is a solution of suduku then the code can print the solution



static boolean safe(int arr[][], int row, int col, int n){ // FUNCTION FOR CHECK THE NUMBER IS AT SAFE PLACE
        for (int i = 0; i < arr.length; i++) {// CHECK IF THE COLOUMN HAS THE SAME NUMBER
            if (n == arr[row][i]) {
                return false;
            }

        }
        for (int i = 0; i < arr.length; i++) {// CHECK IF THE ROW HAS THE SAME NUMBER
            if (n == arr[i][col]) {
                return false;
            }
        }

        int startRow = row - row % 3, startCol = col - col % 3;// CHECK IF THE GRID HAS THE SAME NUMBER
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                if (arr[i + startRow][j + startCol] == n)
                    return false;
        return true;

    }

    public static boolean sudukuSolver(int arr[][], int row, int col) {

        if (col == arr.length && row == arr.length - 1) {// BASE CASE

            return true;
        }
        if (col == arr.length) {
            row++;
            col = 0;
        }

        if (arr[row][col] != 0) {
            return sudukuSolver(arr, row, col + 1);// CHECK THE PLACE IS EMPTY OR NOT
        } else {// PLACE IS EMPTY

            for (int i = 1; i <= 9; i++) {
                if (safe(arr, row, col, i)) {// CHECK THE NUMBER IS VALID AND PUT THE NUMBER IN EMPTY SPACE
                    arr[row][col] = i;
                    if (sudukuSolver(arr, row, col + 1)) {
                        return true;
                    } //

                    {

                    }
                }
                arr[row][col] = 0;// NOT VALID NUMBER THEN REMAIN EMPTY SPACE
            }

        }

        return false;

    }

    public static void main(String[] args) {
        // int arr[][]=new int[9][9];
        int[][] arr = { { 5, 3, 0, 0, 7, 0, 0, 0, 0 }, { 6, 0, 0, 1, 9, 5, 0, 0, 0 }, { 0, 9, 8, 0, 0, 0, 0, 6, 0 },
                { 8, 0, 0, 0, 6, 0, 0, 0, 3 }, { 4, 0, 0, 8, 0, 3, 0, 0, 1 }, { 7, 0, 0, 0, 2, 0, 0, 0, 6 },
                { 0, 6, 0, 0, 0, 0, 2, 8, 0 }, { 0, 0, 0, 4, 1, 9, 0, 0, 5 }, { 0, 0, 0, 0, 0, 0, 0, 7, 9 } };

        if (sudukuSolver(arr, 0, 0)) {
            for (int i = 0; i < arr.length; i++) {
                for (int j = 0; j < arr.length; j++)
                    System.out.print(arr[i][j] + " ");
                System.out.println();
            }
        } else {
            System.out.println("NO SOLUTION EXIST");
        }

    }
