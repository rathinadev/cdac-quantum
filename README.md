# 🚀 Hybrid Quantum-Safe Key Exchange (QSKE) Prototype

**Bridging classical and post-quantum cryptography for future-proof secure communication.**

---

## 💡 Project Overview

This project develops a proof-of-concept client-server prototype to demonstrate a **hybrid key exchange mechanism**. It addresses the critical challenge of transitioning to quantum-safe cryptography by combining the strengths of established classical algorithms with emerging post-quantum cryptographic (PQC) algorithms. This approach ensures security against both current classical attacks and future quantum computer attacks.

Developed as part of my **CDAC Internship** in Quantum Computing, this prototype focuses on the key exchange phase – the crucial first step in establishing a secure communication channel (analogous to the handshake in TLS/SSL or SSH).

## ⚠️ The Problem: Quantum Threat to Current Security

Modern secure communication relies heavily on public-key cryptography (e.g., RSA, ECDH) for key exchange. While robust against classical computers, these algorithms are known to be vulnerable to attacks by large-scale quantum computers. This poses a significant long-term threat to global digital security.

## ✨ The Solution: Hybrid Key Exchange

To mitigate this "quantum threat" during the transition period, **hybrid cryptosystems** are proposed. These systems derive a single session key from two independent key exchanges:
1.  **Classical Key Exchange:** Provides security against current, non-quantum attacks and leverages widely adopted, battle-tested algorithms.
2.  **Post-Quantum Key Exchange (PQC):** Offers resilience against future quantum computer attacks.

By combining the two, the overall security relies on the *strongest* of the two underlying schemes. If either the classical or the PQC component remains unbroken, the hybrid key exchange is secure.

This prototype specifically implements and benchmarks this hybrid key exchange process.

## 🔑 Key Features

*   **Client-Server Architecture:** A basic Python `socket` based client-server model simulating a network connection.
*   **Dual Key Exchange:**
    *   **Classical Component:** Implements key exchange using a standard classical algorithm (e.g., RSA Key Encapsulation or ECDH).
    *   **Post-Quantum Component:** Integrates a NIST-standardized PQC Key Encapsulation Mechanism (KEM), primarily **Kyber**.
*   **Hybrid Key Derivation:** Securely combines the two individual shared secrets into a final, unified hybrid session key using a cryptographic hash function (SHA-256).
*   **Performance Benchmarking:** Measures and reports:
    *   Execution time for key generation, encapsulation, decapsulation for both classical and PQC algorithms.
    *   Total handshake time for the hybrid key exchange.
    *   Size (in bytes) of the public keys and encrypted key material transmitted over the network.
*   **Modularity:** Designed for easy extension to swap in different classical or PQC algorithms for comparative analysis.

## ⚙️ Technologies Used

*   **Python 3.8+**
*   **`socket`**: For basic client-server network communication.
*   **`cryptography` (PyCA)**: For classical cryptographic primitives (RSA, ECDH, SHA-256).
*   **`pqcrypto`**: Python bindings to NIST PQC reference implementations (e.g., Kyber).
*   **`hashlib`**: For cryptographic hashing (SHA-256).
*   **`json` & `base64`**: For robust serialization and deserialization of cryptographic objects over the network.
*   **`time` & `timeit`**: For accurate performance benchmarking.
*   **`sys`**: For measuring object sizes.
*   **`matplotlib`**: (Planned for results visualization) For plotting performance and size comparisons.

## 🛠️ Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/rathinadev/cdac-quantum
    cd cdac-quantum
    ```
2.  **Create a virtual environment (recommended):**
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    (You'll need to create a `requirements.txt` file after installing the libs you use, e.g., `pip freeze > requirements.txt`).
    A typical `requirements.txt` might look like:
    ```
    cryptography
    pqcrypto
    matplotlib
    jsonpickle # Or implement manual json/base64 serialization
    ```

## 🚀 Usage

The project consists of two main scripts: `server.py` and `client.py`.

1.  **Start the Server:**
    Open a terminal and run:
    ```bash
    python server.py
    ```
    The server will start listening for incoming connections.

2.  **Run the Client:**
    Open a **separate terminal** and run:
    ```bash
    python client.py
    ```
    The client will connect to the server, perform the hybrid key exchange, and both parties will print their derived hybrid session key and performance metrics.

    *(Optional: If you implement command-line arguments for algorithm selection, update instructions here, e.g., `python client.py --classical-kem rsa --pqc-kem kyber`)*

### Expected Output

Both the client and server should output similar messages confirming:
*   Successful connection.
*   Key generation times.
*   Key exchange times.
*   The derived `Hybrid Session Key` (which should match on both ends).
*   Sizes of transmitted public keys and ciphertexts.

---

## 📊 Results & Analysis (Placeholder - **To be filled in after project completion**)

This section will detail the findings from running the hybrid key exchange with various algorithm combinations. It will include:

*   **Performance Charts:** Bar graphs/line plots comparing handshake times (e.g., RSA+Kyber vs. ECDH+Kyber).
*   **Overhead Analysis:** Comparison of public key and ciphertext sizes, highlighting the increased bandwidth usage with PQC.
*   **Key Findings:** Summary of insights gained regarding the practical implications (speed, size trade-offs) of hybrid PQC integration.
*   *(Include screenshots of your `matplotlib` plots here!)*

---

## 🛣️ Future Enhancements

*   **Additional Algorithms:** Integrate more NIST PQC KEMs (e.g., FrodoKEM, CRYSTALS-Dilithium for signatures if extending beyond KEMs).
*   **Authentication:** Add post-quantum digital signatures (e.g., Dilithium, Falcon) to authenticate the key exchange messages.
*   **Error Handling:** Implement more robust error handling for network failures or cryptographic issues.
*   **Full TLS Handshake Simulation:** Extend to simulate more phases of a real TLS handshake (e.g., certificate exchange, finished messages).
*   **GUI/Web Interface:** Develop a simple UI (using Streamlit or Flask) to make interaction and visualization more intuitive.
*   **Advanced Benchmarking:** More rigorous statistical analysis and profiling.

## 🤝 Contributing

This is an internship project, so direct contributions might not be the primary focus. However, feel free to open issues if you find bugs or have suggestions.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgements

*   **CDAC (Centre for Development of Advanced Computing):** For providing this incredible internship opportunity and guidance.
*   The developers of the `cryptography` and `pqcrypto` libraries for providing robust cryptographic tools.
*   The **NIST Post-Quantum Cryptography Standardization Project** for leading the charge on quantum-safe algorithms.

---

## 📧 Contact

For any questions or further discussion, feel free to reach out:

**Rathinadevan E M**  
GitHub: [rathinadev](https://github.com/rathinadev)  
LinkedIn: [rathina-devan](https://www.linkedin.com/in/rathina-devan/)


---