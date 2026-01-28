# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM

```
#include <stdio.h>
#include <string.h>

#define MAX 200

/* Function to encrypt using Rail Fence Cipher */
void encryptRailFence(char text[], int key, char result[])
{
    int len = strlen(text);
    char rail[key][len];

    /* Initialize rail matrix */
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, col = 0;
    int dir_down = 0;

    /* Fill the rail matrix */
    for (int i = 0; i < len; i++)
    {
        if (row == 0 || row == key - 1)
            dir_down = !dir_down;

        rail[row][col++] = text[i];

        dir_down ? row++ : row--;
    }

    /* Construct ciphertext */
    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                result[index++] = rail[i][j];

    result[index] = '\0';
}

/* Function to decrypt Rail Fence Cipher */
void decryptRailFence(char cipher[], int key, char result[])
{
    int len = strlen(cipher);
    char rail[key][len];

    /* Initialize rail matrix */
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, col = 0;
    int dir_down = 0;

    /* Mark zig-zag path with '*' */
    for (int i = 0; i < len; i++)
    {
        if (row == 0)
            dir_down = 1;
        if (row == key - 1)
            dir_down = 0;

        rail[row][col++] = '*';
        dir_down ? row++ : row--;
    }

    /* Fill rail matrix with ciphertext */
    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipher[index++];

    /* Read the matrix in zig-zag manner */
    row = 0;
    col = 0;
    for (int i = 0; i < len; i++)
    {
        if (row == 0)
            dir_down = 1;
        if (row == key - 1)
            dir_down = 0;

        result[i] = rail[row][col++];

        dir_down ? row++ : row--;
    }

    result[len] = '\0';
}

/* Driver program */
int main()
{
    char result[MAX];

    encryptRailFence("attack at once", 2, result);
    printf("Encryption:\n");
    printf("Ciphere Text for Attack at once -> %s\n", result);

    encryptRailFence("GeeksforGeeks ", 3, result);
    printf("Ciphere Text for GeeksforGeeks -> %s\n", result);

    encryptRailFence("defend the east wall", 3, result);
    printf("Ciphere Text for defend the east wall -> %s\n", result);
    printf("Decryption: \n");
    decryptRailFence("GsGsekfrek eoe", 3, result);
    printf("Plain text %s\n", result);

    decryptRailFence("atc toctaka ne", 2, result);
    printf("Plain text %s\n", result);

    decryptRailFence("dnhaweedtees alf  tl", 3, result);
    printf("Plain text %s\n", result);

    return 0;
}

```

# OUTPUT

<img width="911" height="438" alt="image" src="https://github.com/user-attachments/assets/796cc096-89ae-466b-96cf-4fa13f9e1549" />

# RESULT

Thus the programm for the rail fence transposition technique is implemented and done successfull.

