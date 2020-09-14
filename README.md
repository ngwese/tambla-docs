# tambla

[tambla](https://github.com/ngwese/tambla) is a semi-generative rhythmic
arpeggiator with bendable playheads

requirements:
- **norns** (20mmdd or later)
- **midi keyboard** - for note input, preferably with velocity sensitivity
- **midi controller** (encouraged) - for mapping performance parameters to dedicated
  controls

pairs well with:
- multi-channel MIDI-CV converters
- (one or more) velocity sensitive polyphonic MIDI sound sources
- delays
- clock synchronized setups

## overview

tambla is tool to explore polyrhythms and syncopation. patterns consist of four
rows. rows have 2-16 triggers with velocity, duration, and chance values per
step. holding down a key generates notes at the given pitch
with the trigger pattern in the first (top most) row. each subsequent key held,
begins generation based on the trigger pattern in next lower row. note generation
begins from the current playhead position instead of the beginning of the row
ensuring the overall rhythmic structure is maintained.

the four playheads scanning each row are synchronized to a common clock.
individual rows can divide down the clock for linear phasing effects or bend the
clock or both. bend values < 1.0 result in the playhead progressing in a
logarithmic fashion (fast then slowing down) where as bend values > 1.0 result
in exponential progression (slow then speeding up).

## interface

the tambla ui consists of three pages in addition to number of mappable
parameters exposed in the _norns_ menu.

![](img/tambla-page-structure.png)

the **play** page is displayed when the script starts. conceptually the pages
are laid out horizontally. several controls are common across all pages:

| control | purpose |
|---------|---------|
| `K1 + K2`   | move left through the pages |
| `K1 + K3`   | move right through the pages |
| `ENC1`      | horizontal selection within the page |
| `K1 + ENC1` | vertical selection within the page |

<hr>

### play page

the **play** page, designated by the `P` in the lower right corner, shows the
four rows of the pattern in the currently selected **slot**. parameters which
affect an entire row can be manipulated on this page.

![](img/tambla-play-m.png)

| control | purpose |
| ------- | ------- |
| `ENC1`  | select the active pattern slot |
| `K1 + ENC1` | select the row to adjust parameters for |
| `K3 + K2` | randomize all rows (key press order is important) |
| `ENC2` | select the row parameter to edit |
| `ENC3` | adjust parameter value |

below each row is a horizontal bar which shows the current playhead position for that row.

_the currently selected row_ is indicated by the small square box to the left of
the row's playhead indicator.

_the currently selected slot_ is indicated by the large number in the middle
right of the display (slot `1` is selected in the image above).

the upper right corner shows the currently selected/editable row parameter.

| code | parameter | purpose |
| ---- | --------- | ------- |
| `b` | bend | playhead time bending. values < 1.0 result in logarithmic progressing, values > 1.0 result in exponential progression |
| `o` | offset | step offset for playhead (not currently visualized) |
| `r` | rate/divisor | divide down the clock, 4 is the minimum and default. 8 is half speed, 16 quarter speed |
| `n` | length | number of steps in the row |

<hr>

### edit page

the **edit** page, designated by the `E` in the lower right corner, allows per
step editing of the triggers in the current pattern.

![](img/tambla-edit-m.png)

triggers are visualized as vertical bars above the playhead indicator. the
height of the bar indicates the trigger _velocity_ (`v`), the width the trigger
_duration_ (`d`), and the brightness the trigger _chance_ (`%`).

just as with the **play** page the currently selected row is indicated by the
small box to the left of the row playhead.

_the currently selected step_ is indicated by the small open rectangle on top of
the playhead bar.

| control | purpose |
| ------- | ------- |
| `ENC1`  | select step within the row |
| `K1 + ENC1` | select the row |
| `K3 + K2` | randomize _the selected row_ (key press order is important) |
| `K2 + K3` | clear _the selected row_ (key press order is important) |
| `ENC2` | adjust step velocity |
| `ENC3` | adjust step duration |
| `K2 + ENC2` | adjust step chance |


**note:** the trigger at a given step is consider off if either the velocity or the chance
values are zero.

<hr>

### macro page
![](img/tambla-macro-m.png)
- copy/paste

## structure

![](img/tambla-event-flow.png)

- slots
- rows

## parameters
