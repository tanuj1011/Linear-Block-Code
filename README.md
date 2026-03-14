# Linear-Block-Code

# Aim
Write a simple python program to Generate Matrix, Codeword, Hamming weight, Syndrome matrix and find the error on received codeword using Linear block code. 
# Tools required
COLAB

# Program

```
import numpy as np

# Input
p_bits = int(input("Enter parity bits: "))
m_bits = int(input("Enter message bits: "))

# Parity matrix
P = np.array([list(map(int, input("Enter row values: ").split())) for _ in range(m_bits)])

# Generator matrix G = [P | I]
I = np.eye(m_bits, dtype=int)
G = np.hstack((P, I))

n, k = G.T.shape

# All possible messages
M = np.array([[ (i >> (k-j-1)) & 1 for j in range(k)] for i in range(2**k)])

# Codewords
C = np.mod(np.dot(M, G), 2)

# Hamming weights
weights = np.sum(C, axis=1)
dmin = np.min(weights[1:])

# Parity Check Matrix H = [I | Pᵀ]
H = np.hstack((np.eye(n-k, dtype=int), P.T))
HT = H.T

print("\nGenerator Matrix G:")
print(G)

print("\nMessage  Codeword  Weight")
for i in range(len(M)):
    print(M[i], C[i], weights[i])

print("\nMinimum Hamming Distance:", dmin)

print("\nParity Check Matrix H:")
print(H)

# Received codeword
r = np.array(list(map(int, input("\nEnter received codeword: ").split())))

# Syndrome
s = np.mod(np.dot(r, HT), 2)
print("\nSyndrome:", s)

# Error detection
error = np.zeros(n, dtype=int)
for i in range(n):
    if np.array_equal(s, HT[i]):
        error[i] = 1

print("Error position:", error)

# Corrected codeword
corrected = np.mod(r + error, 2)
print("Correct codeword:", corrected)
```
# Output Waveform


# Results

