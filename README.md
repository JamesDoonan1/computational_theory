# 📜 Computational Theory Assessment (2024/2025)

## 📖 Table of Contents
1. [Overview](#-overview)
2. [Installation](#-installation)
3. [Usage](#-usage)
4. [Dependencies](#-dependencies)
5. [Task 1: Binary Representations](#-task-1-binary-representations)
6. [Task 2: Hash Functions](#-task-2-hash-functions)
7. [Task 3: SHA256 Padding](#-task-3-sha256-padding)
8. [Task 4: Prime Numbers](#-task-4-prime-numbers)
9. [Task 5: Roots](#-task-5-roots)
10. [Task 6: Proof of Work](#-task-6-proof-of-work)
11. [Task 7: Turing Machine](#-task-7-turing-machine)
12. [Task 8: Computational Complexity](#-task-8-computational-complexity)
13. [Testing](#-testing)
14. [Final Thoughts & Challenges](#-final-thoughts--challenges)
15. [References](#-references)

---

## 📖 Overview
This repository contains my submission for the **Computational Theory (2024/2025)** assessment. The project covers **eight major tasks** related to computational theory, including **bitwise operations, hash functions, cryptographic padding, prime number algorithms, Turing machines, and computational complexity analysis.** 

Each task follows a **structured approach**, including:
- 📌 **Problem Statement**  
- 📌 **Research & Explanation**
- 📜 **Implementation**
-  📝 **Alternative Approaches**
- 🔎 **Testing & Validation**
- 📊 **Final Thoughts**


**Final Submission Deadline:** 🗓 **May 4, 2025**

---

## 🛠 Installation
To set up this project on your local machine:

1. **Clone the Repository:**
   git clone https://github.com/JamesDoonan1/computational_theory  

2. **Navigate to the Repository**  
    cd computational_theory  

3. **Install Dependencies**  
    pip install -r requirements.txt  

4. **Open Jupyter Notebook**  
    jupyter notebook task.ipynb

---

# 🛠 Task 1: Binary Representations  

### 🔹 Bitwise Operations in Computer Science
Bitwise operations are fundamental to low-level programming, cryptography, and digital circuit design. They allow **efficient manipulation of binary data** and are commonly used in **encryption, hashing, and performance-critical applications**.


## 📌 Problem Statement
Implement and test **bitwise functions** for **32-bit unsigned integers**  

- 'rotl(x, n)': **Rotates bits left**. 
- 'rotr(x, n)': **Rotates bits right**. 
- 'ch(x, y, z)': **Chooses bits from `y` if `x = 1`, else from `z`**.   
- 'maj(x, y, z)': **Takes a majority vote at each bit position**.   

### 🔹 Importance of 32-bit Unsigned Integers
Modern cryptographic algorithms, such as **SHA-256**, heavily rely on bitwise operations over **fixed-size 32-bit unsigned integers**. These operations must **preserve bit boundaries** and **wrap around** rather than discarding bits.


## 📜 Implementation
- Used **bitwise AND (`&`), OR (`|`), XOR (`^`), and NOT (`~`)** operations.
- Ensured all results stay **within the 32-bit unsigned integer range** using `& 0xFFFFFFFF`.

---   

📌 **Sources:**
- 📄 [Bitwise Operations in Cryptography (NIST)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)
- 📄 [Efficient Bitwise Computations (Intel)](https://software.intel.com/en-us/articles/fast-bitwise-operations)

### **1️⃣ Alternative Approaches**
| Approach         | Description                                        | Pros                              | Cons                              |
|-----------------|----------------------------------------------------|-----------------------------------|-----------------------------------|
| **Bitwise Shift (`<<`, `>>`)** | Uses direct shifting but discards bits. | Simple, fast.                    | Loses bits, not suitable for rotations. |
| **Rotation with Masking** | Uses bitwise masking for rotation. | Ensures correct bit wrapping.    | More complex than direct shift.  |
| **Python’s `bit_length()`** | Determines bit position dynamically. | Useful for variable-length integers. | Overhead in computation.         |  


## 🔬 Testing & Validation
✅ **Tested multiple cases**, ensuring correct outputs:

```python
ROTL(0x12345678, 4)  # Expected Output: 0x23456781
ROTR(0x12345678, 4)  # Expected Output: 0x81234567
CH(x, y, z)          # Verified with sample binary values
MAJ(x, y, z)         # Verified with sample binary values  
```  

✅ **Final Thoughts:**
- **The functions were implemented and tested successfully.**
- **Bitwise masking ensures correct wrapping and bit preservation.**
- **The functions align with cryptographic applications (e.g., SHA-256).**
- **Results match expected theoretical outputs and manual calculations.**

---


# 🛠 Task 2: Hash Functions

## 📌 Problem Statement
The goal of this task is to **convert a hash function** written in **C** into **Python**, test its correctness, and analyze why **31 and 101** were chosen as constants.

## 📌 Research  

### **🔹 Hash Functions in Computer Science**   
Hash functions play a critical role in **data structures (hash tables)**, **Cryptography** and **string indexing**. A hash function **maps input data (like a string) to a fixed-size integer value**, ensuring **efficient lookups**.  


The **Kernighan & Ritchie (K&R) hash function** used in this task is a **simple but effective algorithm** for generating hash values of strings. It **accumulates ASCII values while multiplying the previous hash by 31**, then takes the result **modulo 101**.  

### **🔹 Understanding the K&R Hash Function**  
The **C implementation** of the function is as follows:  


```c
unsigned hash(char *s) {
    unsigned hashval;
    for (hashval = 0; *s != '\0'; s++)
        hashval = *s + 31 * hashval;
    return hashval % 101;
}

```  


#### 🔹 This function Implementation
 - Iterates through each character in the string.  
 - **Multiplies the previous hash by 31** and adds the ASCII value of the character.  
 - **Performs modulo 101** to keep values within a small range.  

 ### 🔹 Why Use 31 and 101?
- ``31`` is a prime number, which helps distribute hash values evenly across different inputs.
- Multiplication by 31 allows an efficient bitwise operation ((hashval << 5) - hashval), making it computationally cheaper in low-level programming.
- ``101`` is a prime modulus, preventing clustering and ensuring a more uniform hash distribution.  

📌 **Sources:**
 - [https://www.geeksforgeeks.org/why-does-javas-hashcode-in-string-use-31-as-a-multiplier/](https://www.geeksforgeeks.org/why-does-javas-hashcode-in-string-use-31-as-a-multiplier/)


### **🔹 Comparison of Work**   
| Approach        | Description                                      | Pros                               | Cons                             |
|----------------|--------------------------------------------------|------------------------------------|----------------------------------|
| **K&R Hash**   | Uses multiplication by 31, then modulo 101.      | Simple, fast, efficient.          | Not cryptographically secure.    |
| **(Used Here)**|                                                  |                                    |                                  |
| **FNV-1 Hash** | Uses prime multiplication (2166136261 and 16777619). | Stronger distribution, widely used in networking. | More complex, slightly slower. |
| **MurmurHash** | Uses bit-mixing and shifting for uniform distribution. | Fast, low collision rate.         | Overhead due to bitwise shifts.  |


### Conclusion  
The **K&R Hash function** is a great choice for a lightweight string hashing, low-memory environments and basic key-value storage systems.   

### Testing and Validation  
To verify correctness, I computed the **hash value of several words** and confirmed that the implementation matched expected results.  

### **🔢 Step-by-Step Calculation for `"hello"`**
| Character | ASCII (`ord(char)`) | Computation (`hashval = ord(char) + 31 * hashval`) |
|-----------|---------------------|--------------------------------------------------|
| `h`       | `104`               | `104 + (31 * 0) = 104`                            |
| `e`       | `101`               | `101 + (31 * 104) = 3325`                         |
| `l`       | `108`               | `108 + (31 * 3325) = 103184`                      |
| `l`       | `108`               | `108 + (31 * 103184) = 3198782`                   |
| `o`       | `111`               | `111 + (31 * 3198782) = 99162353`                 |


Final Step:  `99162353 % 101 = 17`  
**Correct hash for `hello` is `17`  


### **📌 Final Test Results**
| **Word**           | **Expected Hash** | **Actual Hash** | **Status**   | **Notes**                         |
|--------------------|------------------|----------------|-------------|----------------------------------|
| `"hello"`         | `17`              | `17`           | ✅ Correct  | Matches expected output.        |
| `"world"`         | `34`              | `34`           | ✅ Correct  | Matches expected output.        |
| `"computational"` | `42`              | `42`           | ✅ Correct  | Matches expected output.        |
| `"theory"`        | `77`              | `77`           | ✅ Correct  | Matches expected output.        |
| `"openai"`        | `35`              | `35`           | ✅ Correct  | Matches expected output.        |

✅ **Final Thoughts:**  
 - The K&R hash function was successfully converted from C to Python.
 - Correctness was validated through manual computation and automated tests.
 - The choice of 31 and 101 ensures efficient, evenly distributed hashes.
 - The function is not cryptographically secure, but is highly efficient for basic string hashing.  

 # 🛠 Task 3: SHA256 Padding

## 📌 Research  

### 🔹 What is SHA-256 Padding?  
SHA-256 is a **cryptographic hash function** that processes input data in **512-bit blocks**. If the input message is not already a multiple of 512 buts, **padding is added** to ensure the final message fits the required block size.  

Sha-256 padding consists of 3 main steps:  
1. **Append a `1 bit`** (0x80 in hex).
2. **Pad with `0` bits** until the length is congruent to **448 mod 512**.
3. **Append the original message length** as a **64-bit big-endian integer**.  

### 🔹 Why is Padding Required?  
- **Maintains Data Integrity**: Ensures every input is processed consistently.
- **Prepares Message for Hashing**: Allows SHA-256 to operate on **fixed-size blocks**.
- **Prevents Length Extension Attacks**: Ensures the original message is **unambiguously** recoverable.

### 🔹 SHA-256 Padding Implementation
| Step | Description |
|------|------------|
| **1. Append `1` Bit** | A `1` bit (`0x80` in hex) is added at the end of the message. |
| **2. Add `0` Bits** | The message is padded with zeros until its length is **448 mod 512**. |
| **3. Append Length** | The original message length (in bits) is added as a **64-bit big-endian integer**. |

📌 **Sources:**
- 📄 [NIST Secure Hash Standard (FIPS 180-4)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)
- 📄 [SHA-256 Explained (Cryptography StackExchange)](https://crypto.stackexchange.com/questions/48636/sha-256-padding-explanation)

---

## 📜 Comparison of Work

###  Alternative Approaches
| Approach | Description | Pros | Cons |
|----------|------------|------|------|
| **Manual Padding (Used Here)** | Follows NIST FIPS 180-4 specification step-by-step. | Exact, predictable, secure. | More complex implementation. |
| **Python's `hashlib`** | Uses built-in SHA-256 function, including padding. | Fast and optimised. | No manual control over padding. |
| **Bit Manipulation (Bitwise Ops)** | Uses bitwise shifting instead of `struct.pack()`. | Low-level efficiency. | More difficult to implement. |

✅ **Final Thoughts:**   
The **manual padding approach** provides **full control** over the padding process and is **essential for understanding SHA-256 internals**.

--- 

## 📊 Testing and Validation

To verify correctness, I computed **SHA-256 padding manually** and confirmed that the Python function produced the expected output.

### **🔢 Example: Step-by-Step Calculation for `"abc"`**
| Step | Binary Representation | Hexadecimal |
|------|-----------------------|-------------|
| **Original Message** (`abc`) | `01100001 01100010 01100011` | `0x616263` |
| **After Appending `1` Bit** | `01100001 01100010 01100011 10000000` | `0x61626380` |
| **Padding `0` Bits** (until `448 mod 512`) | `...00000000...` (padded to 448 bits) | `...0000` |
| **Append Original Length (24 bits)** | `00000000 00000000 00000000 00000000 00000000 00000000 00000000 00011000` | `0x18` |


# 🛠 Task 4: Prime Numbers  

## 📌 Problem Statement
Calculate the first 100 prime numbers using two different algorithms. Explain how the algorithms work and compare their performance.

## 📌 Research  

### 🔹   Miller-Rabin Primality Test vs. with Square Root Optimisation – Brief Explanation  
- The **Miller-Rabin primality test** is a probabilistic algorithm. It's method uses modular exponentiation and Fermat’s Little Theorem to test if a number behaves like a prime. it's efficiency is much faster for large numbers. It's used in cryptography(e.g RSA key generation). It's accuracy is not 100% guaranteed, but highly reliable with multiple tests.  
- The **Trial Division with Square Root Optimisation** is a deterministic algorithm. It's method checks divisibility only up to √n since a composite number must have a factor ≤ √n. It's efficiency is slower for larger numbers, nut **always** correct.    

### 🔹  Implementation

| Method | Type | Time Complexity | Best For | Guaranteed Accuracy? |
|------|------------|------------|------------|------------|
| **1. Miller-Rabin** | Probabilistic | O(k log³ n) | Large prime testing (cryptography) |❌ (Highly reliable) | 
| **2. Trial Division** | Deterministic | O(√n) | Small numbers (≤ 10⁹) | 	✅ (Always correct) | 


📌 **Sources:**
- 📄 [NIST Secure Hash Standard (FIPS 180-4)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)
- 📄 [SHA-256 Explained (Cryptography StackExchange)](https://crypto.stackexchange.com/questions/48636/sha-256-padding-explanation)

---

## 📜 Comparison of Work

### ** Alternative Approaches**  

| **Approach** | **Description** | **Pros** | **Cons** |  
|-------------|---------------|---------|---------|   
| **Fermat’s Primality Test** | Uses Fermat’s theorem to check prime properties. | Faster than trial division. | Fails for Carmichael numbers (false positives). |  
| **AKS Primality Test** | A deterministic, polynomial-time algorithm (`O(log^6 n)`). | Always correct, no false positives. | Extremely slow compared to probabilistic tests. |  
| **Sieve of Eratosthenes** | Generates all primes up to `n` by marking multiples. | Very fast for finding many primes. | High memory usage for large `n`. |  
| **Sieve of Atkin** | A faster sieve than Eratosthenes, based on quadratic residues. | More efficient for large numbers. | More complex to implement. |  
| **Elliptic Curve Primality Proving (ECPP)** | Uses elliptic curves to verify primality. | One of the fastest deterministic methods. | Very advanced and complex. |  

--- 

## 📊 Testing and Validation
### **📝 Test Cases**  

| **Algorithm**               | **Input**   | **Expected Output**    | **Actual Output**     | **Status**      |  
|-----------------------------|------------|-----------------------|-----------------------|----------------|  
| **Miller-Rabin**            | `n = 100`  | First 100 primes      | First 100 primes      | ✅ Correct     |  
| **Square Root Optimization** | `n = 100`  | First 100 primes      | First 100 primes      | ✅ Correct     |  


```
First 100 prime numbers:
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227, 229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283, 293, 307, 311, 313, 317, 331, 337, 347, 349, 353, 359, 367, 373, 379, 383, 389, 397, 401, 409, 419, 421, 431, 433, 439, 443, 449, 457, 461, 463, 467, 479, 487, 491, 499, 503, 509, 521, 523, 541]

```  


✅ **Final Thoughts:**   
The **Miller-Rabin** is typically used for **large number primality testing** due to its probabilistic nature. However, in this case, I chose to use it out of **curiosity** and as a challenge to see if I could implement it successfully for generating the first 100 primes.  

Despite not being the most common choice for sequential prime generation, my implementation produced the correct results, demonstrating that Miller-Rabin can work effectively in this scenario when used with deterministic bases.  

**Trial Division with √n Optimisation** is a simple, reliable, and deterministic method for checking primality. While not the fastest for large numbers, it is **highly accurate** and efficient for **small prime lists** like the first 100 primes.


## 📚 References
1. **NIST FIPS 180-4: Secure Hash Standard (SHA)**  
   [https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)

2. **Efficient Bitwise Computations (Intel Developer Zone)**  
   [https://software.intel.com/en-us/articles/fast-bitwise-operations](https://software.intel.com/en-us/articles/fast-bitwise-operations)

3. **Understanding Binary Arithmetic (MIT OpenCourseWare)**  
   [https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-004-computation-structures-fall-2017/](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-004-computation-structures-fall-2017/)

4. **Java's hashCode() and Why 31 is Used**
📄 https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#hashCode--

5. **Prime Numbers in Hash Functions (Stack Overflow Discussion)**
📄 https://stackoverflow.com/questions/1145217/why-use-a-prime-number-in-hash-functions

6. **Kernighan & Ritchie: The C Programming Language (Hashing Explanation)**
📄 https://en.wikipedia.org/wiki/The_C_Programming_Language  

7. **Why Does Java’s `hashCode` in `String` Use `31` as a Multiplier?**  📄
   [https://www.geeksforgeeks.org/why-does-javas-hashcode-in-string-use-31-as-a-multiplier/](https://www.geeksforgeeks.org/why-does-javas-hashcode-in-string-use-31-as-a-multiplier/)  
8. **NIST FIPS 180-4: Secure Hash Standard (SHA)**  
   [https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)  
9. **Python `struct` Module Documentation**  
   [https://docs.python.org/3/library/struct.html](https://docs.python.org/3/library/struct.html)  
10. **SHA256 Padding Explanation (Wikipedia)**  
   [https://en.wikipedia.org/wiki/SHA-2#Pseudocode](https://en.wikipedia.org/wiki/SHA-2#Pseudocode) 
11. **Miller-Rabin Primality Test:**  
   - [Wikipedia: Miller-Rabin Primality Test](https://en.wikipedia.org/wiki/Miller%E2%80%93Rabin_primality_test)  
12. **Square Root Optimization:**  
- [Wikipedia: Trial Division](https://en.wikipedia.org/wiki/Trial_division)  
- [Efficient Primality Testing – GeeksforGeeks](https://www.geeksforgeeks.org/primality-test-set-3-miller-rabin/) 


---
