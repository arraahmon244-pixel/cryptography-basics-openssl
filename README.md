

# `README.md` for Cryptography Basics Assignment

```markdown
# Cryptography Basics using OpenSSL

## Objective
This project demonstrates hands-on implementation of **symmetric (AES)** and **asymmetric (RSA)** encryption using OpenSSL on Kali Linux.  
It highlights how data confidentiality can be maintained in real-world cybersecurity scenarios.

---

## Tools Used
- **Operating System:** Kali Linux  
- **Tool:** OpenSSL (version 3.x)  
- **Terminal:** Bash

---

## Project Structure

```

cryptography-basics-openssl/
│
─ screenshots/
  ─ part1_symmetric/       # AES encryption screenshots
 ── part2_asymmetric/      # RSA encryption screenshots

── outputs/                   # Encrypted and decrypted files
─ keys/                      # RSA key pair
── commands.txt               # Commands used for execution
─ README.md

````

---

## Part 1 — Symmetric Encryption (AES-256-CBC)

**Objective:** Encrypt and decrypt a message using the same secret key.  

**Steps:**

1. **Create Message File**
   ```bash
   echo "This is a secret message" > message.txt
   cat message.txt
````

![Create Message](screenshots/part1_symmetric/01_create_message.png)

2. **Encrypt the File**

   ```bash
   openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 -in message.txt -out encrypted.txt
   ```

   ![Encrypt AES](screenshots/part1_symmetric/02_encrypt_aes.png)

3. **View Encrypted File**

   ```bash
   cat encrypted.txt
   ```

   ![View Encrypted](screenshots/part1_symmetric/03_view_encrypted.png)

4. **Decrypt the File**

   ```bash
   openssl enc -aes-256-cbc -d -pbkdf2 -iter 100000 -in encrypted.txt -out decrypted.txt
   ```

   ![Decrypt AES](screenshots/part1_symmetric/04_decrypt_aes.png)

5. **Verify Decrypted File**

   ```bash
   cat decrypted.txt
   ```

   ![Verify Decryption](screenshots/part1_symmetric/05_verify_decryption.png)

**Security Note:** PBKDF2 with 100,000 iterations was used to strengthen key derivation against brute-force attacks.

---

## Part 2 — Asymmetric Encryption (RSA)

**Objective:** Encrypt a message using a public key and decrypt it using the private key.

**Steps:**

1. **Generate Private Key**

   ```bash
   openssl genpkey -algorithm RSA -out private_key.pem
   ```

   ![Generate Private Key](screenshots/part2_asymmetric/06_generate_private_key.png)

2. **Extract Public Key**

   ```bash
   openssl rsa -pubout -in private_key.pem -out public_key.pem
   ```

   ![Generate Public Key](screenshots/part2_asymmetric/07_generate_public_key.png)

3. **Encrypt Using Public Key**

   ```bash
   openssl pkeyutl -encrypt -pubin -inkey public_key.pem -in message.txt -out encrypted_rsa.txt
   ```

   ![Encrypt RSA](screenshots/part2_asymmetric/09_rsa_encrypt.png)

4. **View Encrypted RSA File**

   ```bash
   cat encrypted_rsa.txt
   ```

   ![View Encrypted RSA](screenshots/part2_asymmetric/10_view_rsa_encrypted.png)

5. **Decrypt Using Private Key**

   ```bash
   openssl pkeyutl -decrypt -inkey private_key.pem -in encrypted_rsa.txt -out decrypted_rsa.txt
   ```

   ![Decrypt RSA](screenshots/part2_asymmetric/11_rsa_decrypt.png)

6. **Verify Decrypted Message**

   ```bash
   cat decrypted_rsa.txt
   ```

   ![Verify RSA Decryption](screenshots/part2_asymmetric/12_verify_rsa.png)

**Security Note:** RSA allows anyone to encrypt a message using the **public key**, but only the **private key owner** can decrypt it, ensuring secure communication.

---

## Commands Used

All commands are listed in `commands.txt` for reproducibility.

---

## Conclusion

This project demonstrates:

* **Symmetric encryption (AES)** for fast and efficient data protection
* **Asymmetric encryption (RSA)** for secure key exchange and communication

Together, these techniques provide a foundational understanding of **cryptography in cybersecurity**.


```
