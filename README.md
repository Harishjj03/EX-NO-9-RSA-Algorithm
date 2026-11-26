# EX-NO-9-RSA-Algorithm
## Name: HARISHBALA J
## Reg no: 212224223002
## Date: 26/11/2026

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```c
#include <stdio.h>

long long gcd(long long a, long long b)
{
    while (b != 0)
    {
        long long temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

long long modInverse(long long e, long long phi)
{
    for (long long d = 1; d < phi; d++)
    {
        if ((e * d) % phi == 1)
            return d;
    }
    return -1;
}

long long modExp(long long base, long long exp, long long mod)
{
    long long result = 1;
    base = base % mod;
    while (exp > 0)
    {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        exp = exp / 2;
        base = (base * base) % mod;
    }
    return result;
}

int main()
{
    long long p, q, n, phi, e, d, msg, enc, dec;

    printf("Enter two prime numbers (p and q): ");
    scanf("%lld %lld", &p, &q);

    n = p * q;
    phi = (p - 1) * (q - 1);

    e = 2;
    while (e < phi && gcd(e, phi) != 1)
        e++;

    d = modInverse(e, phi);

    printf("Public Key (e, n): (%lld, %lld)\n", e, n);
    printf("Private Key (d, n): (%lld, %lld)\n", d, n);

    printf("Enter message (integer < %lld): ", n);
    scanf("%lld", &msg);

    enc = modExp(msg, e, n);
    dec = modExp(enc, d, n);

    printf("Encrypted message: %lld\n", enc);
    printf("Decrypted message: %lld\n", dec);

    return 0;
}
```



## Output:
<img width="1530" height="917" alt="image" src="https://github.com/user-attachments/assets/c6bab88f-920e-47e7-ab1b-cb6e985fcfd4" />




## Result:
 The program is executed successfully.
