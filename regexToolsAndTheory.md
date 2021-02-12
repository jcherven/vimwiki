# Regex Tools and Theory

- [regexr.com](regexr.com)
- [regex101.com](regex101.com)
- [regexpal.com](regexpal.com)

## Regex Engines

A character, word, group, etc to be matched is a token.

In general, an expression is searched from left to right, token by token. If a token matches, it's pushed onto a stack and the next token is searched from the position of the last match.

If the entire expression is fulfilled, that stack is returned. If the entire expression is not matched, the stack is thrown away.

## Algorithms

- NFA: Nondeterministic Finite Automaton

Found in:
	- Perl
	- Python
	- vi/vim
	- sed

- DFA: Deterministic Finite Automaton

Found in:
	- grep
	- awk
	- BSD grep
	- these days, most applications that use a DFA by default also support backreferences and other extended features in their options. 

NFA based engines can "go back" in the regex. In the expression `\d{1,3}`, the part of the expression in brackets modifies the previous token. This is what is meant by the term backreference. DFA-based regex engines won't be able to look back, and will search for the literal brackets, numbers, and comma.  

## Standards

- IEEE POSIX Standards
	- generally DFA-minded
	- BRE (basic regular expressions)
		- provivides only basic pattern matching
		- `()` and `{}` metacharacters must be escaped to work
			- `\( \)`, `\{ \}`
	- ERE (extended regular expressions)
		- additional features like alternation (or) and repetition 
		- Superset of BRE
		- `()` and `{}` metacharacters don't need to be escaped unless they are part of a string literal token
		- Character classes are done like this: `[:digit:]`

	- SRE (simple regular expressions)
		- has been replaced by BRE
- PCRE (Perl compatible regular expressions) Standards
	- generally NFA-minded
	- Most programming languages follow this standard (java, python, .net, etc)
	- perl pulls from other standards; for instance perl supports many python implementations

## Example

```
8.8.8.8
12.234.43.51
192.168.0.2
127.0.0.1
903725819582349
ABC
hello123
```

Gnu grep with the PCRE flag will work with the following command in a file with IP addresses

```bash
grep -P '\d{1,3}\.\d{1,3}\.\d{1,3}' ip
```
However, grep with the ERE flag will not, due to its DFA affinity.

```bash
grep -E '\d{1,3}\.\d{1,3}\.\d{1,3}' ip
```

will need to be changed to:

```bash
grep -E '[[:digit:]]{1,3}\.[[:digit:]]{1,3}\.[[:digit:]]{1,3}' ip
```

 
