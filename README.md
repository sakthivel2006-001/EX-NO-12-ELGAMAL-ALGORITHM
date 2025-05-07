# EX-NO-12-ELGAMAL-ALGORITHM
## SAKTHIVEL S
## 212223220090
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
#include <stdlib.h>
#include <math.h>
long long mod_exp(long long base, long long exp, long long mod) {
    long long result = 1;
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
long long mod_inverse(long long a, long long p) {
    return mod_exp(a, p - 2, p);
}
int main() {
    long long p, g, x, y, k, c1, c2, decrypted, message;
    printf("Enter a prime number (p): ");
    scanf("%lld", &p);
    printf("Enter a primitive root (g): ");
    scanf("%lld", &g);
    printf("Enter the private key (x): ");
    scanf("%lld", &x);
    y = mod_exp(g, x, p);
    printf("Public key (y) is: %lld\n", y);
    printf("Enter the message to encrypt (integer): ");
    scanf("%lld", &message);
    printf("Enter a random encryption key (k): ");
    scanf("%lld", &k);
    c1 = mod_exp(g, k, p);
    c2 = (message * mod_exp(y, k, p)) % p;
    printf("\nEncrypted values:\n");
    printf("c1: %lld\n", c1);
    printf("c2: %lld\n", c2);
    long long c1_inverse = mod_exp(c1, p - 1 - x, p); // Using (c1^x)^(-1) mod p
    decrypted = (c2 * c1_inverse) % p;
    printf("\nDecrypted message: %lld\n", decrypted);
    return 0;
}
```


## Output:
![image](https://github.com/user-attachments/assets/0b06f8ad-2dc5-4ad9-bf87-2437d4208cb3)


## Result:
The program is executed successfully.
