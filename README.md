# cracking-rsa-64bit
A quantum computing simulation to crack RSA encryption
cracking-rsa-64bit
# Project Overview
This project investigates the vulnerability of the widely used RSA encryption algorithm to quantum adversaries. With the continuous advancement of technology, including the emergence of large-scale quantum computers, traditional cryptographic systems like RSA face a significant threat of compromise. This study provides a practical demonstration of RSA breaking by simulating quantum attacks, specifically focusing on the factorization problem which underpins RSA's security.

# Motivation
RSA's security relies on the computational difficulty of factoring large numbers. However, quantum computers, leveraging algorithms like Shor's algorithm, are inherently capable of efficiently solving such "hard problems." This project is motivated by the critical need to:
Examine the efficacy of both conventional and quantum computing in the decryption of RSA encryption.
Evaluate the security posture of cryptographic systems in the post-quantum era.
Contribute to the ongoing discussion and development of quantum-resistant cryptographic methods.
![rsa algorithm](https://github.com/user-attachments/assets/d7654f76-93cd-4a6e-80c7-cca17468fb36)

# Key Features & Methodology
This project simulates the breaking of RSA encryption, specifically targeting a 64-bit RSA key for demonstration purposes. The methodology involves:
RSA Key Generation: Utilizing OpenSSL to generate RSA public and private keys.
Information Encryption: Encrypting sample information using the generated RSA keys.
Quantum Simulation for Decryption: Attempting to decipher the encrypted information through quantum simulation. This process leverages the fundamental principles of quantum computing to undermine RSA's security.
Factoring to Period-Finding Reduction: The core of the quantum attack involves reducing the computationally intensive factoring problem (determining the prime factors of the large RSA modulus N) to a period-finding problem.
Quantum Fourier Transform (QFT) Utilization: The Quantum Fourier Transform is employed as a crucial component in solving the period-finding problem efficiently on a quantum simulator.
By determining the factors of the large number N, the private key can be computed, enabling the subsequent decryption of the message, thereby demonstrating the vulnerability.
<img width="911" height="473" alt="image" src="https://github.com/user-attachments/assets/f5d4d9d8-4e11-4330-87ad-7839102a07b5" />


# Expected Insights
The results derived from this study are expected to provide valuable insights into:

The practical effectiveness and speed of quantum simulation in breaking RSA encryption.
The current level of protection offered by RSA encryption against a simulated quantum adversary.
The urgency and necessity for transitioning to quantum-resistant cryptography in critical applications.

# Technologies Used
OpenSSL: For RSA key generation and conventional encryption/decryption operations.
Quantum Simulation Framework: Python with Qiskit for quantum circuit simulation.

# How to Run
To set up and run this project locally, please follow these steps:
Prerequisites: Python, OpenSSL installed, and a few specific quantum libraries.


Contributing
Feel free to open issues or submit pull requests if you have suggestions for improvements or bug fixes.
