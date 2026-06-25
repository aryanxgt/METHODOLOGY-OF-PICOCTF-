# METHODOLOGY-OF-PICOCTF-
# My picoCTF Journey 🚩

Welcome to my picoCTF writeup repository! I am currently working my way through the platform to build my skills in Reverse Engineering, Binary Exploitation, Forensics, Cryptography, and general cybersecurity. 

## 🏆 Completed Learning Paths & Categories

### **[Low Level Binary Intro] - 100% Complete**
This learning path introduces assembly language, debuggers, and basic program manipulation. 

| Category | Challenges | Status |
| :--- | :--- | :---: |
| **Warmup** | Obedient Cat, Warmed Up, ASCII Numbers, Picker I | ✅ |
| **Intro to Assembly** | Bit-O-Asm-1, Bit-O-Asm-2, Bit-O-Asm-3, Bit-O-Asm-4 | ✅ |
| **Intro to Debuggers** | GDB baby step 1, GDB baby step 2, GDB baby step 3, GDB baby step 4 | ✅ |

### **[Challenge Library Intro] - 100% Complete**
This section serves as a fundamental introduction to navigating the picoCTF platform, understanding the challenge format, and grasping the basics of capturing flags.

| Category | Challenges | Status |
| :--- | :--- | :---: |
| **Intro to CTFs** | *All Challenges Completed* | ✅ |

### **[General Skills] - 100% Complete**
This category covers foundational CTF skills, including Linux terminal navigation, bash scripting, encoding/decoding, and basic network requests.

| Category | Challenges | Status |
| :--- | :--- | :---: |
| **General Skills** | *All Challenges Completed* (e.g., Bases, First Grep, strings it, plumbing) | ✅ |

### **[Cryptography] - 100% Complete**
This category focuses on modern and historical encryption methods, hashing algorithms, and mathematical puzzles.

| Category | Challenges | Status |
| :--- | :--- | :---: |
| **Cryptography** | *All Challenges Completed* (e.g., Mod 26, 13, The Numbers, Caesar) | ✅ |

### **[Forensics] - 100% Complete**
This category covers the analysis of digital artifacts, including hidden files, packet captures (PCAPs), steganography, and metadata extraction.

| Category | Challenges | Status |
| :--- | :--- | :---: |
| **Forensics** | *All Challenges Completed* (e.g., information, Matryoshka doll, Wireshark doo dooo) | ✅ |

### **[Python in CTF] - 100% Complete**
This section demonstrates proficiency in using Python for cybersecurity tasks, including automating exploits, decoding data, and analyzing scripts.

| Category | Challenges | Status |
| :--- | :--- | :---: |
| **Python / Scripting** | *All Challenges Completed* | ✅ |

---

> **Note:** All challenge folders contain my specific step-by-step writeups (`README.md`), the provided artifacts, and any solve scripts I used.
> # 🎯 picoCTF: Low Level Binary Intro - 100% Completion Methodology

## 📌 Overview
This repository documents my methodology and solutions for achieving 100% completion in the **Low Level Binary Intro** learning path on picoCTF. As a student diving into cybersecurity and low-level systems, this path served as my foundational introduction to how code executes at the machine level, how memory is managed, and how vulnerabilities are actively exploited.

## 🧰 Tools of the Trade
Before tackling the challenges, setting up the right environment is non-negotiable. My primary toolkit consists of:
* **Linux Environment:** Ubuntu via WSL or a dedicated Virtual Machine.
* **GDB (GNU Debugger):** Essential for dynamic analysis (setting breakpoints, stepping through execution, and inspecting registers).
* **Python 3:** For rapid scripting, particularly hex-to-decimal conversions and payload generation.
* **Objdump / Disassemblers:** For static analysis of ELF binaries without executing them.

---

## 🧠 Core Methodology: The 3-Phase Approach

### Phase 1: Static Analysis & Assembly (The Blueprint)
*Focus: Warmup & Intro to Assembly Challenges*

Before running any binary, I analyze its structure to understand the underlying logic.
1. **Disassembly:** I use `objdump -d` or GDB's `disassemble main` command to view the raw assembly instructions.
2. **Register Tracking:** I manually track the state of key registers (like EAX for return values, and RBP/RSP for stack pointers) line by line.
3. **Control Flow Mapping:** I identify `cmp` (compare) and `jmp`/`jle` (jump) instructions to map out loops and if/else conditions.
4. **Data Conversion:** Assembly heavily relies on hexadecimal values (e.g., 0x30). I write simple Python scripts to convert these to decimal formats as required by the picoCTF flag format.

### Phase 2: Dynamic Analysis (The Execution)
*Focus: Intro to Debuggers Challenges*

When static analysis isn't enough, I run the program in a controlled environment to observe how memory changes in real-time.
1. **Setting Breakpoints:** I place breakpoints before critical `return` statements or conditional jumps.
2. **Execution & Inspection:** I run the program and use GDB commands to inspect the memory state at exact moments in time.
3. **Understanding Endianness:** A key hurdle in these challenges is reading memory correctly. I reverse the byte order for **Little Endian** architectures (e.g., reading the bytes 0x11 0x22 0x33 0x44 in memory as 0x44332211).

### Phase 3: Binary Exploitation (The Break-In)
*Focus: Binary Exploitation Basics*

This is where understanding memory turns into an offensive attack.
1. **Finding the Vulnerability:** I look for unsafe C functions (like `gets()`) that do not perform bounds checking on the size of user input.
2. **Calculating the Offset:** I feed the program patterned inputs to intentionally crash it. By checking the Instruction Pointer (RIP/EIP), I find exactly how many bytes are needed to trigger a buffer overflow and overwrite the return address.
3. **Payload Delivery:** Using Python or bash piping, I craft a payload that fills the buffer and accurately overwrites the return address with the memory address of the hidden "win" function to print the flag.

---

## 🎓 Key Takeaways
Completing this path reinforced several critical concepts that bridge the gap between software and hardware:
* High-level code (like C or C++) is ultimately just a series of instructions moving bytes between registers and memory addresses.
* Manual memory management is the most critical—and dangerous—aspect of low-level software security.
* Patience, systematic debugging, and reading the stack are much more valuable skills than trying to memorize every single assembly instruction.

* # 🎯 picoCTF: Challenge Library Intro - 100% Completion Methodology

## 📌 Overview
This repository documents my methodology for completing the **Challenge Library Intro** on picoCTF. As the gateway to competitive CTFs, this path focuses heavily on "General Skills." It builds the muscle memory required for navigating Linux, manipulating different data encodings, and performing basic web and forensic analysis. Mastering these fundamentals is the prerequisite for tackling advanced cryptography and binary exploitation.

## 🧰 Tools of the Trade
For introductory challenges, keeping the toolset lightweight and fast is key:
* **Linux Terminal:** The primary environment (WSL, native Linux, or the picoCTF webshell).
* **CyberChef:** The ultimate browser-based "Swiss Army Knife" for translating, decoding, and analyzing data formats.
* **Netcat (`nc`) & SSH:** Essential for connecting to remote challenge instances and interacting with live services.
* **Python 3:** For automating repetitive decoding math or interacting with sockets using the `pwntools` library.

---

## 🧠 Core Methodology: The 3-Phase Approach

### Phase 1: Terminal Mastery & Navigation (The Command Center)
*Focus: General Skills & File System Manipulation*

Before trying to "hack" anything, I ensure I can move through the environment efficiently.
1. **File System Navigation:** I rely on `ls -la` to expose hidden files (files starting with a `.`) and `cd` to move through nested directories quickly.
2. **Text Processing & Searching:** When dealing with massive text dumps or log files, I use `grep`. Commands like `grep -iE "picoCTF\{.*?\}" file.txt` allow me to isolate the flag instantly using Regular Expressions.
3. **Network Interaction:** For remote challenges, I use `ssh` for secure shell access and `nc` (netcat) to pipe inputs into active challenge sockets and read the server's raw responses.

### Phase 2: Encodings & Data Transformation (The Rosetta Stone)
*Focus: Basic Cryptography & Data Representation*

Information in CTFs is rarely presented in plain text. I use a systematic approach to identify and reverse data obfuscation.
1. **Signature Identification:** I train myself to recognize the visual signatures of different data formats—such as Base64 (alphanumeric, often ending in `=` padding), Hexadecimal (0-9, a-f), and raw binary.
2. **Rapid Decoding:** I use CyberChef's recipes to quickly decode nested encodings (e.g., peeling back layers from Hex to Base64 to ASCII) without writing custom scripts.
3. **Scripted Automation:** When challenges require rapid, repeated decoding or math (like Caesar ciphers or XOR operations), I write short Python scripts using the `base64` and `binascii` libraries to automate the translation process.

### Phase 3: Inspection & Forensics Basics (The Scavenger Hunt)
*Focus: Intro to Web & File Analysis*

Finding data hidden in plain sight or buried within file metadata.
1. **Web Inspection:** For basic web challenges, my first step is always checking the page source code (looking for hidden HTML/JS comments), inspecting the `robots.txt` file, and viewing the Browser Developer Tools (specifically the Network tab and Cookies).
2. **File Identification:** I never trust file extensions. I run the `file` command in Linux to determine the true file type by its magic numbers (e.g., finding an ELF executable disguised as a `.jpg`).
3. **String Extraction:** When handed an unknown, compiled, or corrupted file, I run the `strings` command to pull out any readable ASCII text, which frequently exposes hidden flags or developer notes.

---

## 🎓 Key Takeaways
Completing the Challenge Library Intro reinforced several foundational rules of cybersecurity:
* **The CLI is king:** The command line is the most powerful tool in a security professional's arsenal; mastering it saves hours of manual GUI work.
* **Data is fluid:** A file is just a sequence of bytes. Understanding how computers encode and interpret those bytes is step one to finding vulnerabilities.
* **Trust nothing, inspect everything:** Whether it is a file extension or a website's input field, the surface level is always designed to hide the underlying mechanics.
