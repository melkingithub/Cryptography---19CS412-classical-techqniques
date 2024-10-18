## Rail Fence Cipher
## AIM :
To write a C program to implement the rail fence transposition technique.

## ALGORRITHM :
Step 1 :

Read the Plain text.

Step 2 :

Arrange the plain text in row columnar matrix format

Step 3 :

Now read the keyword depending on the number of columns of the plain text

Step 4 :

Arrange the characters of the keyword in sorted order and the

corresponding columns of the plain text.

Step 5 :

Read the characters row wise or column wise in the former order to get the

cipher text.

## PROGRAM :
```
#include <stdio.h>
#include <string.h>

void encryptRailFence(char *text, int key, char *cipherText) {
    int len = strlen(text);
    int row, col, direction;
    char rail[key][len];

    // Initializing the rail matrix with null characters
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            rail[row][col] = '\n';

    // Placing characters in the rail matrix in a zig-zag manner
    row = 0;
    direction = 1; // 1 for down, -1 for up
    for (col = 0; col < len; col++) {
        rail[row][col] = text[col];
        if (row == 0)
            direction = 1;
        else if (row == key - 1)
            direction = -1;
        row += direction;
    }

    // Reading the matrix row-wise to get the cipher text
    int index = 0;
    for (row = 0; row < key; row++) {
        for (col = 0; col < len; col++) {
            if (rail[row][col] != '\n') {
                cipherText[index++] = rail[row][col];
            }
        }
    }
    cipherText[index] = '\0';
}

void decryptRailFence(char *cipherText, int key, char *plainText) {
    int len = strlen(cipherText);
    int row, col, direction;
    char rail[key][len];

    // Initializing the rail matrix with null characters
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            rail[row][col] = '\n';

    // Marking the places in the rail matrix where the cipher text characters will go
    row = 0;
    direction = 1; // 1 for down, -1 for up
    for (col = 0; col < len; col++) {
        rail[row][col] = '*';
        if (row == 0)
            direction = 1;
        else if (row == key - 1)
            direction = -1;
        row += direction;
    }

    // Filling the rail matrix with the cipher text characters
    int index = 0;
    for (row = 0; row < key; row++) {
        for (col = 0; col < len; col++) {
            if (rail[row][col] == '*' && index < len) {
                rail[row][col] = cipherText[index++];
            }
        }
    }

    // Reading the matrix in a zig-zag manner to get the plain text
    row = 0;
    direction = 1; // 1 for down, -1 for up
    for (col = 0; col < len; col++) {
        plainText[col] = rail[row][col];
        if (row == 0)
            direction = 1;
        else if (row == key - 1)
            direction = -1;
        row += direction;
    }
    plainText[len] = '\0';
}

int main() {
    char text[100], cipherText[100], plainText[100];
    int key;

    // Input the plain text
    printf("Enter the plain text: ");
    gets(text);

    // Input the key (number of rails)
    printf("Enter the key (number of rails): ");
    scanf("%d", &key);

    // Encrypt the plain text
    encryptRailFence(text, key, cipherText);
    printf("Encrypted Text: %s\n", cipherText);

    // Decrypt the cipher text
    decryptRailFence(cipherText, key, plainText);
    printf("Decrypted Text: %s\n", plainText);

    return 0;
}
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/b7abc345-db82-4bf0-9c28-bb0a543da83c)

## RESULT:
The Program for Rail Fence is executed successfully.
