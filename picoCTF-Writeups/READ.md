# Step 1: Copy the given output array from the challenge
ciphertext = [58, 36, 43, 56, 29, 35, 34, 40, 66, 44, 119, 53, 118, 65, 19, 55, 121, 61, 123, 59, 61, 128, 74, 68, 63]
key = 0x5A  # 90 in decimal

decrypted_bytes = []

# Step 2: Loop and invert the math
for index, element in enumerate(ciphertext):
    # Reverse logic: flag_char = (element - index) ^ key
    step1 = element - index
    flag_char_ascii = step1 ^ key
    decrypted_bytes.append(chr(flag_char_ascii))

# Step 3: Join and print the reconstructed flag
flag = "".join(decrypted_bytes)
print(f"[+] Reconstructed Flag: {flag}")
