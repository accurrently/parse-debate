#!/usr/bin/python
# parse-debate by Alex Campbell <alex@alexthejourno.com>
#
# This program's purpose is to parse and pull data about keywords from
# debates or interviews, keeping track of hits from each speaker.
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

import argparse
import re

# Let's get all of our arguments sorted out.
parser = argparse.ArgumentParser()
parser.add_argument("-f", "--file", nargs='+', type=str, help="Input file to read", required=True)
parser.add_argument("-v", "--verbose", help="Verbose output", action="count", default=0)
parser.add_argument("-t", "--terms", help="Comma delinated list of terms to search for", required=True)
# parser.add_argument("-w", "--write", help="Output lines for each speaker into their own files", action="store_true")
parser.add_argument("-o", "--output", help="Write CSV output results data to file", action="store_true")
parser.add_argument("-c", "--case", help="Preserve case sensitivity in search for terms", action="store_true")

# Handle inputs
args = parser.parse_args()

# This will tell us who said what
data = {}
results = {}

# Terms we'll be searching for
terms = args.terms.split(',')

# This holds all of the lines for each file
lines = {}

file_list = args.file
for file_index in range(len(file_list)):

	filecontents = ""

	try:
		if args.verbose >= 2:
			print("Opening %s ...\n" % file_list[file_index])
		infile = open(file_list[file_index], "r")
		try:
			filecontents = infile.read()
			
		finally:
			infile.close()
	except IOError:
		print("Could not read file: %s. Exiting.\n" % args.file)
		exit()

	# create a line for each paragraph
	lines[file_index] = filecontents.splitlines()

	# first off, determine what lines belong to what speaker

	speaker_pattern = re.compile("^(?P<name>[A-Z]([A-Z]|[a-z])+):\s")
	
	current_speaker = None

	for lines_index in range(len(lines)):
		hit = speaker_pattern.search(lines[lines_index])
		if hit:
			if args.verbose >= 3:
				print("Found speaker: %s.\n" % hit.group("name"))
			if not (hit.group("name") in data):
				data[hit.group("name")] = []
			if not (file_index in data[hit.group("name")]):
				data[hit.group("name")][file_index] = []
			if args.verbose >= 3:
				print("Adding line for speaker: %s.\n" % hit.group("name"))
			data[hit.group("name")][file_index].append(lines_index)
			current_speaker = hit.group("name")
		elif current_speaker:
			data[current_speaker][file_index].append(lines_index)
			

	

# Create a data table for each term
for term in terms:
	results[term] = {}

	# Create a row for each speaker
	for speaker in range(data):
		results[term][speaker] = []
		for file_index in range(len(file_list)):
			score = 0
			for line_numbers in data[speaker][file_index]:
				for line_number in line_numbers:
					thestring = lines[file_index][line_number]
					if not args.case:
						thestring = thestring.tolower()
					score += thestring.count(term)
			if args.verbose >= 2:
				print("Score: %s\n" % score)
			results[term][speaker][file_index] = score
	
	out = ""
	out = "speaker"
	for file_name in file_list:
		out += "," + file_name
	out = "\n"
	
	for speaker in range(data):
		out += speaker
		for file_index in range(results[term][speaker]):
			out += "," + str(results[term][speaker][file_index])
		out += "\n"
	
	if args.verbose >= 1:
		print out
	
	
	if args.output:
		fname = "results-" + term + ".csv"
		try:
			outfile = open(fname, "w")
			outfile.write(out)
		finally:
			outfile.close()
		#except IOError:
			#print "Could not open file for writing, sorry.\n"

exit()
		















