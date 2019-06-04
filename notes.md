#css-grid

[cssgrid.io](https://cssgrid.io/) - Wes Bos

[CSS Grid](https://www.youtube.com/playlist?list=PLu8EoSxDXHP5CIFvt9-ze3IngcdAc2xKG) - Wes Bos Youtube

[A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/) - css-tricks

[Implicit vs Explicit](https://css-tricks.com/difference-explicit-implicit-grids/) - css tricks

[CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout) - MDN

- [CSS Grid Layout](#css-grid-layout)
- [Basics](#basics)
- [Properties (grid container)](#properties-grid-container)
  - [Container Alignment](#container-alignment)
- [Properties (grid items)](#properties-grid-items)
  - [Item Alignment](#item-alignment)
- [My Notes](#my-notes)

***

## CSS Grid Layout

- most powerful layout system available in CSS
- aim to completely change the way we design grid-based user interfaces
- created to solve previously hacked website layouts
- 2-dimensional system (columns and rows)
- surpasses Flexbox which was intended for simpler one-dimensional layouts
- works very well with Flexbox

## Basics

grid container - direct parent of all grid items

grid item - direct children of the grid container

grid line - dividing lines (vertical or horizontal) that make up the structure of the grid and reside on either side of the tracks

grid track - space between two adjacent grid lines (columns or rows)

grid cell - space between two adjacent row and two adjacent column lines (single unit of the grid)

grid area - total space surrounded by four grid lines (any number of grid cells)

explicit grid - manually defined with grid-template-rows, grid-template-columns, and grid-template-areas

implicit grid - automatically created when items do not fit onto the explicit grid

## Properties (grid container)

`display: grid | inline-grid`

defines element as a grid container and establishes a grid formatting context for its contents

`grid-template-columns: <track-size> ... | <line-name> <track-size> ...`

`grid-template-rows: <track-size> ... | <line-name> <track-size> ...`

defines the columns and rows of the grid with a space-separated list of values (values represent track-size and spaces between them represent grid lines)

track sizes...

- px, rem , %, etc.
- fr (similar to flex)
- min-content, max-content, auto
- repeat(number | auto-fill | auto-fit, tracks)

fr - unit that allows you to set the size of a track as a fraction of the free space of the grid container (free space calculated after any non-flexible items placed)

`auto-fill` - largest possible number that does not cause the grid to overflow its grid container (if container has a definite/maximal size)

`auto-fit` - behaves the same as auto-fill, except that after placing the grid items any empty repeated tracks are collapsed

grid lines - automatically assigned positive and negative indexes, optional names can be added in brackets (multiple names allowed)

- index: 1 to #tracks + 1
- index -(#tracks + 1) to -1
- [line-name]
- [name1 name2 name3]

defining track sizes

```css
.container {
  grid-template-columns: 40px 50px auto 50px 40px;
  grid-template-rows: 25% 100px auto;
}
```

defining track sizes and line names

```css
.container {
  grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
  grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
}
```

repeat(#, track-sizes/line-names)

minmax(min-size, max-size)

```css
.container {
  grid-template-columns: repeat(3, 20px [col-start]);
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start];
}
```

```css
grid-template-areas:
  "<grid-area-name> | . | none | ..."
  "...";
```

defines a grid template by referencing the names of the grid areas in different cells (syntax provides a visualization of the structure of the grid)

- grid-area-name - the name of a grid area
- . - signifies an empty grid cell
- none - no grid areas are defined

each row needs to have the same number of cells

grid lines are named automatically with areaname-start and areaname-end

`grid-template: none | <grid-template-rows> / <grid-template-columns>`

shorthand for setting the grid template properties (also excepts more complex syntax for setting all three)

`grid: none | <grid-template> | <grid-template-rows> / [ auto-flow && dense? ] <grid-auto-columns>? | <grid-template-rows> / [ auto-flow && dense? ] <grid-auto-columns>?`

shorthand for setting many grid properties

`grid-column-gap: <line-size>`

`grid-row-gap: <line-size>`

specifies the size of the grid lines (like setting the width of the gutters between the columns/rows) (only between columns/rows not outer edges)

`grid-gap: <grid-row-gap> <grid-column-gap>`

shorthand property for grid-row-gap and grid-column-gap (if one is missing, they are set to the same value)

**note** - 'grid-' prefix is being removed from these properties

### Container Alignment

`justify-items: start | end | center | stretch`

Aligns grid items along the inline (row) axis

`align-items: start | end | center | stretch`

Aligns grid items along the block (column) axis

`place-items: align-items / justify-items`

shorthand property for item alignment

`justify-content: start | end | center | stretch | space-around | space-between | space-evenly`

aligns the grid along the inline (row) axis

`align-content: start | end | center | stretch | space-around | space-between | space-evenly`

aligns the grid along the block (column) axis

`place-content: align-content / justify-content`

shorthand property for content alignment

`grid-auto-columns: <track-size> ...`

`grid-auto-rows: <track-size> ...`

specifies the size of any auto-generated grid tracks (implicit grid tracks)

`grid-auto-flow: row | column | row dense | column dense`

controls the grid auto-placement algorithm

***

## Properties (grid items)

`grid-column-start: <number> | <name> | span <number> | span <name> | auto`

`grid-column-end: <number> | <name> | span <number> | span <name> | auto`

`grid-row-start: <number> | <name> | span <number> | span <name> | auto`

`grid-row-end: <number> | <name> | span <number> | span <name> | auto`

determine a grid item's location within the grid by referring to specific grid lines or spans (if no end line value declared, item will span 1 track be default) (use z-index to control their stacking order)

`grid-column: <grid-column-start> / <grid-column-end>`

`grid-row: <grid-row-start> / <grid-row-end>`

shorthand property for grid-column-start + grid-column-end and grid-row-start and grid-row-end, respectively (if no end line value declared, item will span 1 track be default)

`grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>`

gives an item a name to be referenced by a grid-template-areas property, or is an even shorter shorthand for grid-row and grid-column

### Item Alignment

`justify-self: start | end | center | stretch`

aligns grid item inside a cell along the inline (row) axis

`align-self: start | end | center | stretch`

aligns a grid item inside a cell along the block (column) axis

`place-self: auto | <align-self> / <justify-self>`

shorthand property for self alignment

## My Notes

take an element
dice it up into columns and rows (tracks)
take items and lay them out anywhere inside grid
no need for positioning (top, left, right, bottom, position, etc.)
concepts of implicit and explicit grid later
delicate dance between a container
and all of its items (direct children)
grid properties are specified on the container
and this affects the items' positioning
.container {
grid declaration
display: grid;
number of things specified by sizes
different units allowed here
grid-template-columns: 10rem auto 200px 50px;
grid-template-rows: 100px 50px 20rem;
space items apart with gap
grid-gap: 20px;
}
guide to Firefox dev tools
columns/rows = tracks
tracks are not numbered by the actual column/row number itself
but by the lines that start and stop them
will always have a line number one greater than the number of columns/rows
solid lines - explicit grid edge
dark dashed lines - explicit track
light dotted lines - implicit track
dashed diagonal lines - gap
explicit - tracks created clearly and in detail (template),
no room for confusion or doubt
implicit - tracks created through implication,
not clearly expressed
grid-template-x for explicitly created tracks
grid-auto-x for implicitly created tracks (also extra items)
both use a space separated track list
by default - define columns and any extra elements turned into 
implicit rows
grid-auto-flow to change this -> next video

grid-auto-flow - controls how auto-placement algorithm works,
specifically how auto-placed items get flowed into the grid
default is row - auto-places items into rows,
generating new rows as necessary
also column
also dense - fit items where there is space?

pixels (px) are pretty basic and easy to use but don't work well
for dynamic sizing / responsiveness
same with rems, ems, etc.

percentages (%) don't really work adding to 100% because grid-gap is 
not factored into the equation

fractional unit (fr) represent the amount of space left after all
the other elements (and explicit tracks/gaps) are layed out
could think about it as "free space"

.container {
display: grid;
grid-gap: 20px;
border: 10px solid var(--yellow);
grid-template-columns: 100px 100px 1fr;
grid-template-columns: 100px 3fr 1fr;
grid-template-columns: 2fr 3fr 1fr;
grid-template-columns: 1fr 1fr 1fr 1fr;
auto keyword sizes rows/columns to the min size of the
content inside them here
grid-template-columns: auto 1fr auto 1fr;
does nothing because by default the height of the items 
implicitly fills all free space possible
grid-template-rows: 1fr 1fr 1fr 1fr;
}

repeat(# of times, space separated track list)
allows a recurring pattern of rows/columns to be written
in a compact form
grid-template-columns: 1fr 1fr 1fr 1fr;
grid-template-columns: repeat(4, 1fr);
grid-template-columns: repeat(4, 1fr auto);
grid-template-columns: 100px repeat(2, 1fr auto) 50px repeat(2, 3fr);

changing width of single item changes the size of the
entire column (same thing with increasing the size of the
content inside a single item)

instead use item spanning
grid-column: span #
grid-row: span #
item flows into grid naturally but it will be extended to span multiple
rows/columns
other items are pushed around but still flow into the grid naturally

grid-column/grid-row are shorthand properties
explicitly define grid-xxx-start/grid-xxx-end
or utilize grid-xxx: start / end

indices go from 1 to #columns + 1
or -1 to -#columns -1 from opposite end
negative indices do not work for implicit dimensions (usually rows)

use 1 / -1 to take up entire dimension

grid-column-start: 2;
grid-column-end: 5;
grid-column: 2 / 5;
grid-column: 1 / span 2;
grid-column: 1 / -1;
grid-column: 1 / -4;
grid-row: 3 / span 3;

11 cardio

auto-fill - FILLS the row with as many columns (explicit) as it 
can fit, they may be empty but they will still occupy a designated 
space in the row
auto-fit - FITS the CURRENTLY AVAILABLE columns into the space
by expanding them so that they take up any available space (collapses 
the extra columns that would be generated by auto-fill

grid-template-columns: repeat(auto-fill, 150px);
grid-template-columns: repeat(auto-fit, 150px);

minmax specifies a min and max value for track size
grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));

fit-content clamps a given size to an available size
formula: min(maximum size, max(minimum size, argument))
grid-template-columns: fit-content(100px) 150px 150px 150px;

any time there is a grid area with a name
name-start and name-end are valid line names
.container {
display: grid;
grid-gap: 20px;
grid-template-areas:
"x x x x o o o o"
"x x x x o o o o"
"x x x x o o o o"
"x x x x o o o o"
}

.item3 {
grid-column: x-start / o-end;
grid-row-end: x-end;
}

grid-template-areas to name grid areas
use a . for an unnamed area

grid-area: name to assign a grid-area
use media queries to redefine grid-template-areas layout

grid-template-areas:
"sidebar-1  content   sidebar-2"
"sidebar-1  content   sidebar-2"
"footer     footer    footer";

.footer {
grid-area: footer;
}

.item1 {
grid-area: sidebar-1;
}

.item2 {
grid-area: content;
}

.item3 {
grid-area: sidebar-2;
}


@media (max-width: 700px) {
.container {
grid-template-areas:
"content  content   content"
"sidebar-1  sidebar-1   sidebar-2"
"footer     footer    footer";
}
}

name track lines by placing names in brackets between the tracks
when defining them in grid-template-xxx
these names can then be used to reference the lines just as if
you were using the numbers
you can assign multiple names to a single track line

you define the names here as opposed to area-start and area-end 
for defined area names

grid-template-columns: [site-left other-name] 1fr [content-start] 500px [content-end] 1fr [site-right];
grid-template-rows: [content-top] repeat(10, auto) [content-bottom];

grid-column: content-start;
grid-row: content-top / content-bottom;

grid-auto-flow: dense
fills holes created by default flow algorithms
allows "order" of items to be manipulated in order to
fit all of the items as closely as possible

/*
justify-items:
align-items:

justify-content:
align-content:

align-self:
justify-self:

justify-* is row (x) axis
align-* is column (y) axis
*/

place-xxx: align justify 
shorthand for doing both properties
or just place-xxx: both

items mean the item placement inside of the grid spaces
stretch (default), start, end, center

content means the grid placement inside of the container
start(default), end, center, space-around, space-between

self means a single item itself 

justify-items: center;
align-items: center;
place-items: stretch;
justify-content: space-between;
align-content: space-between;
place-content: space-between;

order - rearrange normal order of grid items
default value: 0
higher order means item will be placed further towards the end
messes with screen readers and highlighting text with mouse

19 albums
nested grids
grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));

20 img gall
js
overlap items by placing them on the same column/row
z-index / relative position comes into play 
grid-template-columns: repeat(auto-fill, 100px);

21...css v flex in situations

pefectly centerd
display: grid;
justify-items: center;
align-content: center;

unknown content size
grid-template-columns: repeat(4, auto);


grid-template: 1fr 1fr / 1fr 1fr;
unknown number of items
grid-template-columns: repeat(auto-fit, minmax(50px, 1fr));

rigid bootstrap grid

minmax(0, 1fr)
this makes items not take extra space for their content

css variables or class names can be used for determining span

var(--name, default)
set vars in html style attribute
--name: value;

grid-template-columns: repeat(var(--cols, 12), minmax(0, 1fr));
