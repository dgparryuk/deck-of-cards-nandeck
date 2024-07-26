SIMPLE DECK OF CARDS via NANDECK!

This repo does a few things.

1. example on using nandeck macros and file linking to programmatically creating a deck of cards
2. create Tabletop Simulator (TTS) compatible output file to load the deck in-game
3. run nandeck in batch mode, which includes some code to upload files to a remote server and deleting local cached copies to force TTS to always pull the latest versions

Instructions

1. install nanDeck http://www.nand.it/nandeck/ (need at least version 1_23_beta1)
2. install "Card Characters" fonts from http://haroldsfonts.com/portfolio/card-characters/ (free fonts. install both)
3. edit update.sh. see the notes in the file
4. run ./update.sh and answer prompts to delete local images, run nandeck in batch for all decks in folder, and upload to remote server.

I recommend not worrying about options 3 and 4 for now. just install the new font and fire up nandeck and try to validate and build basic-deck.nde.

Basically, we use the data in data-basic-deck.csv to know where to draw the pips for each card.  The coordinates in the file (x and y) assume a grid of 36 x 48. This is defined in deck-commond.nde label, [wid_cells]=36 and [ht_cells]=48.

For each pip, just define the x,y locations and fill out the other columns.

cardtitle= just a name for the card. not really used at the moment
cardvalue= numeric value that is used by the nested loops in basic-deck.nde to know the card range for that card.
x= x coordinate
y= y coordinate
scale= relative scale used to set the size of the pip on the card
angle= angle used in the image directive. currently using 0. haven't extensively tested yet.
flags= flags used in the image directive.  recommend using TRP or TRPV. Use TRPV to flip the pips vertically.
cornervalue= text used for the corner icons. note for the '10' use '=' to use the special '10' in the Card Characters font
imgface=0 or path to image to use for face card images. 0 means don't set a face card image.
yface= fudge value for yposition of the face card graphic. this was a bit experimentally determined.

Philosophy:
the idea I was going for was to be able to have a file (data-basic-deck.csv) that could define the positioning of the pips and pair that with a nandeck nde file with some simple logic to parse the file and re-skin it with new suits/icons.

you can see how this works by comparing basic-deck.nde and kids-fun-deck.nde and seeing how similar they are except for the top info ([suits], [colors], and [deckname]).  they use the same LINK file (data-basic.deck.csv) so the output is identical except for the graphics.

Ideally [suits], [colors], [deckname], and the LINK file would be read from another LINK file. This is on the ToDo list.



dgparryuk notes
i've added a couple of csv's and nde & txt files
extended - will make A,2,3,4,5,6,7,8,9,10,J,Q,K,11,12,0,1 with 4 suits
discworld - will make a pack suitable for ""Cripple Mr Onion""

for the extended & Discworld to show correctly i changed the Macro CORNER_ICON in deck-marcos.nde and created a CORNER_ICON2 which uses the narrow font for 7a, 11 & 12, so also added an if routine to check for 
also moved the corrections from the second branch over to the master branch
the discworld icons were stolen from a PDF of Cripple Mr Onion that i've had for ages but can't find where it came from originally

_