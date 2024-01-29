# Regex
`[0-9][0-9][0-9]\.[0-9][0-9][0-9]\.` pattern will match any three-number.three-number word. `^<something>$` means match from start to end, for example `^[A-Z][a-z]$` match such that a capital letter is at start and a small letter at end.

Paranthesis: `(a|b|c)` is a regex "OR" and means "a or b or c", although the presence of brackets, necessary for the OR, also _captures_ the digit.

Square Brackets: `[abc]` is a "character class" that means "any character from a,b or c" (a character class may use ranges, e.g. `[a-d]` = `[abcd]`)

Curly Brackets: `{n,m}` This form of the curly brackets is used to match the preceding character or pattern from n to m times, with n greater than m. If m is not present then the pattern is matched n or more times. For example, "/x{2,3}/" matches "xx" and "xxx".

`exrex` can be used to generate passwords with regular expressions like `exrex ‘^ed[h#f]{3}[123]{1,2}xf[!@#*]$’ -o wordlist.txt`