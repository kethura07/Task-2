#include <stdio.h>

#define MAX 10

// Function prototypes
void inputMatrix(int matrix[MAX][MAX], int rows, int cols);
void displayMatrix(int matrix[MAX][MAX], int rows, int cols);
void addMatrices(int mat1[MAX][MAX], int mat2[MAX][MAX], int res[MAX][MAX], int rows, int cols);
void multiplyMatrices(int mat1[MAX][MAX], int mat2[MAX][MAX], int res[MAX][MAX], int r1, int c1, int c2);
void transposeMatrix(int mat[MAX][MAX], int trans[MAX][MAX], int rows, int cols);

int main() {
    int matA[MAX][MAX], matB[MAX][MAX], result[MAX][MAX], transposed[MAX][MAX];
    int r1, c1, r2, c2;

    // Input dimensions for Matrix A
    printf("Enter rows and columns for Matrix A: ");
    scanf("%d %d", &r1, &c1);
    printf("Enter elements of Matrix A:\n");
    inputMatrix(matA, r1, c1);

    // Input dimensions for Matrix B
    printf("Enter rows and columns for Matrix B: ");
    scanf("%d %d", &r2, &c2);
    printf("Enter elements of Matrix B:\n");
    inputMatrix(matB, r2, c2);

    // 1. Matrix Addition
    if (r1 == r2 && c1 == c2) {
        addMatrices(matA, matB, result, r1, c1);
        printf("\n--- Matrix Addition (A + B) ---\n");
        displayMatrix(result, r1, c1);
    } else {
        printf("\nMatrix Addition not possible (Dimensions must match).\n");
    }

    // 2. Matrix Multiplication
    if (c1 == r2) {
        multiplyMatrices(matA, matB, result, r1, c1, c2);
        printf("\n--- Matrix Multiplication (A * B) ---\n");
        displayMatrix(result, r1, c2);
    } else {
        printf("\nMatrix Multiplication not possible (Columns of A must equal rows of B).\n");
    }

    // 3. Transpose of Matrix A
    transposeMatrix(matA, transposed, r1, c1);
    printf("\n--- Transpose of Matrix A ---\n");
    displayMatrix(transposed, c1, r1);

    return 0;
}

// Function to read a matrix from user input
void inputMatrix(int matrix[MAX][MAX], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("Element [%d][%d]: ", i, j);
            scanf("%d", &matrix[i][j]);
        }
    }
}

// Function to print a matrix
void displayMatrix(int matrix[MAX][MAX], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("%d\t", matrix[i][j]);
        }
        printf("\n");
    }
}

// Function to add two matrices
void addMatrices(int mat1[MAX][MAX], int mat2[MAX][MAX], int res[MAX][MAX], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            res[i][j] = mat1[i][j] + mat2[i][j];
        }
    }
}

// Function to multiply two matrices
void multiplyMatrices(int mat1[MAX][MAX], int mat2[MAX][MAX], int res[MAX][MAX], int r1, int c1, int c2) {
    // Initialize result matrix to 0
    for (int i = 0; i < r1; i++) {
        for (int j = 0; j < c2; j++) {
            res[i][j] = 0;
        }
    }

    // Compute multiplication
    for (int i = 0; i < r1; i++) {
        for (int j = 0; j < c2; j++) {
            for (int k = 0; k < c1; k++) {
                res[i][j] += mat1[i][k] * mat2[k][j];
            }
        }
    }
}

// Function to find the transpose of a matrix
void transposeMatrix(int mat[MAX][MAX], int trans[MAX][MAX], int rows, int cols) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            trans[j][i] = mat[i][j];
        }
    }
}
