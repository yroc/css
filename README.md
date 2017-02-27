# How CSS Works

## The Visual Formatting Model
The visual formatting model (VFM) is a set of rules that describe how the browser *visually* represents a document (as opposed to how a document is represented in memory).

The important precursor to the VFM is the box model. The basic idea is that document elements (usually we&rsquo;re talking about HTML elements  of an HTML document) are visually manifested as rectangular boxes (of course there are many details regarding the a box's structure, but that's the basic idea).

Next there's the block formatting context (BFC) and inline formatting context (IFC), which are rules that determine boxes&rsquo; dimensions (width and height) and how the boxes are laid out relative to one another.

An important concept in the VFM is that of containing block. Many box positions and sizes are calculated with respect to the edges of a rectangular box called a containing block. In general, generated boxes act as containing blocks for descendant boxes; we say that a box "establishes" the containing block for its descendants, and each box is given a position with respect to its containing block. Note: This doesn't imply that boxes are necessarily confined by their containing block; they may "overflow."

Of course, the devil is in the details; it's nice to have this overall perspective, but you won't feel you understand any of this without knowing all the details -- the actual sizing and layout rules. Fasten your safety belt -- it's a long and bumpy ride!