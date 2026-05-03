Annotation Guideline: Vehicle & Person Detection

1. Overview
This dataset requires bounding‑box annotations for three object classes:

 car (id=1)
 bicycle (id=2)
 person (id=3)
All annotations must follow the rules below. Consistency and accuracy are essential.

2. Class Definitions
Class	ID	Description
car	1	Sedans (saloon), station wagons (wagon), SUVs, and small pickup trucks (e.g., Toyota Tacoma, Ford Ranger).
bicycle	2	Pedal bicycles only (city bikes, mountain bikes, road bikes, e‑bikes). Motorcycles are not included – do not label them.
person	3	Any human figure (pedestrian, rider, standing person).
Important Exclusions for “car”:
Do NOT label as car:
Vans (passenger vans, cargo vans)
Buses (city bus, coach)
Large trucks (box trucks, articulated lorries, schoolbus)

Small pickup trucks (Toyota Tacoma‑class, similar to mid‑size SUVs) are included because they share the same visual footprint as SUVs/wagons. If in doubt, refer to the lead annotator.

3. General Annotation Rules

3.1 Visibility – “⅔ Rule”
An object must be at least ⅔ visible to be labelled.“Visible” means not cut off by the image border and not hidden behind another object.
If more than ⅓ of the object is missing (occluded or out‑of‑frame), skip it – do not draw a box.
For objects that pass the ⅔ test, draw a tight box around the visible portion only. Never guess the hidden part.
Example: A car enters the frame from the right – if only the front half is visible, leave it out. If the whole car is visible but one wheel is hidden behind a pole, that’s still >⅔ visible and you draw a tight box around the visible car body.

3.2 Bounding‑Box Tightness
Draw the smallest axis‑aligned rectangle that completely encloses the visible object pixels.
The box edges must exactly touch the extreme points (top of head, bottom of wheels, etc.).
No padding or safety margins.
Export coordinates as integers (whole pixels). Avoid long decimal strings.

3.3 Object Completeness & Ambiguity
Label only objects that are clearly identifiable as one of the three classes.
Tiny blobs (<20×20 px on a ~300×170 image) are often indistinguishable – do not label them unless you are >90% certain of the class.
When in doubt, leave it out.

3.4 Overlap & Occlusion – With Image Example
It is normal for a person and a bicycle to overlap, e.g., when a person is riding a bicycle.
Rule: Each bounding box must tightly enclose its own object only, even if this causes boxes to overlap. Do not merge the two boxes.

text
Imagine a side‑view photo of a person pedalling a bicycle.
The person’s torso, arms, and head are visible above the bicycle frame.
The bicycle’s wheels, frame, and handlebars are visible below and around the person.

Correct annotation:
- A blue bounding box (person, id=3) encloses the visible person from the top of the helmet
  down to the thighs, tightly hugging the body – width ~30% of the bicycle’s length.
- A green bounding box (bicycle, id=2) encloses the whole bicycle: wheels, frame,
  pedals, handlebars, but does NOT include the rider’s torso or head.
- The two boxes overlap vertically where the rider’s legs meet the pedals,
  but horizontally the person box is narrower and sits inside the bicycle box’s top region.

Incorrect annotation:
- Drawing a single combined box that covers both person and bicycle.
- Extending the bicycle box upwards to include the rider’s head.
- Labelling the person as “bicycle” or vice‑versa.
A simple diagram (text‑based):

text
        +---+(person box)
        |   |
        |   |
+-------|--|-------+  <- bicycle box (top edge near handlebars)
|       |  |       |
|       |  |       |
|       +--+       |
|                  |
+--+------------+--+   <- bicycle wheels at bottom
Person box (vertical) overlaps the upper part of the bicycle box. Both are tight to their respective objects. When two objects of the same class partially occlude each other (e.g., two persons behind one another), apply the ⅔ rule to each separately. If one person is <⅔ visible, omit it. If both are >⅔ visible, label the visible parts of each.

3.5 Image Borders
If an object is cut by the image edge, apply the ⅔ rule. Label it only if >⅔ of the object lies inside the frame. The bounding box must stop at the image border (x, y, width, height must stay within image dimensions).

3.6 Consistency
All annotators must follow the same interpretation. When unclear, consult the lead annotator for a ruling.
Do not change drawing style partway through a batch (e.g., suddenly switching from integer to floating‑point coordinates).

4. COCO JSON Format Requirements
image_id matching the image’s id.
category_id as defined: car=1, bicycle=2, person=3.
bbox in [x, y, width, height] format (x, y from top‑left corner).
segmentation as empty list [] (no mask annotations).
iscrowd = 0, ignore = 0.
area = width × height (integer).
All annotation id values must be unique and incremental.

5. Quality Checklist Before Submission
Class check: Verify that every bounding box matches the class definition. Especially:
Tall, narrow boxes should almost never be “bicycle” or “car” – they are likely persons.
No large vans, buses, or big trucks mistakenly labelled “car”.

Visibility check: For each box, confirm that >⅔ of the object is visible.

Tightness check: Zoom in – boxes should hug the object without empty space.

Coordinate sanity: No negative values, nothing beyond image dimensions, coordinates are integers.

Small‑boxes audit: Inspect boxes with area < 400 px² (~20×20) – are they truly identifiable? Remove doubtful ones.

Overlap review: In bicycle‑person pairs, ensure two separate boxes are used, each tight to its own object.

Consistency check: Pick random images and verify that the same rules were applied uniformly.

6. Difficult‑Case Decision Table
Scenario	Action
A full‑size bus or van visible	Do not label (excluded from “car”).
A Toyota Tacoma  (Small pickup)	Label as car (id=1).
A large truck (e.g., Ford F‑350)	Do not label.
A person riding a bicycle	Draw two boxes: one person (id=3) around the rider, one bicycle (id=2) around the bicycle. Boxes will overlap.
A motorcycle	Do not label (only pedal bicycles allowed).
Two persons partially hidden behind each other	Label each if >⅔ visible; otherwise skip the more occluded one.
A person cut off at the ankles by the image bottom edge	If >⅔ of the person’s height is visible (head to ankles), label the visible portion. If only half the body is in frame, skip.
A reflection / shadow that looks like a car	Do not label. Only actual physical objects.