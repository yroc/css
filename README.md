# How CSS Works

## The Visual Formatting Model ([&sect;9 Visual formatting model](https://www.w3.org/TR/CSS22/visuren.html))
The visual formatting model (VFM) is a set of rules that describe how the browser *visually* represents a document (as opposed to how a document is represented in memory).

The important precursor to the VFM is the box model. The basic idea is that document elements (usually HTML elements  of an HTML document) are visually manifested as rectangular boxes (of course there are many details regarding the a box's structure, but that's the basic idea).

Next there's the block formatting context (BFC) and inline formatting context (IFC), which are rules that determine boxes&rsquo; dimensions (width and height) and how the boxes are laid out relative to one another.

An important concept in the VFM is that of containing block. Many box positions and sizes are calculated with respect to the edges of a rectangular box called a containing block. In general, generated boxes act as containing blocks for descendant boxes; we say that a box "establishes" the containing block for its descendants, and each box is given a position with respect to its containing block. Note: This doesn't imply that boxes are necessarily confined by their containing block; they may "overflow."

Of course, the devil is in the details; it's nice to have this overall perspective, but you won't feel you understand any of this without knowing all the details -- the actual sizing and layout rules. Fasten your safety belt&mdash;it's a long and bumpy ride!

## About the Reset Stylesheet (`reset.css`)
### What is it?
A stylesheet that *reinitializes* all CSS properties (typically except `display`). Alternatively, a stylesheet that sets all CSS properties to *baseline* values&mdash;property values that the experienced developer thinks ought to be the defaults.
### Why is it needed?
As stated in [&sect;6.4 The cascade](https://www.w3.org/TR/CSS22/cascade.html#cascade) of CSS 2.2, &ldquo;Conforming user agents must apply a default style sheet (or behave as if they did).&rdquo;. The intention here is to give some basic styling to HTML documents for which no accompanying style rules are provided. Thus, due to browsers&rsquo; default styles, some CSS properties will no longer be set to their initial values. But for *experienced* web authors who provide their own styles, the browsers&rsquo; default styles are typically more of a nuisance than anything&mdash;they may introduce unwanted styling as well as styling inconsistencies between browsers (supposing different browsers provide different default style rules).
### Why do reset stylesheets tend not to reinitialize `display`?
As stated in [&sect;9.2.4 The 'display' property](https://www.w3.org/TR/CSS22/visuren.html#display-prop) of CSS 2.2, &ldquo;&hellip;although the initial value of `display` is `inline`, rules in the user agent&rsquo;s default style sheet may override this value.&rdquo; `display` defaults just happen to be one property where there is pretty much universal agreement: `div`s, `p`s, etc., should be `block` by default, `head` and its descendants should be `none` by default, etc. Thus, there&rsquo;s no need to reset them.

## Box model ([&sect;8 Box model](https://www.w3.org/TR/CSS22/box.html))
The CSS box model describes the rectangular boxes that are generated for elements in the document tree and laid out according to the visual formatting model.
### Box structure
Each box has an innermost content area that contains its corresponding element&rsquo;s *data* (e.g., text, images) and descendant boxes. The content area is optionally surrounding by three rectangular frame areas. In order from inner to outer: the padding area, the border area, and the margin area.

## Block formatting context ([&sect;9.4.1 Block formatting contexts](https://www.w3.org/TR/CSS22/visuren.html#block-formatting))
In a block formatting context, boxes are laid out one after the other, vertically, in source order, beginning at the top-left corner of the inner (content) edge of their containing block. Each box&rsquo;s left outer (margin) edge touches the left inner (content) edge of its containing block (`001BFM.html`, `001BFM.css`). This is true even in the presence of floats (although a box&rsquo;s *line* boxes may shrink due to the floats), unless the box establishes a new block formatting context (in which case the box itself may become narrower due to the floats).

The vertical distance between two sibling boxes is determined by the `margin-top` and `margin-bottom` (`002BFM.html`, `002BFM.css`).

Definition: Suppose, hypothetically, that the adjoining margins of two or more boxes (which might or might not be siblings) combine to form a single margin. Margins that combine in this way are said to <dfn>collapse</dfn>, and the resulting combined margin is called a <dfn>collapsed margin</dfn>. When two or more margins collapse, the resulting margin width is the maximum of the collapsing margins&rsquo;s widths. In the case of negative margins, the maximum of the absolute values of the negative adjoining margins is deducted from the maximum of the positive adjoining margins. If there are no positive margins, the maximum of the absolute values of the adjoining margins is deducted from zero. [&sect;8.3.1 Collapsing margins](https://www.w3.org/TR/CSS22/box.html#collapsing-margins)

Vertical margins between adjacent boxes collapse (`003BFM.html`, `003BFM.css`).

## Inline formatting context ([&sect;9.4.2 Inline formatting contexts](https://www.w3.org/TR/CSS22/visuren.html#inline-formatting))
An inline formatting context is established by a block container box that contains no block-level boxes. In an inline formatting context, boxes are laid out one after the other horizontally, in source order, beginning at the top-left corner of the inner (content) edge of their containing block.

Horizontal margins, borders, and padding are respected between these boxes.

The rectangular area that contains the boxes that form a line is called a line box.
