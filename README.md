# parse-debate
A python program to parse debate transcripts.

## Who is this for?
Anyone (mainly journalists) who want to grab data about terms used in debates or interviews, and who said them.

## Usage
**parse-debate \[-h\] -f FILE \[FILE ...\] \[-v\] -t TERMS \[-o\] \[-s\] \[-c\]**

**-h, --help**
Show help message and exit

**-f FILE \[FILE ...\], --file FILE \[FILE ...\]**
Input file to read
  
**-v, --verbose**
Verbose output (doesn't do anything just yet)

**-t TERMS, --terms TERMS**
Comma delinated list of terms to search for

**-o, --output**
Write CSV output results data to file

**-s, --silent**
Prints output to std out

**-c, --case**
Preserve case sensitivity in search for terms

At the very least, **-f** and **-t** must be used.


