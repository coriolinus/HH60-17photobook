# HH-60 DA 2408-17 Photo Guide

## What is this?

A -17 inventory is a comprehensive inventory of aircraft components, used whenever control of the 
aircraft is turned over to another party: before and after depot-level maintenance, for example. 

It is a characteristic weakness that even experienced pilots have difficulty identifying the terse
jargon employed. A typical entry, for example, might read as follows:

> **Item No. 5: Electronics Module Assy (M130), 9311431; Qty 1**

Nobody knows what that is or where to find it in order to identify whether or not it is in
fact present in the required quantity.

For the HH-60, there are 13 pages of such entries.

It is therefore traditional to make various cheat-sheets and photo guides to help the poor people 
tasked to perform these inventories. It is equally traditional for the guides to be ancient, 
falling apart, obsolete, and for not quite the same model of aircraft which is actually being 
inventoried. The best of these traditions is that there's always an email address for the creator
near the front, but when you write them to ask for files to update, the response is invariably 
"it's been a long time, dude; I'll take a look on my personal computer, but I really don't know 
where those files went."

I've been tasked to create a new photo reference book, in handy hyperlinked PDF form, so that people
can simply put it on their personal tablets and click happily away. It must also be 
fully and easily usable when printed out and put into a binder. I'd also like to get all
source material permanently online, so that the next guy who's stuck updating the book doesn't have
to do it entirely from scratch the way I am. 

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>

# Editing

## How to Make Changes

Almost all the data which makes up the final book is stored in the .csv files. Images go into the 
Images/ folder. To add an entry, simply add a line in the relevant .csv. To modify an entry, 
likewise modify the relevant line in the .csv. 

.csv files can be edited in any decent text editor, or in Excel.

### Structure of `sectionN.csv`

Section .csv files have four columns. From left to right:

1. Item Number, from the -17.
2. Nomenclature
3. Figure reference. If this column is empty, the text "No Reference" is automaically generated.
4. Additional text. If this column is not empty, it is inserted into field 3 of the generated table,
   immediately after the reference link. It is not hyperlinked. It is mainly used to indicate which 
   portion of a figure reference is indicated.

The figure reference column should contain only a reference ID to a particular figure and nothing else.
If the reference it points to does not exist, `csv2tex.py` will generate a warning; if you continue
to generate the document anyway, LaTeX will generate a nastier warning and possibly fail to compile 
the document.

Contents of columns 2 and 4 are pasted directly into the LaTeX document. This gives you full 
capabilities--there's a reference to a different figure inside one of the captions, for example--but
it means that there are also certain proprieties to be observed. In particular, if after editing 
LaTeX complains a lot about misused characters but everything looks right, check the line against 
the reserved characters at <https://en.wikibooks.org/wiki/LaTeX/Basics#Reserved_Characters> and make
whatever substitutions or escapes are necessary.

The first line of each section is interpreted as the table header.

### Structure of `figures.csv`

`figures.csv` has three columns. From left to right:

1. Figure Reference. This can be any arbitrary text, so long as it is unique in the set of figure 
   references. This is the name which is referred to in `sectionN.csv` to generate the link to the 
   appropriate figure. It does not appear in the output document.
2. Filename. This is in relation to the inside of the `Images` subfolder; a bare filename is 
   sufficient for any files in that folder. For files outside that folder, specifying a relative or
   absolute path is likely to work--but it's a better habit to just put all the images where they're
   supposed to go.
3. Caption. This text appears below the image in the output document. As in the Nomenclature and 
   Additional Text columns in the `sectionN.csv` documents, this is interpreted by LaTeX, so you have
   full access to its formatting capabilities, but you have to respect its reserved characters and 
   escape as necessary.

Unlike `sectionN.csv`, `figures.csv` does not have any headers.

Don't worry about the ordering of figures. One of the tasks of `csv2tex.py` is to generate a 
reasonable figure ordering. In the future, this may be some sort of geometric ordering (if I add 
additional metadata), or "least-backups" ordering designed to maximize the tendency to progress 
forward through the figures. For now, though, it's simpler: each figure is placed in the order in 
which the first reference to it appears. Figures which are not referenced go at the end in no 
particular order. 

## How to Build

You've been tasked to update this document and have no idea what you're looking at or where to start.
Good news! This is much simpler than it may seem.

LaTeX is software which takes semantically-structured input documents and produces nicely-formatted
outputs from them. It does all the heavy lifting in this project of making sure the footnotes line 
up, the figures are numbered correctly, the hyperlinks all work; all that jazz. MiKTeX is a handy
installer for LaTeX on Windows. TeXstudio is a visual environment for working with LaTeX documents
on Windows.

Python is an interpreted programming language. Its only use in this project is to run a small piece
of special purpose software I wrote for this project, `csv2tex.py`, which takes very simple .csv files
and uses them to produce marginally more complex .tex documents. In principle, you could do without
it and produce the .tex documents by hand, but it would mean a lot more typing and correlating. It's
faster and more accurate to have the computer do that kind of work.

### 1. Set up your development environment

1. If on unix/linux/mac:
	2. In a command line: `git clone https://github.com/coriolinus/HH60-17photobook`
	3. Use your preferred package manager to ensure that [Python 3](https://www.python.org/) and
	   [LaTeX](http://latex-project.org/) are installed and available.
2. If on Windows:
	1. Use the sidebar to the right of this page and click `Download ZIP`. Unzip the project somewhere.
	2. Install [MiKTeX](http://miktex.org/), [TeXstudio](http://texstudio.sourceforge.net/), and
	   [Python 3](https://www.python.org/downloads/windows/). 
	3. In TeXstudio, in the Options menu, choose Configure TeXstudio. Go to the Commands tab. Ensure
	   that the commands point to the appropriate utilities. The only ones you really need are LaTeX,
	   pdflatex, and external PDF viewer, but it can't hurt to set more of them. They'll all be found
	   in the miktex/bin subfolder of the place where you installed MiKTeX.

### 2. Make your edits

If you're just substituting an image, the simplest possible thing is to just replace the old image
with the new one in the `Images` folder, keeping the same filename. 

If you're doing anything else, you're going to have to edit the .csv files. Excel is pretty friendly
at this task and will keep you from screwing things up by forgetting to include quotes if they're 
necessary. It will complain every time you try to save, saying that some features are not available,
but just save as .csv anyway and things will be fine.

**Some Excel features are not available.** No formatting in the Excel document will be preserved. 
Formulas won't work. If you want anything like that, look up the LaTeX commands and put them in the
appropriate places.

If you're a little bolder, you can also edit the .csv files in any decent text editor. I'm a fan of
[Notepad++](http://notepad-plus-plus.org/). Just be careful to quote any entry which includes a 
comma, so that you don't screw up the .csv formatting.

Either way you do it, the format of .csv files is fairly simple, and documented above. Just put the 
right things in the right places and everything will work out just fine.

### 3. Compile the document

Open a terminal window into the folder the project is stored in. On Windows, you can do this by 
`shift-Right Click`ing in that folder and selecting `Open command window here`.

In the command window, execute `python csv2tex.py`. This will interpret the .csv files and use them 
to generate the .tex files which will then be generated.

Now, generate the document itself. In unix/linux/mac, this can usually be done by running `pdflatex photobook.tex`
N times, where N is usually 2. In Windows, TeXstudio takes care of that for you. Open `photobook.tex` 
inside TeXstudio, and press `F1`. This will produce a new version of `photobook.pdf` in the working 
folder, and display it on the right side of the screen.

The first time you do this, MiKTeX will inform you that a number of required packages are not 
installed. Just tell it to install each of them from a random repository, and it will fetch them for 
you. 

If you're lucky, things will work perfectly on the first try. In general, a typical editing cycle
involves iterating through edit-compile cycles multiple times, until things look right. Just keep 
poking at it and fixing errors until you're happy with the results.

### 4. Share Alike

Once you've got things set up properly, *do not* just print it out and call it a day. Do the future 
maintainers of the file a favor, and put your version up online as well. Update the frontmatter in
`photobook.tex` to point to your new version's permanent location. I'm obviously using GitHub for 
this purpose, because it's free, convenient, and comes with the full functionality of a real 
[DVCS](http://git-scm.com/book/en/v2/Getting-Started-About-Version-Control), but you can put yours
anywhere, so long as it's avilable to people in general. 

Please include a line in the frontmatter saying you based your version off of mine, with a link to 
this project's GitHub page. Technically, that's required by the license, but really, it's only polite.

## Miscellaneous Notes

One feature of this project which makes it more complex than it could have been is the fact that 
there are two indices with different sort orders. This could be handled manually, at the cost of 
increased difficulty when updating the document. I chose instead to handle the data only once, and
generate the two indices programatically. 

`sectionN.csv` are precursor files containing the raw data for each section index: the Item number, 
the Nomenclature, the Figure reference. Run `csv2tex.py` using Python 3, without any arguments, to 
generate the appropriate section indices which will be included into the final document when LaTeX
is run.

Efficiently adding images is a bit of a bear. The best workflow I've come up with so far:

1. Mess with contrast / exposure / crop / etc. in [Adobe Lightroom](http://www.adobe.com/products/photoshop-lightroom.html)
2. Export to .jpg (possibly to a temporary directory)
3. If markup is necessary:
	3. Import as raster into [Inkscape](https://www.inkscape.org/en/)
	4. Add markup as necessary to hilight relevant parts
	5. Export bitmap as .png
5. Add image definition to `figures.csv`
6. Add relevant figure entries into `sectionN.csv`