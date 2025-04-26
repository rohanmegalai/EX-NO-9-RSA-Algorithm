# EX-NO-9-RSA-Algorithm
## NAME: ROHAN J
## REGISTER NO: 212223040171

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:

# Step 1:
Get two distinct prime numbers p and q from the user or predefine them.

# Step 2:
Calculate the modulus n by multiplying p and q: n=p*q.

# Step 3:
Calculate Euler’s Totient function φ(n): φ(n) = (p-1) * (q-1)

# Step 4:
Choose a public exponent e such that: 1 < e < φ(n) = 1 and gcd(e, φ(n)) = 1(ensure e is coprime with φ(n))

# Step 5:
Calculate the private key d as the modular inverse of e modulo φ(n): d . e ≡ 1(mod φ(n)) and Formulate the public key as the pair (e, n) and the private key as the pair (d, n), Ask the user for an alphabetic message to encrypt.

# Step 6:
Convert each character in the message to its ASCII value. , Encrypt each ASCII value using the formula: C=M^e mod n (where M is the ASCII value and C is the ciphertext)

# Step 7:
Decrypt each ciphertext using the formula: M=C^d mod n (where C is the ciphertext and M is the decrypted ASCII value).

# Step 8:
Convert the decrypted ASCII values back to characters to retrieve the original message.

# Step 9:
Print the encrypted message and the decrypted message and End the program.

## Program:
```
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <ctype.h>
#include <stdlib.h>

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}


long long mod_exp(long long base, long long exp, long long mod) {
    long long result = 1;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        base = (base * base) % mod;
        exp = exp / 2;
    }
    return result;
}

int mod_inverse(int e, int phi) {
    int t = 0, newt = 1;
    int r = phi, newr = e;
    while (newr != 0) {
        int quotient = r / newr;
        int temp = t;
        t = newt;
        newt = temp - quotient * newt;
        temp = r;
        r = newr;
        newr = temp - quotient * newr;
    }
    if (r > 1) return -1; 
    if (t < 0) t = t + phi;
    return t;
}

int main() {
   
    int p = 61;
    int q = 53;
    
    int n = p * q;
    int phi = (p - 1) * (q - 1);

 
    int e = 17; 
    if (gcd(e, phi) != 1) {
        printf("e and phi(n) are not coprime!\n");
        return -1;
    }

    int d = mod_inverse(e, phi);
    if (d == -1) {
        printf("No modular inverse found for e!\n");
        return -1;
    }

   
    printf("Public Key: (e = %d, n = %d)\n", e, n);
    printf("Private Key: (d = %d, n = %d)\n", d, n);

    char message[100];
    printf("Enter a message to encrypt (alphabetic characters only): ");
    fgets(message, sizeof(message), stdin);
    int len = strlen(message);
    if (message[len - 1] == '\n') message[len - 1] = '\0'; 

    printf("\nEncrypted Message:\n");
    long long encrypted[100];
    for (int i = 0; i < len; i++) {
        int m = (int)message[i];  
        encrypted[i] = mod_exp(m, e, n); 
        printf("%lld ", encrypted[i]);  
    }
    printf("\n");

   
    printf("\nDecrypted Message:\n");
    for (int i = 0; i < len; i++) {
        int decrypted = (int)mod_exp(encrypted[i], d, n);  
        printf("%c", (char)decrypted);  
    }
    printf("\n");

    return 0;
}
```
## Output:

![Screenshot 2025-04-26 153328](https://github.com/user-attachments/assets/7bca8902-dfa0-4c41-a1ca-8f2b2e9077e6)




## Result:
 The program is executed successfully.
