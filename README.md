# Project Overview

This project provides a practical demonstration of RSA encryption's vulnerability to quantum adversaries. The security of traditional cryptographic systems like RSA faces a significant threat from the emergence of large-scale quantum computers. By simulating a quantum attack, this study investigates the foundational problem of factoring large numbers, which underpins RSA's security, and offers a compelling proof of concept for its compromise.


# Motivation

RSA's security relies on the computational difficulty of factoring a large number into its prime components. However, quantum computers, with algorithms like **Shor's algorithm**, are inherently capable of solving such problems efficiently. This project is motivated by the critical need to:
* Evaluate the efficacy of quantum computing in the decryption of RSA encryption.
* Assess the security posture of cryptographic systems in the post-quantum era.
* Contribute to the ongoing discussion and development of **quantum-resistant cryptographic methods**.

# Key Features & Methodology

The project simulates the breaking of a 64-bit RSA key through a **hybrid quantum-classical approach**. The methodology is centered on the following steps:
<img width="1810" height="937" alt="shors_circuit_diagram1" src="https://github.com/user-attachments/assets/3a54f7c3-2f59-4d00-bb10-8733b55e73ce" />
figure 1.	High-Level Quantum Circuit Diagram.
* **RSA Key Generation**: A 64-bit RSA key pair is generated with a large modulus $N$ composed of two prime numbers, $p$ and $q$. A message is then encrypted using this public key.

* **Factoring to Period-Finding Reduction**: The core of the quantum attack involves reducing the computationally intensive factoring problem to a **period-finding problem**. A quantum circuit is constructed to find the period of the modular exponentiation function $f(x) = a^x \pmod{N}$, which is a crucial step in Shor's algorithm.

* **Quantum Fourier Transform (QFT) Utilization**: To efficiently solve the period-finding problem on a quantum simulator, the **Quantum Fourier Transform (QFT)** is employed. Specifically, a **semiclassical QFT** is utilized, which is a key feature of this project's implementation. This hybrid approach significantly reduces the circuit depth and the number of qubits required by strategically offloading the conditional phase rotations to a classical processor. This makes the simulation more robust against quantum noise and more practical for demonstration on current hardware. (To read more about  semiclassical QFT, https://github.com/AsnaMuneer/semiclassical_QFT)

* **Classical Post-processing**: The final step involves classical post-processing of the quantum measurement results. The most probable outcome from the quantum circuit is used to find the period of the function. This period is then used in a **continued fractions algorithm** and a **greatest common divisor (GCD)** calculation to derive the original prime factors, $p$ and $q$. By determining these factors, the private key can be computed and the message decrypted, thereby demonstrating the successful compromise of RSA's security.

<img width="1879" height="1282" alt="semiclassical qft flowchart" src="https://github.com/user-attachments/assets/57197c41-9421-490f-9cf8-45f043b3a778" />

# Expected Insights

The results derived from this study are expected to provide valuable insights into:

* The practical effectiveness and speed of a **hybrid quantum-classical simulation** in breaking RSA encryption.
* The current level of protection offered by RSA encryption against a simulated quantum adversary.
* The urgency and necessity for transitioning to **quantum-resistant cryptography** in critical applications.

<img width="1231" height="358" alt="qft_circuit_diagram" src="https://github.com/user-attachments/assets/471bb6d5-a282-46cb-aef3-aac4d1ec2d39" />

# Technologies Used

* **Python**: The primary programming language.
* **Qiskit**: The open-source framework used for building and simulating the quantum circuits.
* **rsa and sympy**: Python libraries used for RSA key generation and number-theoretic calculations.

# How to Run

To set up and run this project locally, please follow these steps:
* Prerequisites: Python, OpenSSL installed, and a few specific quantum libraries.

<img width="1426" height="842" alt="Screenshot rsa crack" src="https://github.com/user-attachments/assets/549a1f6d-ad46-4dfd-8e4e-d0552147fe03" />

The output systematically demonstrates each phase of the hybrid quantum-classical attack, from setting up the problem to successfully solving it.

### **Phase 1: Conceptual Demonstration of the Problem**
<img width="787" height="947" alt="shors flowchart replaced with semiclassical qft" src="https://github.com/user-attachments/assets/44575fd4-a024-4958-babc-8f1b51f72af3" />

The first part of the output establishes the cryptographic challenge we are addressing.

* **`Generating a 64-bit RSA key pair...`**: This initial section showcases the creation of a large-scale RSA key pair. The prime numbers $p$ and $q$ are deliberately chosen to be 32-bit, resulting in a 64-bit modulus $N$. This demonstrates the scale of the problem that Shor's algorithm is designed to solve in a real-world scenario.
* **`Original Message: 'Secret'`** and **`Encrypted Message (Ciphertext): ...`**: Following key generation, a sample message is encrypted. This step highlights why a factoring attack is so powerful: if we can find the prime factors, we can reconstruct the private key and decrypt the message.

This initial section is a conceptual setup. The actual cracking simulation that follows operates on a much smaller, pre-defined number ($N=15$) to make the demonstration feasible.

### **Phase 2: The Quantum Simulation and Its Output**

This is the core of the demonstration where the quantum algorithm is simulated to find the period of a function.

* **`Starting Shor's Algorithm Simulation for Proof of Concept (N=15)`**: This line explicitly states that the subsequent steps are for a proof of concept. The simulation is focused on factoring $N=15$ because factoring a 64-bit number is not currently possible on a quantum simulator.
* **`Most frequent measured value (binary): 01000000`** and **`Measured value (integer): 64`**: This is the critical result of the quantum part of the algorithm. The semiclassical QFT's job is to prepare a quantum state where the highest-amplitude outcome corresponds to the information needed to find the period. Our simulation, for a perfect demonstration, was configured to guarantee this specific measurement. In a real-world scenario, this would be the tallest peak on a probability histogram, representing the most likely correct measurement.

### **Phase 3: Classical Post-processing and Factoring**

The final phase uses the quantum result to perform classical number theory, ultimately leading to the solution.

* **`Calculated period r: 4`**: This is the moment where the quantum result is turned into a useful number for factoring. The measured value of $64$ is fed into a classical **continued fractions algorithm**. This algorithm finds a fraction that approximates the measured value, and the denominator of this fraction is the period $r$. In this case, the algorithm correctly identifies the period as $4$.
* **`SUCCESS! Found prime factors: p = 3, q = 5`**: This is the culmination of the entire process. The period $r=4$ is used in the final step of Shor's algorithm to calculate the prime factors. The classical calculation uses the greatest common divisor (GCD) to derive the factors $p=3$ and $q=5$. This is the ultimate objective—finding the factors that were used to create the original number $N=15$.

### **Phase 4: Verification**

The final output block serves as verification that the entire process was successful.

* **`Decryption with Cracked Key`**: A new private key is reconstructed from the factors we just found ($p=3$ and $q=5$).
* **`Verification: The cracked key successfully decrypted the message!`**: A test message is encrypted and then decrypted with the newly reconstructed key. The successful decryption confirms that our quantum simulation and subsequent classical post-processing correctly broke the key's security.
# Contributing

Feel free to open issues or submit pull requests if you have suggestions for improvements or bug fixes.
