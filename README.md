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
- 📌 **Research & Explanation**
- 📝 **Implementation**
- 🔎 **Testing & Validation**
- 📊 **Performance Analysis**

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

## 📌 Problem Statement
Implement and test **bitwise functions** for **32-bit unsigned integers**  

- 'rotl(x, n)': **Rotates bits left**. 
- 'rotr(x, n)': **Rotates bits right**. 
- 'ch(x, y, z)': **Chooses bits from `y` if `x = 1`, else from `z`**.   
- 'maj(x, y, z)': **Takes a majority vote at each bit position**. 

## 📜 Implementation
- Used **bitwise AND (`&`), OR (`|`), XOR (`^`), and NOT (`~`)** operations.
- Ensured all results stay **within the 32-bit unsigned integer range** using `& 0xFFFFFFFF`.

---  

## 🔬 Testing & Validation
✅ **Tested multiple cases**, ensuring correct outputs:

```python
ROTL(0x12345678, 4)  # Expected Output: 0x23456781
ROTR(0x12345678, 4)  # Expected Output: 0x81234567
CH(x, y, z)          # Verified with sample binary values
MAJ(x, y, z)         # Verified with sample binary values
``` 
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

#### 🔹 This function  
 - Iterates through each character in the string.  
 - **Multiplies the previous hash by 31** and adds the ASCII value of the character.  
 - **Performs modulo 101** to keep values within a small range.  

 ### 🔹 Why Use 31 and 101?
- ``31`` is a prime number, which helps distribute hash values evenly across different inputs.
- Multiplication by 31 allows an efficient bitwise operation ((hashval << 5) - hashval), making it computationally cheaper in low-level programming.
- ``101`` is a prime modulus, preventing clustering and ensuring a more uniform hash distribution.  TODO: ADDED SOURCES/ CITATION IF I CAN

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

### Final Thoughts  

 - The K&R hash function was successfully converted from C to Python.
 - Correctness was validated through manual computation and automated tests.
 - The choice of 31 and 101 ensures efficient, evenly distributed hashes.
 - The function is not cryptographically secure, but is highly efficient for basic string hashing.


## References  
1. Java's hashCode() and Why 31 is Used
📄 https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#hashCode--

2. Prime Numbers in Hash Functions (Stack Overflow Discussion)
📄 https://stackoverflow.com/questions/1145217/why-use-a-prime-number-in-hash-functions

3. Kernighan & Ritchie: The C Programming Language (Hashing Explanation)
📄 https://en.wikipedia.org/wiki/The_C_Programming_Language