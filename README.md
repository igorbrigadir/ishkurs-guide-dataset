# Ishkur's Guide to Electronic Music Dataset:

Structured Data from v2.5 and v3 of Ishkur's Guide to Electronic Music. I wanted to preserve the information in the guide, without relying on flash or html, and have a good dataset to experiment with. Extracted largely manually, if you spot a missing data point, let me know. This is a relatively small dataset, but might be interesting to use as an example in hirarchical community detection, or some other network analysis. v2.5 and v3 differ quite a lot, but there is some overlap.

# The 2019 v3 HTML Version:

![](v3_gephi_data/genres.svg?sanitize=true)

## Genres: [View](v3_genres.csv)

-|slug|scene|genre|emerged|aka
-|---|---|---|---|---
count|166|166|166|166|166
unique|166|28|166|28|165
top|electroclash|Drum n Bass|US Deep House|early 90s|Hardstep
freq|1|12|1|27|2

## Network: [View](v3_links.csv)

Directed. With time intervals. A genre can split, end or spawn a new one. Genres also have "self loops" for the duration of their "influence". Every edge has a start and end year. Links between genres and years are indicative only.

-|source|target|start|end
-|---|---|---|---
count|352|352|352|352
unique|166|166|49|45
top|experimental|jumpup|1993|2019
freq|9|4|21|145

## Tracks: [View](v3_tracks.csv)

-|slug|scene|genre|year|artist|title
-|---|---|---|---|---|---
count|11317|11317|11317|11317|11317|11317
unique|166|28|166|65|9594|10724
top|synthpop|House|Synthpop|2000|Eat Static|Move Your Body
freq|256|812|256|445|6|6

## Data Cleaning Steps:

* http://music.ishkur.com/ in dev tools to extract json requests.
* Most of the useful things are in json files `gcpoly.json`, `scenelabels.json` in Geo Json format.
* Genres were grouped and sorted manually in `sorted_genres.jsonl`
* Polygons define genre "sections" per year.
* Network is again manually re-constructed from background images. v3 Network is Directed, by year.

## Data Dictionary:

* `v3_genres.csv`
  - `slug`: Slugified genre label, matches `v3_links` and `v3_tracks`.
  - `scene`: Plain text label for the "Scene"
  - `genre`: Plain text label of the genre.
  - `emerged`: Text description of decade. eg: "mid to late 70s"
  - `aka`: Also known as, alternative names for genre.

* `v3_links.csv`
  - `source`: Slugified genre label where an edge starts. 
  - `target`: Slugified genre label where an edge ends. Self loops define genre lifetimes.
  - `start`: Year where the edge starts from the `source`
  - `end`: Year where the edge `target` finishes, or in a self-loop, where the genre "bar" ends.

* `v3_tracks.csv`
  - `slug`: Slugified genre label, matches `v3_links` and `v3_genres`.
  - `scene`: Plain text label for the "Scene"
  - `genre`: Plain text label of the genre.
  - `year`: Year from chart.
  - `artist`: Track Artist.
  - `title`: Track Title.

* `v3_guide.md`: All the genre descriptions turned into markdown. Does not include embedded media, or links. Does not include additional parts (Help, FAQ, How to etc.)

* `v3_json_data`: JSON Files loaded by guide. Coordinates of clickable links.
* `v3_html_data`: HTML Data loaded for each genre and tracklist.
* `preprocessing`: Contains scripts used to process json, extract text, format CSVs etc.

# The 2005 v2.5 Flash Version: 

![](v2.5_gephi_data/genres.svg?sanitize=true)

## Genres: [View](v2.5_genres.csv)

-|genre|node|title|aka|type|scene|decade|description
-|---|---|---|---|---|---|---|---
count|187|187|187|129|187|96|180|187
unique|187|156|185|125|7|15|6|185
top|hardcore|Tribal|Jungle|Tribal|Trance|Hard Dance|90s|Like rats...
freq|1|4|2|4|37|10|121|3

## Network: [View](v2.5_links.csv)

Undirected. A genre can be associated with another, edges are undirected but `source` and `target` nodes are loosely based on the decade.

-|source|target
-|---|---
count|305|249
unique|187|170
top|hiphop|acidhouse
freq|7|4

## Tracks: [View](v2.5_tracks.csv)

Each genre node has a number of representative tracks.

-|genre|number|artist|track
-|---|---|---|---
count|1178|1178|1178|1176
unique|179|11|1151|1157
top|italodisco|1|Dj Funk|Yeah
freq|11|179|5|3

## Data Cleaning Steps:

* Load up http://techno.org/electronic-music-guide/ with dev tools on.
* Click on everything that loads resources (each main page and genre)
* Extract HAR files wiht [Har Extractor](https://github.com/azu/har-extractor) 
`har-extractor techno.org.har`
* Extract SWF Files texts (tracks) with [JPEXS](https://github.com/jindrapetrik/jpexs-decompiler). 
`ffdec.sh -export text "swf_data/breakbeat" "raw_data/breakbeat.swf"`
* Extract connections: SWF is a nightmare. Connections extractred manually.
* Visualisation made in [Gephi](https://gephi.org/). Layout is Yifan Hu Proportional, with some manual adjustments.

## Data Dictionary:

* `v2.5_genres.csv` Data:
  - `genre`: Name of swf and txt file with description.
  - `node`: The visible label on the button, sometimes different to Title.
  - `title`: What loads in description box.
  - `aka`: If available, aka label.
  - `type`: Main section, eg: house, techno, hardcore etc.
  - `scene`: The "scene" the genres are in, eg: "funk".
  - `decade`: 70s, 80s, 90s, etc. Roughly, some nodes are on the border in swf
  - `description`: The text description of the genre.

* `v2.5_links.csv` Data:
  - `source,target`: source and target are based on `genre`. An undirected link between nodes (in the guide, dashed lines link across genres, and solid lines within genres).
  
* `v2.5_tracks.csv` Data:
  - `genre`: matches `genres.csv`
  - `number`: Order in playlist (Does not match the SWF order)
  - `artist`: Track Artist.
  - `track`: Track Title.

* `v2.5_guide.md` Data:
  - This is all the text in the "Tutorial", "Equipment", Credits, Disclaimer etc.

* `v2.5_raw_data/`: Contains all swf and txt files from http://techno.org/electronic-music-guide/
* `v2.5_swf_data/`: Contains extracted text objects from swf files.
* `preprocessing`: Contains scripts used to help clean up decompiled swfs, extract text, format CSVs etc.

# The 2005 v2.0 Flash Version:

This looks like a more sparsely filled in v2.5, "scenes" grouping nodes are missing and there are fewer links, but the main genres are the same.

# The Original v1.0

There's a link to an exe that archive.org does not have an archive for.

## Contributing:

If you make something with this, or find it useful, let me know.
