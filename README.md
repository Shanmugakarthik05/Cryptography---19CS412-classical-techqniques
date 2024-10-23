# Cryptography---19CS412-classical-techqniques
----------------------------------------------
# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:
## Vigenere Cipher
~~~
#include <stdio.h>
#include <string.h>
#include <ctype.h>

void vigenere_encrypt(const char *plaintext, const char *key, char *encrypted) {
    int pt_len = strlen(plaintext);
    int key_len = strlen(key);
    int i, j;

    for (i = 0, j = 0; i < pt_len; i++) {
        if (isalpha(plaintext[i])) {
            char pt_char = toupper(plaintext[i]);
            char key_char = toupper(key[j % key_len]);
            encrypted[i] = ((pt_char - 'A') + (key_char - 'A')) % 26 + 'A';
            j++;
        } else {
            encrypted[i] = plaintext[i];
        }
    }
    encrypted[pt_len] = '\0';
}

void vigenere_decrypt(const char *encrypted, const char *key, char *decrypted) {
    int enc_len = strlen(encrypted);
    int key_len = strlen(key);
    int i, j;

    for (i = 0, j = 0; i < enc_len; i++) {
        if (isalpha(encrypted[i])) {
            char enc_char = toupper(encrypted[i]);
            char key_char = toupper(key[j % key_len]);
            decrypted[i] = ((enc_char - 'A') - (key_char - 'A') + 26) % 26 + 'A';
            j++;
        } else {
            decrypted[i] = encrypted[i];
        }
    }
    decrypted[enc_len] = '\0';
}

int main() {
    char plaintext[1000], key[1000], encrypted[1000], decrypted[1000];

    printf("Enter the plaintext: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = '\0';

    printf("Enter the key: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = '\0';

    vigenere_encrypt(plaintext, key, encrypted);
    printf("Encrypted message: %s\n", encrypted);

    vigenere_decrypt(encrypted, key, decrypted);
    printf("Decoded message: %s\n", decrypted);

    return 0;
}

~~~
## OUTPUT:
![image](https://github.com/user-attachments/assets/c04c838e-c6f4-40cd-ac8d-957ea688b817)
## RESULT:
The program is executed successfully

