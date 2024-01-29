# grep
`grep -iRl`  matches the string provided recursively and lists matching files

`grep`:

*   `-E '\w+'` searches for words
*   `-o` only prints the portion of the line that matches

`grep -oP '(?<=potato: ).*'` useful grep regex for matching something after a keyword