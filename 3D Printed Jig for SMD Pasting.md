# 3D Printed Jig for Solder Pasting Small PCBs

## About

This is a jig for solder pasting small PCB's for SMD parts.
The jig holds a pasting stencil and PCB in alignment.
It is 3D printed plastic.
The repo holds the FreeCad design files.
The design is parametric: you can customize the jig to your PCB.

## Why use this specialized jig instead of a generic jig

If you are only pasting a few boards, then you can use generic jigs.
If you are pasting a few tens of boards, you might find this jig saves effort.
It saves effort in aligning the stencil on the jig,
and in cutting down generic jigs.

The jig has two L-shaped pieces. 
This is similar to the generic jigs you can order from OSHStencil.
The difference here is that one jig has a pocket to hold the stencil
in precisely the right place.
Thus it is easy to align the stencil before taping it to the jig.
Also, if the taped stencil slips, you will know since the stencil no longer fits the pocket.

Another difference with generic jigs is that you don't need to cut down one of two L-shaped pieces: 
it is printed to fit the PCB exactly.

## Status

This is experimental.  Just try it to see if it helps you.

I have tested this design on only two boards.
Thus I have tested that:

  - it is relatively straightforward to parameterize.
  - it works without requiring tweaking due to variances in accuracy in the fabs

I have not tested with a full range of board and stencil thicknesses and sizes.
The parameterization might not be correct.

## How to use

1.  Measure certain distances in your PCB CAD software (e.g. KiCad.)
2.  Enter those distances as parameters in the spreadsheet of the FreeCad design.
3.  Export from FreeCad, both parts.
4.  Slice and print both parts of the jig using your favorite slicer.
5.  Order the boards and stencil (e.g. from OSHPark and OSHStencil.)
6.  Tape the stencil to the jig, in the pocket.  I use masking tape but Kaptan tape might be better.
7.  Use the jig to paste your PCBs.

To use for another board, just clone the FreeCad file, then change parameters in the spreadsheet, and so forth.

## Generic use of L-shaped jigs to solder paste PCBs

Both pieces lay on a work surface.
Both pieces are the thickness of the PCB.
The two pieces press diagonally towards each other, clamping the PCB between them.
The upper-left piece holds the stencil, hinged by tape to the top of the piece.

  - Fix (e.g. pin) the lower-right piece to the work surface.
  - Hinge the stencil up and lay the PCB in the notch of the lower-right piece.
  - Hold the upper-left piece by hand, clamping the PCB.
  - Hinge the stencil down
  - Check alignment
  - Squeegee paste across the stencil
  - Hinge the stencil up. Ensure it separates from the PCB and does not lift it.
  - Slide the upper-left L away
  - Slide the pasted PCB away
  - Repeat

## How this jig differs

This jig is different because it is further custom/specialized to a PCB.

Here the upper-left L-shaped piece is slightly deeper/taller than the PCB.
It has a shallow pocket the size of the stencil.
The pocket is a little deeper than the stencil, to hold the stencil securely.
The stencil then rests flush with the top of the PCB.

Since the pocket is slightly deeper than the stencil depth,
you must use a squeegee that fits inside the stencil (and misses the tape.)

In a generic jig, the tape rises from the jig surface to the top of the stencil,
forming a sloppy hinge.
In this jig, the tap descends very slightly (say from the jig surface to the top of the stencil, forming a more perfect hinge.

## Using the jig

Use the jig just as for a generic jig.
Only the preparation of the jig differs.

### Preparation

1.  Pin the LR body to a work surface.
2.  Place a PCB in the notch.
3.  Slide the UL body against the PCB.
4.  Place the stencil in the pocket of the UL body.
5.  Check the alignment of the stencil holes with the pads on the PCB.
6.  Use one strip of tape to tape the top edge of the stencil to the UL body of the jig.  The tape serves as a hinge.
7   Check alignment again.

The stencil should align unless: 
  - you have made an error in dimensioning
  - or the PCB edge is cut wrong
  - the stencil is not in the pocket
  - some other inaccuracy in fabrication of PCB or stencil

## Customizing the jig

The jig must be customized for each PCB design.

### Preliminaries: measuring the paste bounding box.

The stencil fab doesn't exactly care where the PCB edge is.
The stencil fab creates a stencil having a margin around the bounding box of the pasted pads on the PCB.  This complicates the design of the jig, but the calculations are present in the spreadsheet.

You will however need to measure the bounding box of the pasted pads on the PCB.
Measure the offset from the UL corner of the PCB
to the upper left corner of the bounding box of pasted pads.
Measure the lower right corner of the bounding box of pasted pads.
In other words, measure from the left side of the PCB to the left side of the left-most pasted pad on the PCB, and so forth.

### Preliminaries: stencil thickness

The jig assumes the stencil is 3 or 4 mils thick (roughly 0.08 or 0.1 mm ).
The pocket for the jig is 0.2 mm deep so the top surface of the stencil is about 0.1 mm
below the top surface of the frame.
The thickness of the stencil is not a parameter
but you can adjust the *FrameH* parameter.

### Data flow in the FreeCad design

Main sketches in the beginning of the model tree:

  - PCB rect
  - Stencil rect
  - Frame (jig) edge rect

These are all dimensioned via the spreadsheet in the design.

The sketches are all copied into the pads and pockets of the two pieces/bodies: UL and LR.

Thus to customize the design you only need to change parameters in the spreadsheet.

### Parameters

Dimensions of the PCB :

  - *PCBWidth*
  - *PCBLength*
  - *PCBDepth* (Note currently thin boards .8mm depth.  This affects the height of the jig.)

Distances from PCB UL corner to paste bounding box UL 
corner:

  - *PasteBoundsULX*
  - *PasteBoundsULY*

Distances from PCB UL corner to paste bounding box LR 
corner:
  - *PasteBoundsLRX*
  - *PasteBoundsLRY*

Jig margin, the width of the frame to surround the stencil, somewhat arbitrary
  - *FrameMargin*

Stencil margin, the width of the stencil that surrounds the pasted area.  This is what you chose when ordering the stencil, defaults to 1.5" but I use 0.75" (19.05 mm):
  - *StencilMargin*  

Dimension of LR body.  Somewhat arbitrary.  Choose enough to give you room to work.  The UL and LR bodies together do not form a rectangle; the LR body is larger so it extends away from the pasted area.

  - *LRBodyW*
  - *LRBodyL*

## Tolerances

Whether the jig works depends on several tolerances:

  - the accuracy of your 3D printer
  - the accuracy of the PCB fab
  - the accuracy of the stencil fab
  - the accuracy of your measurments of bounding box of the paste on the PCB.

It seems that the accuracy of the cutting of the edge of a PCB has the least accuracy.
When a board is cut wrong, the stencil might not line up correctly.

The parameters are currently in values having around 0.05 mm precision
(one or two digits of precision after the decimal point.)
You can specify more precision.
But it might not make sense unless the accuracies listed above are to that precision.

A 3D printer generally has accuracy of about 0.05 mm.
But, for example, the accuracy may be less due to gross shrinkage of plastic during cooling.

This design seems to work for pads as small as 0.3 mm.
