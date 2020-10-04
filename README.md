# wordwrap
An efficient non-destructive soft-wrap algorithm in PHP

This is written as a commandline utility, via the shebang on the first line, 
the usage note and the references to $argv and $argc.

The script takes a reference to a text file and a width that you want each line 
to be soft-wrapped at. It outputs the text without any line exceeding the specified width.

It is written in a slightly strange way, not the way I would typically program.
But this is because it is an exercise for me to figure out how it works and then factoring
it down to a simple structure, in preparation for porting to 6502 Assembly.

For example, there are two places where more than one IF statement occurs in a row next that
result in the same thing if true, a break. Normally I would reduce these to a single IF
statement with the conditions OR'd together. Splitting them into multiple IF's is closer
in structure to how it will be in 6502.

This algorithm is efficient and non-destructive, because it doesn't add any characters 
to the source text, nor does it duplicate any of the source text. Instead it builds a
single array ($lines) of offsets into the source text of where each line begins.

When outputting the wrapped text, a line's length is determined by making sure the offset
within the current line being output does not exceed the start offset of the next line.
Additionally, because long strings of spaces could cause a line to exceed width, the 
output loop over a single line should just end that line when it reaches the maximum 
width.

The algorithm is quite simple. It doesn't handle breaking words at hyphens or slashes.
And it doesn't handle tabs at all. It just treats a tab as a single non-space character.
But, this should be a good basis to build off of. And it should be well suited to being
ported to the C64, and other platforms with very limited memory.
