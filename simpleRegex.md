# Simple Regex

## Character Classes

Lowercase character classes will match positively, while uppercase classes will match negatively.

`\s` matches whitespaces (spaces and tabs) while `\S` matches any non-whitespace characters (letters, numbers, punctuation, etc.)

	- `.` matches any character including all whitespace except newline
	- `\w` matches any word, which are considered as any alphanumeric, non-whitespace character. For instance, punctuation and brackets are not words.
	- `\d` matches any numerical word
	- `\s` matches any whitespace, not including linefeeds and carriage returns
	- 
