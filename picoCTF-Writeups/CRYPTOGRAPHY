# Cryptography Reversal Methodology (CTF Framework)

This framework explains how to mathematically break dynamic substitution ciphers (like the Vigenère cipher) commonly found in Medium-tier CTF cryptography challenges. Instead of relying on automated online tools, this approach uses pure algebraic logic and Python scripting to reverse the encryption function.

---

## Phase 1: Analyzing the Cipher Logic (The Forward Math)
In modern cryptography challenges, you are usually given a ciphertext and a key string. The encryption algorithm shifts the plaintext dynamically, meaning the same letter in the plaintext might become a different letter in the ciphertext depending on its position.

Treat the English alphabet as a modulus number line where $A = 0, B = 1, \dots, Z = 25$.

The forward encryption formula used by the challenge is:
$$C \equiv (P + K) \pmod{26}$$
*   $C$ = Ciphertext integer value
*   $P$ = Plaintext integer value
*   $K$ = Key integer value at the current index

---

## Phase 2: Inverting the Mathematical Shift (The Reverse Logic)
Just like solving a linear equation in a Class 12 mathematics exam, we must isolate the unknown variable ($P$). 

To reverse the modular addition, we simply subtract the key value from the ciphertext value. 
The reverse decryption formula is:
$$P \equiv (C - K) \pmod{26}$$

**The Logic Trap (What most students miss):** 
The script must *only* apply this mathematical shift to alphabetical characters. Numbers (`0`, `3`), underscores (`_`), and curly braces (`{`, `}`) in the `picoCTF{...}` format must remain completely untouched. Furthermore, the key loop should "pause" and not increment when it hits a non-alphabetical character.

---

## Phase 3: Writing the Exploit Script (`solve.py`)
This script takes the encrypted string, applies the inverted mathematical function to the letters, and ignores the special characters to reconstruct the original flag.

```python
# Step 1: Input the given variables from the challenge
ciphertext = "rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_2951c89f}"
key = "CYLAB"

decrypted_flag = []
key_index = 0

# Step 2: Loop through the ciphertext and reverse the math
for char in ciphertext:
    if char.isalpha():
        # Convert the current key letter into an integer shift (0-25)
        k = ord(key[key_index % len(key)].upper()) - ord('A')
        
        # Determine if the ciphertext character is upper or lower case
        base = ord('A') if char.isupper() else ord('a')
        
        # Apply the reverse formula: P = (C - K) mod 26
        c_val = ord(char) - base
        p_val = (c_val - k) % 26
        
        # Convert the integer back to a character and append
        decrypted_flag.append(chr(p_val + base))
        
        # IMPORTANT: Only advance the key sequence if a letter was shifted
        key_index += 1
    else:
        # Ignore numbers and symbols (like brackets and underscores)
        decrypted_flag.append(char)

# Step 3: Print the mathematically reconstructed string
flag = "".join(decrypted_flag)
print(f"[+] Decrypted Flag: {flag}")
