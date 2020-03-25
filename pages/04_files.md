# Read & Write Files

1. [General text files](#general-text-files)
2. [JSON files](#json-files)
3. [CSV files](#csv-files)
4. [PDF files (Write only)](#pdf-files-write-only)
5. [Pickle files](#pickle-files)

## General text files
- Open a file using the `with` statement. It creates a scope which will close the opened file automatically after it finishes every command under the scope.

### Reading files (Mode: r)
- **Most used** : Using the file pointer `f` as an iterator

		with open("test.txt", 'r', encoding = 'utf-8') as f:
			for line in r:
				print(line)

- **Option 1** : Using the `read` command to read characters or to read the entire file 

		with open("test.txt", 'r', encoding = 'utf-8') as f:
			t1 = f.read(4)	#  read the first 4 chars
			t2 = f.read(4)	#  read the next 4 char
			t3 = f.read() 	#  read the rest of the file
			t4 = f.read() 	#  further reading returns an empty string

- **Option 2** : Using the `readline` command to read a single line

		with open("test.txt", 'r', encoding = 'utf-8') as f:
			t1 = f.readline()	#  read the first line
			t2 = f.readline()	#  read the second line

- **Option 3** : Using the `readlines` command to read the whole file as a list of its lines which you can then iterate over. 

		with open("test.txt", 'r', encoding = 'utf-8') as f:
			lines = f.readlines() 	#  a list of all the lines in the file
			for line in lines:
				print(line)

### Writing files (Mode: w)
Using the `write` command.

		with open("test.txt", 'w', encoding = 'utf-8') as f:
			f.write("First line\n")
			f.write("Second line\n")
			f.write("\n".join(lines_to_write)) # Write a list of lines

## JSON files

Using the `json` library

### Read-write JSON files
Using the `load` and `dump` commands, respectively

		import json
		data = { "course": { "name": "Python", "term": 1 } }
		with open("data.json", "w") as f: # Write a JSON file
			json.dump(data, f)
		
		with open("data.json", "r") as f: # Read a JSON file
			loaded_data = json.load(f)

### Read-write JSON strings
Using the `loads` (load string) and `dumps` (dump string) commands, respectively.

		import json
		data = { "course": { "name": "Python", "term": 1 } }
		json_string = json.dumps(data, indent=4) # Indent is for pretty printing
		loaded_data = json.loads(json_string)

## CSV files

Using the `csv` library

### Reading CSV files
- Using `csv.reader`

		with open('db.csv', 'r', encoding='utf-8') as csv_file:
			csv_reader = csv.reader(csv_file, delimiter=',')
			column_data = next(csv_reader) # Read the header row
			print(f'Column names are {", ".join(column_data)}')
			for row in csv_reader: # Read the rest of the file
				print(f'{row[0]}-{row[1]}:{row[2]}')

- Using `csv.DictReader` for files with a header row (with column names)

		with open('db.csv', 'r', encoding='utf-8') as csv_file:
			csv_reader = csv.DictReader(csv_file)
			for row in csv_reader:
				print (f'{row["name"]}-{row["faculty"]}-
				{row["department"]}')

- In case the file does not have a header row, 

		with open('db.csv', 'r', encoding='utf-8') as csv_file:
			fieldnames = ['name', 'faculty', 'department']
			csv_reader = csv.DictReader(csv_file, fieldnames=fieldnames)

### Writing CSV files
- Using `csv.writer`, we have two commands. `writerow` is used to write a single row (a single list). Meanwhile, `writerows` is used to write a list of rows (a list of lists). Each row is a line in the csv file.

		header = ['name', 'faculty', 'department']
		data = [['Davies', 'Eng', 'EEE'],
				['Smith','Eng', 'Computing']]
		with open('uni.csv', 'w', newline='\n', encoding='utf-8') as csv_file:
			writer = csv.writer(csv_file, delimiter=',')
			writer.writerow(header)
			writer.writerows(data)

- Using `csv.DictWriter`, similarly we have `writerow` (write a dictionary object as a row) and `writerows` (write a list of dictionary objects as rows).

		data = [{'name': 'Davies', 'faculty': 'Eng', 'dept': 'EEE'},
				{'name': 'Smith', 'faculty': 'Eng', 'dept': 'Comp'}]
		with open('uni.csv', 'w', newline='\n', encoding='utf-8') as csv_file:
			fieldnames = ['name', 'faculty', 'dept']
			writer = csv.DictWriter(csv_file, fieldnames=fieldnames, delimiter = '\t')
			writer.writeheader()
			writer.writerows(data)
			writer.writerow({'name': 'Eugene', 'faculty': 'Med', 'dept': 'Anatomy'})

## PDF files (Write only)
This can be done using fpdf for Python. The tutorial can be found [here](https://pyfpdf.readthedocs.io/en/latest/Tutorial/index.html). 

		from fpdf import FPDF
		def generate_pdf():
		    font = "Arial"
		    pdf = FPDF(orientation='P', unit='mm', format='A4')
		    pdf.add_page()
		    #------------
		    pdf.set_font(font, style="B", size=12)
		    pdf.cell(200, 10, txt="Paper Title", ln=1, align="C")
		    #------------
		    pdf.set_font(font, style="B", size=11)
		    pdf.cell(200, 10, txt="Section 1", ln=1)
		    pdf.set_font(font, style="", size=11)
		    pdf.cell(200, 6, txt="Content 1", ln=1)
		    pdf.multi_cell(0, 6, txt="<Very long text here>")
		    #------------
		    pdf.output("new_folder/sample.pdf")

- `FPDF(orientation, unit, format)` sets up the format of the pdf file.
    - `orientation` could be either `P` or `T` (for portrait and landscape, respectively).
    - `unit` is used as a unit of measures for the following commands. Possible values are `mm`, `cm`, `pt`, `in`.
    - `format` such as `A3`, `A4`, `A5`, `Letter` and `Legal`.
- `pdf.add_page()` adds a new page to the document.
- `pdf.set_font(family, style = '', size = 0)` 
	- `family` could be Courier, Helvetica, Arial, Times, Symbol, ZapfDingbats.
	- `style` is a mixture of `B` (bold), `I` (italic), and `U` (underline). An empty string means a regular font (no decoration).
	- `size` in pt. Default is the current size.
- `pdf.cell(w, h = 0, txt = '', border = 0, ln = 0, align = '')` adds a rectangular cell to the pdf.
	- `w` and `h` are cell width and cell height, respectively.
	- `txt` is the text to be added to the cell.
	- `border` indicates if the cell has borders (1) or not (0).
	- `ln` indicates where the current position should go after the call. Possible values are: (0: to the right) (1: to the beginning of the next line) (2: below)
	- `align` allows to center or align the text. Possible values are `L`, `C`, and `R`.
- `pdf.multi_cell()` has similar arguments as the `cell` function. `multi_cell()` allows printing text with line breaks. They can be automatic (as soon as the text reaches the right border of the cell) or explicit (via the \n character)
- `pdf.output(file_path)` is used for writing the pdf to file.	

## Pickle files
Dump (save) and load (retrieve).

		import pickle
		data = {"A": 12, "B": 15}
		pickle.dump(data, open("filename.pickle", "wb"))
		reloaded_data = pickle.load(open("filename.pickle", "rb"))