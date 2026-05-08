1. OVER VIEW
Over view
This dataset requires polygon segmentation  annotations for three object classes:
  car      (id=1) RED
  building (id=2) GREEN
  animal   (id=3) BLUE
All annotations must follow the rules below. Consistency and accuracy are essential.

2. Class Definitions
Class	ID	Description
car	 1	Sedans (saloon), station wagons (wagon), SUVs, and small pickup trucks.
building 2      houses residentals homes, duplex exceptions;skycrapers.    	
animal	 3	Any animal figure.
Important Exclusions for “car”:Do NOT label as car:
- Vans and buses
- Large trucks
- Motorcycles

3. GENERAL ANNOTATION  GUIDLINES

1. You will annotate images by drawing polygon segmentation masks around each object belonging to the categories “car”, “building”, or “animal”.
2. For cars, trace the full vehicle body including windows, mirrors, and roof, but do not include any passengers or detached parts.
3. For buildings, annotate the entire visible structure from ground level to the highest roof point, excluding any temporary attachments like scaffolding.
4. For every visible instance of an animal (e.g., dogs, cats, or any other living creature), draw a precise polygon that follows its outer contour, including ears, tail, and limbs.
5. If an object is partially occluded by another object, continue the polygon along the inferred visible boundary of the occluded object.
6. Only annotate an object if at least 4/5 of it is visible; if more than 1/5 is cut off by the image edge or heavy occlusion, skip it etirely.
7. For overlapping instances of the same category, draw separate polygons for each distinct object, even if they touch.
8. Each polygon must be a closed loop with vertices placed at every major change in the object’s boundary to ensure high accuracy.
9. After drawing the polygon, the system will automatically generate a bounding box, so you do not need to draw it manually.
10. Do not annotate reflections (e.g., of a car in a window) or images of objects inside pictures or screens.
11. For buildings with complex shapes (e.g., L‑shaped or with protruding towers), create a single polygon that covers the entire connected footprint.
12. If an image contains no objects from the three categories, submit it without any annotations.
13. When multiple animals appear close together, annotate each animal individually, even if their polygons touch.
14. For cars parked partially behind a building or another car, annotate only the visible portion and close the polygon along the contour where it disappears.
15. Ensure every polygon is correctly assigned to the appropriate category ID: 1 for car, 2 for building, 3 for animal in the annotation tool.
16. After finishing each image, review all polygons to confirm they have no self‑intersections and follow the object’s true shape.
17. If you are uncertain whether an object belongs to one of the three categories (e.g., a toy car), mark it as a negative example by leaving it unannotated.