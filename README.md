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
