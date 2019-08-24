# Ishkur's Guide to Electronic Music v2.5 Dataset:

Structured Data from v2.5 of Ishkur's Guide to Electronic Music. I wanted to preserve the information in the guide, without relying on flash, and have a good dataset to experiment with. Extracted largely manually, if you spot a missing data point, let me know. This is a relatively small dataset, but might be interesting to use as an example in hirarchical community detection, or some other network analysis.

## Data Cleaning Steps:

* Load up http://techno.org/electronic-music-guide/ with dev tools on.
* Click on everything that loads resources (each main page and genre)
* Extract HAR files: https://github.com/azu/har-extractor
* Extract SWF Files texts (tracks): https://github.com/jindrapetrik/jpexs-decompiler
* Extract connections: SWF is a nightmare. Connections extractred manually.

## Data Dictionary:

* `raw_data/`: Contains all swf and txt files from http://techno.org/electronic-music-guide/
* `swf_data/`: Contains extracted text objects from swf files.

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

## See Also:

Version 3.0 of the guide is out now: http://music.ishkur.com/ and has even more data, i'll try to save and structure that too.

## Contributing:

If you make something with this, or find it useful, let me know.
