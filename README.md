# Boyer-Moore String Matching Algorithm in Java

This Java program implements the Boyer-Moore string matching algorithm using the Bad Character Heuristic. The Boyer-Moore algorithm is an efficient string-searching algorithm that skips sections of the text to reduce the number of comparisons needed.

## How It Works

1. **Preprocessing the Pattern**:

   - The `badCharHeuristic` function creates a table (`badchar[]`) that records the last occurrence of each character in the pattern.
   - If a character in the text does not match the corresponding character in the pattern, the algorithm uses this table to determine how far to shift the pattern.

2. **Searching the Text**:

   - The `search` function slides the pattern over the text from left to right.
   - For each position, it compares the characters of the pattern with the corresponding characters in the text from right to left.
   - If a mismatch occurs, it uses the `badchar` table to determine the next shift.
   - If the pattern matches the current position in the text, it prints the position and continues to search for other occurrences.

3. **Output**:
   - The program prints the positions where the pattern is found in the text.
   - If the pattern is not found, it prints a message indicating that the pattern is not in the text.

## Code Explanation

```java
class BoyerMoore {

    static int NO_OF_CHARS = 256;

    // A utility function to get maximum of two integers
    static int max(int a, int b) {
        return (a > b) ? a : b;
    }

    // Preprocess the pattern to create the bad character heuristic table
    static void badCharHeuristic(char[] str, int size, int badchar[]) {
        // Initialize all occurrences as -1
        for (int i = 0; i < NO_OF_CHARS; i++)
            badchar[i] = -1;

        // Fill the actual value of last occurrence of a character
        // The index of the character in the pattern is stored
        for (int i = 0; i < size; i++)
            badchar[(int) str[i]] = i;
    }

    // A pattern searching function that uses the Bad Character Heuristic of the
    // Boyer-Moore Algorithm
    static void search(char txt[], char pat[]) {
        int m = pat.length; // Length of the pattern
        int n = txt.length; // Length of the text

        int badchar[] = new int[NO_OF_CHARS]; // Array to store the bad character heuristic

        // Fill the bad character array for the given pattern
        badCharHeuristic(pat, m, badchar);

        int s = 0; // s is the shift of the pattern with respect to text
        boolean patternFound = false; // Flag to check if the pattern is found

        // Loop to slide the pattern over text one by one
        while (s <= (n - m)) {
            int j = m - 1; // Start comparing from the end of the pattern

            // Keep reducing index j of the pattern while characters of the pattern and text
            // are matching at this shift s
            while (j >= 0 && pat[j] == txt[s + j])
                j--;

            // If the pattern is present at the current shift, then index j will become -1
            // after the above loop
            if (j < 0) {
                System.out.println("Pattern found at position: " + s);
                patternFound = true; // Pattern found, set the flag to true

                // Shift the pattern so that the next character in text aligns with the last
                // occurrence of it in the pattern
                // The condition s + m < n is necessary for the case when the pattern occurs at
                // the end of the text
                s += (s + m < n) ? m - badchar[txt[s + m]] : 1;
            } else {
                // Shift the pattern so that the bad character in text aligns with the last
                // occurrence of it in the pattern
                // The max function is used to make sure that we get a positive shift
                s += max(1, j - badchar[txt[s + j]]);
            }
        }

        // If pattern was not found, print the message
        if (!patternFound) {
            System.out.println("Pattern not found in the text.");
        }
    }

    // Driver program to test the above function
    public static void main(String[] args) {
        char txt[] = "Test. This is a test.".toCharArray();
        char pat[] = "test".toCharArray();
        search(txt, pat);
    }
}
```

## How to Run

1. **Compile the program using a Java compiler:**
   ```sh
   javac BoyerMoore.java

2. **Run the compiled program:**
    ```sh
    java BoyerMoore

## Example

For the input text `"Test. This is a test."` and pattern `"test"`, the output will be:

**Pattern found at position: 0**

**Pattern found at position: 15**


If you change the pattern to a string not present in the text, for example, `"xyz"`, the output will be:

**Pattern not found in the text.**
