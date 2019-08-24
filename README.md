# Ishkur's Guide to Electronic Music v2.5 Dataset:

Structured Data from v2.5 of Ishkur's Guide to Electronic Music. I wanted to preserve the information in the guide, without relying on flash, and have a good dataset to experiment with. Extracted largely manually, if you spot a missing data point, let me know. This is a relatively small dataset, but might be interesting to use as an example in hirarchical community detection, or some other network analysis.

# Genres: [View](genres.csv)

~|node|title|aka|type|group|decade|file
---|---|---|---|---|---|---|---
count|187|187|128|187|96|180|187
unique|156|183|127|7|15|6|187
top|Tribal|Hardcore|Tribal|Trance|Hard Dance|90s|hardcore
freq|4|2|2|37|10|121|1

# Network: [View](links.csv)

A genre can be associated with another, edges are undirected but `source` and `target` nodes are loosely based on the decade

~|source|target
---|---|---
count|188|8
unique|187|8
top|house|dub
freq|2|1

Data is incomplete.

# Tracks: [View](tracks.csv)

Each genre node has a number of representative tracks.

~|file|number|artist|track
---|---|---|---|---
count|1178|1178.0|1178|1176
unique|179| |1151|1157
top|italodisco| |Dj Funk|Yeah
freq|11| |5|3
mean| |4.136672325976231| | 
std| |2.3338584552859998| | 
min| |1.0| | 
25%| |2.0| | 
50%| |4.0| | 
75%| |6.0| | 
max| |11.0| | 


## Data Cleaning Steps:

* Load up http://techno.org/electronic-music-guide/ with dev tools on.
* Click on everything that loads resources (each main page and genre)
* Extract HAR files: https://github.com/azu/har-extractor
* Extract SWF Files texts (tracks): https://github.com/jindrapetrik/jpexs-decompiler
* Extract connections: SWF is a nightmare. Connections extractred manually.

## Data Dictionary:

* `genres.csv` Data:
  - `node`: The visible label on the button, sometimes different to Title.
  - `title`: What loads in description box.
  - `aka`: If available, aka label.
  - `type`: Main section, eg: house, techno, hardcore etc.
  - `group`: The "group" the genres are in, eg: "funk".
  - `decade`: 70s, 80s, 90s, etc. Roughly, some nodes are on the border in swf
  - `file`: Name of swf and txt file with description.
  - `description`: The text description of the genre.

* `edges.csv` Data:
  - `source,target`: source and target are based on `file` name without extension. An undirected link between nodes (in the guide, dashed lines link across genres, and solid lines within genres).
  
* `tracks.csv` Data:
  - `file`: matches `genres.csv`
  - `number`: Order in playlist (Does not match the SWF order)
  - `artist`: Artist
  - `track`: Track Title

* `guide.md` Data:
  - This is all the text in the "Tutorial", "Equipment", Credits, Disclaimer etc.

* `preprocessing`: Contains scripts used to help clean up decompiled swfs.
* `raw_data/`: Contains all swf and txt files from http://techno.org/electronic-music-guide/
* `swf_data/`: Contains extracted text objects from swf files.

## See Also:

Version 3.0 of the guide is out now: http://music.ishkur.com/ and has even more data, i'll try to save and structure that too.

## Contributing:

If you make something with this, or find it useful, let me know.
