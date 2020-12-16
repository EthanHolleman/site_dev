---
title: "Data in Vietnam"
date: 2019-11-22T13:49:27-08:00
tags: ['blogs', 'data wrangling']
draft: true
---

## Turing jungles into punchcards

During the early optimistic days of the summer 2020 quarantine I watched 
Ken Burn's fantastic 10 part *18-hour* series on the Vietnam war. It is by far
the most accessible and compressive body of work on the subject. Burn's starts you
off *pre-WWI* so you really get a comprehensive picture of things.

One of the aspects of the war that fascinated me the most was the push by the 
the then Secretary of Defense Robert McNamara to quantify as much of the war
as was computationally possible. One of the most storage intensive of McNamara's
efforts was the Hamlet Evaluation System, which attempted to quantify the degree
to which ~12,000 small, rural Vietnamese villages had been pacified. A RAND
corporation report found the program was producing 90,000 pages of data every
month. More than could have ever been useful.

{{< figure src="/posts/images/doc.png"
title="Example of data produced by the Hamlet Evaluation Program showing change in hamlet classifications over time">}}

And this was the data produced by just one wartime quatification program. Even
if the DoD had the raw 60s era computing power and army of FORTRAN programs
that would be needed to wrangle it all the metric's themselves were questionable
at best. One of the historians interviewed as apart of Burn's series said something 
along the lines of "When you can't measure whats counts, you make what can count
the measure".

I was interested in actually seeing what that data looked like in its raw form.
What where programmers of the era actually looking at and wrangling when some
Army big-wig said "We need to be producing 90,000 pages of data a month". So I
did some googling and dug into a couple documents hosted my the National Archives
to try and get a picture of what Vietnam looked like from the perspective of a
punch card.

## The Phung Hoang Mangement Information System

The degree of documentation relating to the Hamlet Evaluation System that
survives to today is, somewhat unsurprisingly, extremely large. So picking one
out to dive into was adminditly, a highly heurisitic process. 

A came across the [Phung Hoang Mangement Information System](https://catalog.archives.gov/id/17364134), 
PHMIS, (MACV Document Number DAR R33 CM-01A, March 1972) which was later replaced with
the National Police Infrastructure Analysis Subsystem; a database cataloging 
the personal information of Vietnamese who where suspected of or convicted of
aiding communist forces as part of the Hamlet Evaluation Program. From what I
can tell this database and its offspring also have potential ties to the
controversial [Phenoix program](https://en.wikipedia.org/wiki/Phoenix_Program)
a CIA headed counter-insurgency program that amoung other technqiues employed
torture and assassination to identify and kill Viet Cong and Viet Cong 
collaborators.

{{< figure src="/posts/images/flowchart.png"
title="from Phung Hoang Mangement Information System March 1972 Report">}}

## Getting into the data

The PHMIS National Archive entry contains one main data file and some aggregated
technical documentation. 

- `RG330.PHMIS.P6972`: The actual binary data file. Refered to as `RG330`


At first I was a bit lost as to where to start after thumbing through the technical
documentation. At first I naively tried to read `RG330` as UTF-8 but then
soon remembered unicode was not created until the 1980s. 

Thankfully I found the technical specifications summary provided by the National
Archives which had this critical information.

![](/posts/images/tech_summ.png)

The number of records, the length of each record and critically the encoding: 
EBCDIC. At this point I had no idea what EBCDIC encoding was but some quick
googling corrected that. Basically, EBCDIC (Extended Binary Coded Decimal Interchange Code)
was created by IBM in the late 1950s and used a perplexing (see EBCDIC wikipedia page
criticism and humor) eight-bit character encoding for mainframe computers.

{{< figure src="https://upload.wikimedia.org/wikipedia/en/thumb/1/16/Blue-punch-card-front-horiz_top-char-contrast-stretched.png/1920px-Blue-punch-card-front-horiz_top-char-contrast-stretched.png"
title="Example of EBCDIC encoded punch card. ">}}

I almost stopped here, but the Python community came through once again and thanks to
[Thomas Aglassinger](https://pypi.org/user/roskakori/) you can successfully run
the command 

```
pip install ebcdic
```

and have working EBCDIC encodings to work with right in Python. And the
secrets of `RG330` can be revealed in their UTF-8 glory with the Python
snippet below.

```python
import ebcdic
filepath = './RG330.PHMIS.P6972'
data = open(filepath, 'rb').read().decode('cp1141')
```

## Wrangling

The next step was to get the decoded mass of information into something
that could be output to a csv file and would be much easier to work with. The 
technical documentation that let us know `RG330` was EDCDIC encoded also says
that the record length is 319 so my approach was to go with that and pray to
the data-wrangling Gods. 

```python
step = 319
print(data[:step])
```

gives

```
01000005A207000069120H691270122E70125041100002CB  34KKKKK5C12070103001BM########################00000ä    00000ä                           00000ä    00000ä             00000ä    00000ä               00000ä    00000ä               0ä               ########################################################################
```

which as a first attempt does not actually look that bad. The NA documentation notes
that a personaly identifing information in the database has been redacted for public use which
is showing up as the `#` characters. A memo from December 10, 1992 states the
following.

![](/posts/images/memo.png)

I used this to verify the correctness of my naive parsing approach. If everything lines
up, the only characters we should be finding in columns 73-96, 248-271, 272-295
and 296-319 are `#`s.

```python
redacted_base_1 = [(73, 96), (248, 271), (272, 295), (296, 319)]
redacted_base_0 = [(r[0] - 1, r[1]) for r in redacted_base_1]

for redacted_region in redacted_base_0:
    start, end = redacted_region
    assert set(data[start:end]).pop() == "#"
```

Does not produce any assertion errors so lets expand to the whole dataset.

```python
for i in range(0, len(data), 319):
    record = data[i:i+step]
    for redacted_region in redacted_base_0:
        start, end = redacted_region
        assert set(record[start:end]).pop() == "#"
```
Which also does not produce any assertion errors so things are looking pretty
good at this point. The two items of main concern are the `ä` characters and the
large amount of whitespace. Some more investigation revealved the reason for the
whitespace. The document was originally stored in a variable record length format
and was converted to a fixed length by the National Archives at some point. Relevant
documentation in its original photocopy glory below.

![](/posts/images/blanks.png)

The technical documentation also defines the range of each field within a
record that we can use to make the final output file more explicitly
deliminated. A sample of which is shown below. 

![](/posts/images/fields.png)

So now it is just a matter of creating a function that will cut up a record
based on the fields defined in this table. This was pretty boring and involved
some manual formatting. I used the code below to pull out the text from the table
and then went through adding line breaks, removing irrelevant info and correcting
errors in data element names.

```python
import PyPDF2
pdf = open('222.1DP.pdf', 'rb')  
reader = PyPDF2.PdfFileReader(pdf)  
pages = ''.join([reader.getPage(p).extractText() for p in [20, 21, 22, 23]])
print(pages)
```

But after all that I ended up with this beautiful dictionary that can be used
to break up the raw data into a delimitated format. 




















