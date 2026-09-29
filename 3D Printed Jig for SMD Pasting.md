# 3D Printed Jig for Solder Pasting Small PCBs

## About

This jig aligns a stencil with a small PCB during solder-paste application for SMD assembly.
It is made of 3D-printed plastic. The repository contains the FreeCAD design files.
The design is parametric, so you can customize the jig for your PCB.

## Why use this specialized jig instead of a generic jig

For a few boards, a generic jig may be sufficient. For batches of a few dozen,
this design may save setup time by simplifying stencil alignment and eliminating
the need to cut down a generic jig.

The jig has two L-shaped bodies, similar to generic jigs available from OSH Stencils.
The upper-left (UL) body has a pocket that positions the stencil. This makes it
easier to align the stencil before taping it to the jig. If the stencil slips
after taping, it will no longer fit in the pocket.

Unlike a generic jig, the lower-right (LR) body is printed to fit the PCB, so you
do not need to cut it down.

## Status

This design is experimental and has been tested only lightly. Try it to see
whether it works for your setup.

I have tested it on only two boards. In those tests:

- It was relatively straightforward to parameterize.
- It worked without adjustments for variations in fabrication accuracy.

I have not tested a wide range of board and stencil thicknesses or sizes, and the
parameter flow may not work correctly for every design.

## How to use

1. Measure the required distances in your PCB CAD software (for example, KiCad).
2. Enter those measurements in the FreeCAD design spreadsheet.
3. Export both jig bodies from FreeCAD.
4. Slice and print both bodies.
5. Order the PCBs and stencil (for example, from OSH Park and OSH Stencils).
6. Tape the stencil into the pocket. I use masking tape; Kapton tape may work better.
7. Use the jig to apply solder paste to your PCBs.

To make a jig for another board, copy the FreeCAD file and update the spreadsheet
parameters.

## Using generic L-shaped jigs to solder paste PCBs

Both bodies rest on a work surface and are as thick as the PCB. They press
diagonally toward each other to clamp the PCB between them. The stencil is taped
to the top of the UL body, forming a hinge.

- Secure the LR body to the work surface, for example with a pin.
- Lift the stencil and place the PCB in the notch of the LR body.
- Hold the UL body by hand to clamp the PCB.
- Lower the stencil and check its alignment.
- Squeegee solder paste across the stencil.
- Lift the stencil, ensuring that it separates from the PCB without lifting it.
- Slide the UL body away, then remove the pasted PCB.
- Repeat.

## How this jig differs

This jig is customized for a specific PCB.

The UL body is slightly deeper (taller) than the PCB and has a shallow pocket
that matches the stencil. The pocket is slightly deeper than the stencil, so
the stencil sits flush with the top of the PCB. The pocket holds the stencil in
alignment with the PCB. With a generic jig, you must align the stencil manually.

Because the pocket is slightly deeper than the stencil, use a squeegee narrow
enough to fit inside the stencil without hitting the tape. With a generic jig,
you can use a squeegee wider than the stencil.

In a generic jig, the tape rises from the jig surface to the top of the stencil,
which can make a loose hinge. In this jig, the tape descends slightly from the
jig surface to the top of the stencil, forming a tighter hinge.

## Using this jig

Only the jig-preparation steps differ. Apply solder paste as you would with a
generic jig.


### Preparation

1. Pin the LR body to a work surface.
2. Place a PCB in the notch.
3. Slide the UL body against the PCB.
4. Place the stencil in the UL body's pocket. With a generic jig, this step
  requires manual alignment.
5. Check that the stencil apertures align with the PCB pads.
6. Use one strip of tape to attach the stencil's top edge to the UL body. The
  tape acts as a hinge.
7. Check the alignment again.

If the stencil does not align, check for:

- Incorrect dimensions.
- An inaccurately cut PCB edge.
- A stencil that is not seated in the pocket.
- Other inaccuracies in the PCB or stencil fabrication.

## Customizing the jig

Customize the jig for each PCB design.

### Preliminaries

#### Measuring the paste bounding box.

The stencil manufacturer positions the stencil relative to the bounding box of
the paste apertures, not the PCB edge. The stencil includes a margin around this
bounding box. This complicates the jig design, so the spreadsheet includes the
necessary calculations.

Measure the paste-area bounding box on the PCB. Record the offset from the PCB's
upper-left (UL) corner to the UL corner of that bounding box, and measure the
lower-right (LR) corner as well. For example, measure from the PCB's left edge
to the left edge of the leftmost paste aperture, and make the corresponding
measurements for the other edges.

#### Stencil thickness

The jig assumes a stencil thickness of 3 or 4 mil (roughly 0.08 or 0.1 mm).
The pocket is 0.2 mm deep, placing the stencil's top surface about 0.1 mm below
the frame's top surface. Stencil thickness is not a separate parameter, but you
can adjust *FrameH*.

#### Coordinate system

The coordinate-system origin is at the PCB's UL corner. This matters only if you
are reading the spreadsheet formulas or making substantial changes to the
FreeCAD design.

### Data flow in the FreeCad design

The main sketches near the beginning of the model tree are:

- PCB rect
- Stencil rect
- Frame (jig) edge rect

The design spreadsheet controls the dimensions of these sketches.

The sketches are used to create the pads and pockets in the two bodies, UL and LR.

To customize the design, change the spreadsheet parameters.

### Important parameters changed for each PCB board

PCB dimensions:

- *PCBWidth*
- *PCBLength*
- *PCBDepth* (Currently set for thin boards that are 0.8 mm thick. This affects
  the jig height.)

Distances from the PCB's UL corner to the paste bounding box's UL corner:

- *PasteBoundsULX*
- *PasteBoundsULY*

Distances from the PCB's UL corner to the paste bounding box's LR corner:

- *PasteBoundsLRX*
- *PasteBoundsLRY*

### Secondary parameters, changed less often

Jig margin: the width of the frame around the stencil. This is somewhat
arbitrary and rarely needs to change.

*FrameMargin*

Stencil margin: the width of the stencil surrounding the paste area. Set this
when ordering the stencil. The default is 1.5 in; I use 0.75 in (19.05 mm).
Change this parameter only if you order a stencil with a different margin.

*StencilMargin*

LR body dimensions: these are somewhat arbitrary; choose values that leave you
enough room to work. The UL and LR bodies do not form a rectangle together. The
LR body extends beyond the paste area. These dimensions rarely need to change.

- *LRBodyW*
- *LRBodyL*

## Tolerances

Jig performance depends on several tolerances:

- 3D-printer accuracy.
- PCB-fabrication accuracy.
- Stencil-fabrication accuracy.
- The accuracy of your measurements of the paste-area bounding box.

PCB edge cutting appears to be the least accurate step. If the board edge is cut
incorrectly, the stencil may not align.

The parameters currently use approximately 0.05 mm precision (one or two digits
after the decimal point). You can enter more precise values, but doing so may
not help unless the fabrication and measurement processes are equally precise.

A 3D printer is generally accurate to about 0.05 mm. Accuracy may be worse,
for example, if the plastic shrinks significantly as it cools.

This design appears to work with pads as small as 0.3 mm.
