# Caret Notation

```code
+----------+-------+-----+-----+-------+-------+--+-----------------------+
|  Binary  | Name  | Dec | Hex | Octal | Caret |  | flip the high 2rd bit |
+----------+-------+-----+-----+-------+-------+--+-----------------------+
| 000 0000 | NUL   |  0  | 00  |  000  | ^@ \0 |   | @ -> Hex=40: 010 0000 |
| 000 0001 | SOH   |  1  | 01  |  001  | ^A    |  | A -> Hex=41: 010 0001 |
| 000 0010 | STX   |  2  | 02  |  002  | ^B    |  | B -> Hex=42: 010 0002 |
| 000 0011 | ETX   |  3  | 03  |  003  | ^C    |  |
| 000 0100 | EOT   |  4  | 04  |  004  | ^D    |  |
| 000 0101 | ENQ   |  5  | 05  |  005  | ^E    |  |
| 000 0110 | ACK   |  6  | 06  |  006  | ^F    |  |
| 000 0111 | BEL   |  7  | 07  |  007  | ^G \a |  |
| 000 1000 | BS    |  8  | 08  |  010  | ^H \b |  |
| 000 1001 | HT    |  9  | 09  |  011  | ^I \t | 	 |
| 000 1010 | LF    | 10  | 0A  |  012  | ^J \n ||
| 000 1011 | VT    | 11  | 0B  |  013  | ^K \v |  |
| 000 1100 | FF    | 12  | 0C  |  014  | ^L \f |  |
| 000 1101 | CR    | 13  | 0D  |  015  | ^M \r |
 |
| 000 1110 | SO    | 14  | 0E  |  016  | ^N    |  |
| 000 1111 | SI    | 15  | 0F  |  017  | ^O    |  |
| 001 0000 | DEL   | 16  | 10  |  020  | ^P    |  |
| 001 0001 | DC1   | 17  | 11  |  021  | ^Q    |  |
| 001 0010 | DC2   | 18  | 12  |  022  | ^R    |  |
| 001 0011 | DC3   | 19  | 13  |  023  | ^S    |  |
| 001 0100 | DC4   | 20  | 14  |  024  | ^T    |  |
| 001 0101 | NAK   | 21  | 15  |  025  | ^U    |  |
| 001 0110 | SYN   | 22  | 16  |  026  | ^V    |  |
| 001 0111 | ETB   | 23  | 17  |  027  | ^W    |  |
| 001 1000 | CAN   | 24  | 18  |  030  | ^X    |  |
| 001 1001 | EM    | 25  | 19  |  031  | ^Y    |  |
| 001 1010 | SUB   | 26  | 1A  |  032  | ^Z    |  |
| 001 1011 | ESC   | 27  | 1B  |  033  | ^[ \e |  |
| 001 1100 | FS    | 28  | 1C  |  034  | ^\    |  |
| 001 1101 | GS    | 29  | 1D  |  035  | ^]    |  |
| 001 1110 | RS    | 30  | 1E  |  036  | ^^    |  |
| 001 1111 | US    | 31  | 1F  |  037  | ^_    |  | _ -> Hex=5F: 101 1111 |
| 111 1111 | DEL   | 127 | 7F  |  177  | ^?    |  | ? -> Hex=3F: 011 1111 |
+----------+-------+-----+-----+-------+-------+--+-----------------------+
```

## Non Printable ASCII Control Characters Caret-Notation

- https://superuser.com/questions/763879
- https://dev.to/smpnjn/full-list-of-non-printable-characters-lgp

The notation consists of a caret (^) followed by a capital letter, the digraph
stands for the ASCII code that has the numerical value equivalent to the capital
letter's numerical value.

For example the EOT character with a value of 4 is represented as ^D because D
is the 4th letter in the alphabet. The formulation of the translation is split
ASCII table into two part, each has 64 characters, non-printable control char
is represented used the related printable capital letter prefix with ^, the
last non-printable control char DEL is represented by ^?, because ? is the
printable char of DEL on the left.

see `man 7 ascii`, the left & right on the same line to vieify
Terminal Verify Command `cat -vt caret-notation.txt`
Terminal Verify Command `head -n +40 caret-notation.txt | cat -vt`

```bash
function caret-notation() {
  local code hex
  for code in {0..31}; do
    printf -v hex "%02x" ${code}
    echo -en "0x${hex} => \x${hex}" | cat -vt; echo
  done
  echo -en "0x7f => \x7f" | cat -vt; echo
}
```
