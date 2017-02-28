# How CSS Works

## The Visual Formatting Model
The visual formatting model (VFM) is a set of rules that describe how the browser *visually* represents a document (as opposed to how a document is represented in memory).

The important precursor to the VFM is the box model. The basic idea is that document elements (usually HTML elements  of an HTML document) are visually manifested as rectangular boxes (of course there are many details regarding the a box's structure, but that's the basic idea).

Next there's the block formatting context (BFC) and inline formatting context (IFC), which are rules that determine boxes&rsquo; dimensions (width and height) and how the boxes are laid out relative to one another.

An important concept in the VFM is that of containing block. Many box positions and sizes are calculated with respect to the edges of a rectangular box called a containing block. In general, generated boxes act as containing blocks for descendant boxes; we say that a box "establishes" the containing block for its descendants, and each box is given a position with respect to its containing block. Note: This doesn't imply that boxes are necessarily confined by their containing block; they may "overflow."

Of course, the devil is in the details; it's nice to have this overall perspective, but you won't feel you understand any of this without knowing all the details -- the actual sizing and layout rules. Fasten your safety belt&mdash;it's a long and bumpy ride!

## About the Reset Stylesheet (`reset.css`)
As stated in [&sect;6.4 The cascade](https://www.w3.org/TR/CSS22/cascade.html#cascade) of CSS 2.2, &ldquo;Conforming user agents must apply a default style sheet (or behave as if they did).&rdquo;. The purpose is to give the HTML author (particularly a novice) some basic styles to make a document shall we say minimally presentable. But for the experienced developer, default styles may be more of a hindrance than a help, as it may introduce unwanted styling.

A better approach for the experienced developer is to start with a styling blank slate (i.e., all properties set to their *initial values*). Then the experienced developer can add just what styling he or she desires. This is accomplished by introducing a user-defined stylesheet whose sole purpose is essentially to *cancel out* browsers&rsquo;s default styling. This user-defined stylesheet is appropriately called `reset.css`.

The only default style that `reset.css` does *not* affect is the `display` property. As stated in [&sect;9.2.4](https://www.w3.org/TR/CSS22/visuren.html#display-prop) of CSS 2.2, &ldquo;&hellip;although the initial value of `display` is `inline`, rules in the user agent&rsquo;s default style sheet may override this value.&rdquo; It is the expectation all developers that certain elements, such as `div` and `p` generate block-level boxes (`display: block`), certain elements, especially `li`, generate block-level boxes with an auxilliary marker box, and certain elements, especially `head` and its descendants, generate no box at all. It would be silly and rather pointless to reset these elements to display as inline-level boxes.

### Block formatting context
In a block formatting context, boxes are laid out one after the other, vertically, beginning at the top-left corner of their containing block.
