# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:

```
#include <stdio.h>
#include <math.h>
#include <stdlib.h>
int mod_exp(int base, int exp, int mod) {
int result = 1;
base = base % mod;
while (exp > 0) {
if (exp % 2 == 1) {
result = (result * base) % mod;
}
exp = exp >> 1; 
base = (base * base) % mod;
}
return result;
}
int gcd(int a, int b) {
if (b == 0)
return a;
else
return gcd(b, a % b);

}
int main() {
int p, g, x;
int h, y; 
int message, k;
int c1, c2, decrypted_message; 
printf("\n\n****Elgamal encryption and decryption**\n\n");
printf("Enter a large prime number (p): ");
scanf("%d", &p);
printf("Enter a primitive root of p (g): ");
scanf("%d", &g);
printf("Enter the private key (x): ");
scanf("%d", &x);
h = mod_exp(g, x, p);
printf("Public key (h) = %d\n", h);
printf("Enter the message to encrypt (as an integer less than p): ");
scanf("%d", &message);
do {
printf("Enter the ephemeral key (k) such that gcd(k, p-1) = 1: ");
scanf("%d", &k);
} while (gcd(k, p - 1) != 1);
c1 = mod_exp(g, k, p); 
c2 = (message * mod_exp(h, k, p)) % p; 
printf("Ciphertext (c1, c2) = (%d, %d)\n", c1, c2);
int inverse = mod_exp(c1, p - 1 - x, p); 
decrypted_message = (c2 * inverse) % p; 
printf("Decrypted message = %d\n", decrypted_message);
return 0;
}
```
## OUTPUT
![crypt12](https://github.com/user-attachments/assets/c18e2e01-0b35-4514-af88-cd3473913b62)


## Result:
The program is executed successfully.
