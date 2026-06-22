import base64

# The weird string I found in the text file
encoded_text = "cGljb0NURntwaXhlbF9tYWdpY19leHBsb2l0fQ=="

# Decoding it
decoded_bytes = base64.b64decode(encoded_text)
print(decoded_bytes.decode('utf-8'))

The script spat out the flag!
[+] Flag: picoCTF{pixel_magic_exploit}

I learned that you shouldn't trust an image just because it looks right. Using binwalk to find embedded files and then checking text files for encodings like Base64 is a really solid way to hunt for hidden data, I FAILED HERE 2 TIMES 
