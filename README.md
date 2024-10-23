# Cryptography---19CS412-classical-techqniques
----------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:
## Rail Fence Cipher
~~~
#include <stdio.h>
#include <string.h>

void encryptRailFence(char *plainText, int key, char *cipherText) {
    int len = strlen(plainText);
    int rail[key][len];
    memset(rail, 0, sizeof(rail));
    int dir_down = 0, row = 0, col = 0;

    for (int i = 0; i < len; i++) {
        if (row == 0 || row == key - 1) dir_down = !dir_down;
        rail[row][col++] = plainText[i];
        dir_down ? row++ : row--;
    }

    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != 0)
                cipherText[index++] = rail[i][j];

    cipherText[index] = '\0';
}

void decryptRailFence(char *cipherText, int key, char *plainText) {
    int len = strlen(cipherText);
    int rail[key][len];
    memset(rail, 0, sizeof(rail));
    int dir_down, row = 0, col = 0;

    for (int i = 0; i < len; i++) {
        if (row == 0) dir_down = 1;
        if (row == key - 1) dir_down = 0;
        rail[row][col++] = 1;
        dir_down ? row++ : row--;
    }

    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == 1 && index < len)
                rail[i][j] = cipherText[index++];

    dir_down = 0, row = 0, col = 0;
    for (int i = 0; i < len; i++) {
        if (row == 0) dir_down = 1;
        if (row == key - 1) dir_down = 0;
        if (rail[row][col] != 0) plainText[i] = rail[row][col++];
        dir_down ? row++ : row--;
    }

    plainText[len] = '\0';
}

int main() {
    char plainText[100], cipherText[100], decryptedText[100];
    int key;

    printf("Enter the plain text: ");
    fgets(plainText, sizeof(plainText), stdin);
    plainText[strcspn(plainText, "\n")] = '\0';

    printf("Enter the key (number of rails): ");
    scanf("%d", &key);

    encryptRailFence(plainText, key, cipherText);
    printf("Encrypted Text: %s\n", cipherText);

    decryptRailFence(cipherText, key, decryptedText);
    printf("Decrypted Text: %s\n", decryptedText);

    return 0;
}

~~~
## OUTPUT:
![image](https://github.com/user-attachments/assets/e63f695f-8e99-4212-b654-94c7cd12232f)


## RESULT:
The program is executed successfully


