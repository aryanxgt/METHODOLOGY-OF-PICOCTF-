# Step 1: Extract the target byte array discovered from the binary's memory data
target_bytes = [
    50, 43, 33, 45, 1, 22, 4, 57, 32, 115, 
    44, 29, 48, 113, 52, 29, 47, 118, 119, 117, 
    113, 48, 63
]

# Step 2: Extract the XOR key constant found in the assembly disassembly
xor_key = 0x42

decrypted_flag = []

# Step 3: Loop through the binary's memory map and reverse the operation
for byte in target_bytes:
    # Reversing the XOR condition: input_char = target_byte ^ xor_key
    original_char = byte ^ xor_key
    decrypted_flag.append(chr(original_char))

# Step 4: Reassemble the characters into a readable string
flag = "".join(decrypted_flag)
print(f"[+] Decoded Binary Flag: {flag}")
