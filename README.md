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

## Build Notes

One feature of this project which makes it more complex than it could have been is the fact that 
there are two indices with different sort orders. This could be handled manually, at the cost of 
increased difficulty when updating the document. I chose instead to handle the data only once, and
generate the two indices programatically. 

`sectionN.csv` are precursor files containing the raw data for each section index: the Item number, 
the Nomenclature, the Figure reference. Run `csv2tex.py` using Python 3, without any arguments, to 
generate the appropriate section indices which will be included into the final document when LaTeX
is run.