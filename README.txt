## Student Information

**Name:** Desmond Farley-Williams
**Student ID:** 008508702
**Repository:** https://github.com/3750449/Project-3----Huffman-Trees-part1-315.git

---

## Collaboration & Sources

- **C++ Reference (cppreference.com):** consulted for syntax and documentation of `<fstream>`, `std::tolower`, and `std::filesystem` functions.
- **GeeksforGeeks (geeksforgeeks.org):** used to compare syntax examples and confirm correct usage of C++ functions and file I/O operations.

---

## Implementation Details

This project implements **Part 1 of Project 3 — the Scanner module** of the Huffman Coding pipeline
It tokenizes text files into normalized ASCII words

### Files Implemented

- `Scanner.hpp / Scanner.cpp` — Implements the `Scanner` class
- `utils.hpp / utils.cpp` — Provides file and directory checks, error handling, and utility functions
- `main.cpp` — Command-line driver
- `CMakeLists.txt` — Build configuration for CLion

### Scanner Class

The `Scanner` reads a `.txt` file and writes one normalized token per line to `<base>.tokens`

#### Tokenization Rules

- Lowercase all letters (`a–z` only)
- Tokens match `[a–z]+` or `[a–z]+’[a–z]+`
- Drop digits, punctuation, dashes, whitespace, and non-ASCII bytes
- Apostrophes are only valid when **inside** a token (e.g., `camp's` → valid, `'tis` → `tis`)
- Each token is written on a separate line, ending with a newline

#### Main Functions

- **`readWord(std::istream&)`** — Reads the next token from the input stream
- **`tokenize(std::vector<std::string>&)`** — In-memory tokenization
- **`tokenize(std::vector<std::string>&, const std::filesystem::path&)`** — Wrapper that also writes tokens to a file
- **Helpers:**
  - `is_ascii(char)` — checks ASCII range
  - `to_lower(char)` — lowercases ASCII letters
  - `trim_edges(std::string&)` — removes stray leading/trailing apostrophes

---

## Testing & Status

### Tested Cases
**Input:**

'Tis the camp's fire.
rock-n-roll and O'Keefe
Room 101... really?
café on the corner
'em—again

**Output (`.tokens`):**

tis
the
camp's
fire
rock
n
roll
and
o'keefe
room
really
caf
on
the
corner
em
again

### Status

- **All required functionality complete.**
- **Tokenization verified** against the sample reference 

---

## How to Compile & Run

mkdir build && cd build
cmake ..
make
./p3_part1 input_output/<filename>.txt

**Example:**

./p3_part1 input_output/call_of_the_wild.txt

**Verify output:**

diff -u input_output/call_of_the_wild.tokens \
/home/faculty/kooshesh/cs315_f2025_p3_part1/part1_tokens_files/call_of_the_wild.tokens

