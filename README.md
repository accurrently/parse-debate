# parse-debate
parse-debate is a Python program to parse debate transcripts and count the times strings appear within the transcript, and who said them.
Right now, the program is tuned to handle plaintext that uses a format similar to UC Berkeley's [American Presidency Project](http://www.presidency.ucsb.edu/debates.php):

*SPEAKER: text*

*more text*

*NEXT SPEAKER: text*

For now, the regex used for speaker detection is */^\[A-Z\](\[A-Z\]|\[a-z\])+:\s/*. Future versions may change this, or make it editable from the command line.

At this time, the keyword search simply uses Python's count() function. As a result, it will find terms that are parts of larger words. The term "tech" will match the word "technology," for instance. If you want to use whole word searches only, be sure to include spaces between the commas in your terms list (see below).

This is a work in progress, and should be used with caution. 

## Who is this for?
Anyone (mainly journalists) who want to grab data about terms used in debates or interviews, and who said them.

## What dependencies does parse-debate use?
There are only two imports: *argparse* and *re*. Both modules ship with Python, so you shouldn't need to grab anything fancy.

## Can I use this with Windows or OS X?
parse-debate is a simple Python script, and will work on any OS running Python. Python is free to use and is available for both [OS X](https://www.python.org/downloads/mac-osx) and [Windows](https://www.python.org/downloads/windows/). parse-debate was originally written on [Ubuntu Linux](http://www.ubuntu.com/), which ships with Python. (Most Linux distros do.) Ubuntu is free to use, and I encourage journalists to try it out.

## Usage
*parse-debate \[-h\] -f FILE \[FILE ...\] \[-v\] -t TERMS \[-o\] \[-s\] \[-c\]*

*-h, --help*

Show help message and exit


*-f FILE \[FILE ...\], --file FILE \[FILE ...\]*

Input file to read

  
*-v, --verbose*

Verbose output (doesn't do anything just yet)


*-t TERMS, --terms TERMS*

Comma delinated list of terms to search for


*-o, --output*

Write CSV output results data to file


*-s, --silent*

Prints output to std out


*-c, --case*

Preserve case sensitivity in search for terms


At the very least, *-f* and *-t* must be used.

## License
This program is free (as in speech) software made available under the GNU General Public License v3.0. See LICENSE for details.

