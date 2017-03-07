# How CSS Works

## Overview
At the heart of CSS are the [&sect;8 Box model](https://www.w3.org/TR/CSS22/box.html) and the [&sect;9 Visual formatting model](https://www.w3.org/TR/CSS22/visuren.html). These models consist of a set of rules that describe how the browsers represent documents *visually* (as opposed to how documents are represented/encoded in a computer&rsquo;s memory).

## About the Reset Stylesheet (`reset.css`)
### What is it?
A reset stylesheet is a stylesheet that *reinitializes* each CSS property (typically except `display`). Alternatively, a reset stylesheet is a stylesheet that sets each CSS property to (a web author&rsquo;s) preferred defaults.
### Why is it needed?
As stated in [&sect;6.4 The cascade](https://www.w3.org/TR/CSS22/cascade.html#cascade) of CSS 2.2, &ldquo;Conforming user agents must apply a default style sheet (or behave as if they did).&rdquo;. The intention here is to give some basic styling to documents for which no accompanying style rules are provided. Thus, due to browsers&rsquo;s default styles, some CSS properties will no longer be set to their initial values. But for web authors who *do* provide their own styles, browsers&rsquo;s default styles may introduce unwanted and unexpected styling. Furthermore, because there&rsquo;s no guarantee that default stylesheets are consistent across browsers, resorting to default styles may result in styling inconsistencies between browsers.
### Why do reset stylesheets tend not to reinitialize `display`?
As stated in [&sect;9.2.4 The 'display' property](https://www.w3.org/TR/CSS22/visuren.html#display-prop) of CSS 2.2, &ldquo;&hellip;although the initial value of `display` is `inline`, rules in the user agent&rsquo;s default style sheet may override this value.&rdquo; `display` defaults just happen to be the one property where there is pretty much universal agreement on which HTML element should be set to which values; `div`s, `p`s, etc., should be `block`, `li` should be `list-item`, `head` and its descendants should be `none`, etc.

## Box model ([&sect;8 Box model](https://www.w3.org/TR/CSS22/box.html))
The CSS box model describes the boxes (rectangular in shape by default) that are generated for elements in the document tree (and subsequently laid out according to the visual formatting model).
### Box type
Each box in the box model is of one of the following three types:

1. Block-level
2. Inline-level
3. Table-level

A box&rsquo;s type determines how it is (or can be) sized and to which set of formatting rules it obeys.

<dfn>Block-level boxes</dfn> are boxes that, under &ldquo;normal&rdquo; circumstances, obey a set of formatting rules called a block formatting context. They are generated from <dfn>block-level elements</dfn>&mdash;elements whose `display` property is set to `block` (in HTML, the `html`, `body`, `article`, `section`, `nav`, `aside`, `h1`, `h2`, `h3`, `h4`, `h5`, `h6`, `hgroup`, `header`, `footer`, `address`, `p`, `hr`, `pre`, `blockquote`, `ol`, `ul`, `dl`, `dt`, `dd`, `figure`, `figcaption`, `main`, `div`, `form`, `fieldset`, `legend`, `details`, `summary`, and `menu` elements), `list-item` (in HTML, the `li` element), or `table` (in HTML, the `table` element).

<dfn>Inline-level boxes</dfn> are boxes that, under &lsquo;normal&rdquo; circumstances, obey a set of formatting rules called an inline formatting context. They are generated from <dfn>inline-level elements</dfn>&mdash;elements whose `display` property is set to `inline` (in HTML, the `a`, `em`, `strong`, `small`, `s`, `cite`, `q`, `dfn`, `abbr`, `data`, `time`, `code`, `var`, `samp`, `kbd`, `sub`, `sup`, `i`, `b`, `u`, `mark`, `span`, `br`, `wbr`, `ins`, `del`, `output` elements) `inline-block` (in HTML, the `marquee`, `input`, `textarea`, `select`, `button`, `meter`, and `progress` elements), or `inline-table` (in HTML, no element is initialized to `inline-table`).

<dfn>Table-level boxes</dfn> are boxes that obey table formatting contexts. They are generated from <dfn>table-level elements</dfn>&mdash;elements whose `display` property is set to `table-row-group` (in HTML, the `tbody` element), `table-header-group` (in HTML, the `thead` element), `table-footer-group` (in HTML, the `tfoot` element), `table-row` (in HTML, the `tr` element), `table-column-group` (in HTML, the `colgroup` element), `table-column` (in HTML, the `col` element), `table-cell` (in HTML, the `td` and `th` elements), or `table-caption` (in HTML, the `caption` element).

### Box structure
#### Content, padding, border, and margin areas and edges
Each box consists of a content area, rectangular in shape by default, that contains either text, zero or more descendant boxes, or replaced data (e.g., an image). The content area is *optionally* framed by&mdash;from innermost to outermost&mdash;a padding area, and/or a border area, and/or a margin area.

The border area is analogous to a picture frame; its purpose is to provide decorative surrounding to the content area. The padding area is analogous to picture matting; its purpose is to provide asthetic spacing between the content and the border. The margin area can be thought of as interbox spacing; its purpose is to create spacing between sibling boxes and between siblings and their parent (containing) box.

The outermost pixel elements of each box area is known as that box&rsquo;s edge. Thus we have the content (aka inner) edge, which delimits the content area, the padding edge, which delimits the padding area, the border edge, which delimits the border area, and the margin (aka outer) edge, which delimits the margin area.

The padding, border, and margin areas each consist of four individual segments: the top segment, the right segment, the bottom segment, and the left segment. In order that the edges of the four segments are equal in length, segments are trapezoidal, *not* rectangular, in shape.

#### Content area width and height
The content area width is defined as the number of content pixels running horizontally from the content area&rsquo;s left edge to the content area&rsquo;s right edge, inclusive. A content area&rsquo;s width is, inter alia, controlled by the `width` property.

The content area height is defined as the number of content pixels running vertically from the content area&rsquo;s top edge to the content area&rsquo;s bottom edge, inclusive. A content area&rsquo;s height is, inter alia, controlled by the `height` property.

#### Padding width
The width of each segment of the padding area is defined as the number of padding pixels running perpendicularly from a content edge to its respective padding edge, excluding the content edge itself. The widths of the top, right, bottom, and left segments of the padding area are individually represented by the properties `padding-top`, `padding-right`, `padding-bottom`, and `padding-left`. All four padding area segments are collectively represented by the `padding` property.

#### Border width
The width of each segment of the border area is defined as the number of border pixels running perpendicularly from a padding edge (if extant, otherwise a content edge) to its respective border edge, excluding the padding edge (or content edge) itself. The widths of the top, right, bottom, and left segments of the border area are represented by the `border-top-width`, `border-right-width`, `border-bottom-width`, and `border-left-width` properties respectively.

#### Margin width
The width of the margin area, i.e., the number of margin pixels running perpendicularly from the border edge (if extant, otherwise the padding edge, if extant, otherwise the content edge), is represented by the `margin` property. Furthermore, with widths of the top, right, bottom, and left segments of the margin area are individually represented by the properties `margin-top`, `margin-right`, `margin-bottom`, and `margin-left` respectively, and can thus be individually set.



## Visual formatting model ([&sect;9 Visual formatting model](https://www.w3.org/TR/CSS22/visuren.html))


### Block formatting context ([&sect;9.4.1 Block formatting contexts](https://www.w3.org/TR/CSS22/visuren.html#block-formatting))
A block formatting context is a set of formatting rules that apply to block-level boxes.

In a block formatting context, boxes are laid out one after the other, vertically, in source order, beginning at the top-left corner of the inner (content) edge of their containing block. Each box&rsquo;s left outer (margin) edge touches the left inner (content) edge of its containing block (`001BFM.html`, `001BFM.css`). This is true even in the presence of floats (although a box&rsquo;s *line* boxes may shrink due to the floats), unless the box establishes a new block formatting context (in which case the box itself may become narrower due to the floats).

The vertical distance between two sibling boxes is determined by the `margin-top` and `margin-bottom` (`002BFM.html`, `002BFM.css`).

Definition: Suppose, hypothetically, that the adjoining margins of two or more boxes (which might or might not be siblings) combine to form a single margin. Margins that combine in this way are said to <dfn>collapse</dfn>, and the resulting combined margin is called a <dfn>collapsed margin</dfn>. When two or more margins collapse, the resulting margin width is the maximum of the collapsing margins&rsquo;s widths. In the case of negative margins, the maximum of the absolute values of the negative adjoining margins is deducted from the maximum of the positive adjoining margins. If there are no positive margins, the maximum of the absolute values of the adjoining margins is deducted from zero. [&sect;8.3.1 Collapsing margins](https://www.w3.org/TR/CSS22/box.html#collapsing-margins)

Vertical margins between adjacent boxes collapse (`003BFM.html`, `003BFM.css`).

## Inline formatting context ([&sect;9.4.2 Inline formatting contexts](https://www.w3.org/TR/CSS22/visuren.html#inline-formatting))
An inline formatting context is established by a block container box that contains no block-level boxes. In an inline formatting context, boxes are laid out one after the other horizontally, in source order, beginning at the top-left corner of the inner (content) edge of their containing block.

Horizontal margins, borders, and padding are respected between these boxes.

The rectangular area that contains the boxes that form a line is called a line box.
