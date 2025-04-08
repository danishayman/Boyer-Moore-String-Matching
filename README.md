# 🔍 Boyer-Moore String Matching Algorithm in Java

This Java program implements the Boyer-Moore string matching algorithm using the Bad Character Heuristic. The Boyer-Moore algorithm is an efficient string-searching algorithm that skips sections of the text to reduce the number of comparisons needed.

## 🚀 How It Works

1. **Preprocessing the Pattern** 🛠️

   - The `badCharHeuristic` function creates a table (`badchar[]`) that records the last occurrence of each character in the pattern.
   - If a character in the text does not match the corresponding character in the pattern, the algorithm uses this table to determine how far to shift the pattern.

2. **Searching the Text** 🔎

   - The `search` function slides the pattern over the text from left to right.
   - For each position, it compares the characters of the pattern with the corresponding characters in the text from right to left.
   - If a mismatch occurs, it uses the `badchar` table to determine the next shift.
   - If the pattern matches the current position in the text, it prints the position and continues to search for other occurrences.

3. **Output** 📊
   - The program prints the positions where the pattern is found in the text.
   - If the pattern is not found, it prints a message indicating that the pattern is not in the text.

## 💻 Code Structure

The implementation consists of several key components:

- `NO_OF_CHARS`: A constant defining the number of possible characters (256)
- `max()`: A utility function to get the maximum of two integers
- `badCharHeuristic()`: Preprocesses the pattern to create the bad character table
- `search()`: The main searching function implementing the Boyer-Moore algorithm
- `main()`: The driver program with a sample test case

## 🛠️ How to Run

1. **Compile the program using a Java compiler:**
   ```sh
   javac BoyerMoore.java
   ```

2. **Run the compiled program:**
   ```sh
   java BoyerMoore
   ```

## 📝 Example

For the input text `"Test. This is a test."` and pattern `"test"`, the output will be:

```
Pattern found at position: 0
Pattern found at position: 15
```

If you change the pattern to a string not present in the text, for example, `"xyz"`, the output will be:

```
Pattern not found in the text.
```

## 🎯 Performance

The Boyer-Moore algorithm is known for its efficiency:
- Best case: O(n/m) where n is the text length and m is the pattern length
- Worst case: O(n*m)
- Average case: O(n)

## 🤝 Contributing

Feel free to contribute to this project by:
- Reporting issues 🐛
- Suggesting improvements 💡
- Submitting pull requests 🔄

## 📜 License

This project is open source and available under the MIT License.
