# Python
## Overview

This script uses Python’s `turtle` module to draw an artistic representation of Lord Ganesha. It composes the artwork by sequencing simple turtle primitives (move, turn, arc, pen up/down, fill) and layering shapes with different pen sizes and colors.

---

## Notes on key turtle functions used

* `forward()` / `fd()` — move forward.
* `left(angle)` / `right(angle)` — rotate turtle.
* `circle(radius, extent)` — draw arc (extent in degrees). Negative radius flips arc side.
* `penup()` / `pendown()` — stop / start drawing while moving.
* `begin_fill()` / `end_fill()` + `fillcolor()` — create filled shapes.
* `pensize()` — stroke width.
* `color()` — sets pen color (and sometimes fill color if fillcolor not separately set).
* `goto(x,y)` — move to absolute coordinates.
* `setheading(angle)` — set absolute direction.
* `write(text, font=..., align=...)` — write text on the canvas.
* `done()` — finish drawing and keep window open.

---


## Step-by-step (walkthrough of code blocks)

1. **Imports & initial setup**

```python
from turtle import *
import turtle as tur

t = tur.Turtle()
tur.speed(0)
tur.bgcolor("black")
tur.color("gold")
tur.pensize(5)
```

* `from turtle import *` and `import turtle as tur` are both present; you mostly use `tur.` calls. (Tip: keep only one style for clarity.)
* `tur.Turtle()` constructs the drawing turtle. `tur.speed(0)` sets fastest drawing. `bgcolor`, `color`, and `pensize` set the initial canvas color, pen color, and stroke width.

2. **Starting the face outline**

```python
tur.left(60)
tur.fd(50)
tur.left(15)
tur.circle(100,90)
tur.fd(30)
```

* `left()` and `fd()` (forward) position the turtle.
* `circle(100,90)` draws an arc with radius `100` and sweep `90°` (quarter circle). `circle(radius, extent)` — positive radius: center is on the turtle’s left; a negative radius mirrors the arc direction.

3. **Vary pen size & reposition**

```python
tur.pensize(10)
tur.penup()
tur.right(90)
tur.fd(20)
tur.pendown()
```

* `penup()` moves the turtle without drawing; `pendown()` resumes drawing.
* Changing `pensize` creates thicker strokes for emphasis/depth.

4. **Second and third head curves**

```python
tur.right(40)
tur.circle(-50,90)
# ...
tur.color("red")
# move and circle(50,90)
# ...
goto(0,0)
tur.pensize(5)
tur.pendown()
tur.left(30)
tur.fd(120)
tur.circle(60,270)
```

* Multiple arcs with different radii and directions combine to form the complex head outline.
* `goto(x,y)` moves to absolute coordinates (useful to reset the drawing position).

5. **Eyes (large arcs) and eyebrow arcs**

* The code uses a mix of `forward()`, `circle()` and repositioning to shape eye outlines and eyebrows. Eyebrows are thin arcs made with a small `pensize`.

6. **Ears (layered arcs)**

* Several `circle()` calls with different radii and right/left turns stack to form ear shapes and inner details.

7. **Trunk (layered arcs with decreasing pen sizes)**

```python
tur.pensize(10)
tur.forward(50)
tur.circle(100,80)
tur.pensize(9)
tur.circle(150,50)
tur.pensize(7)
tur.circle(100,60)
# etc.
```

* The trunk is created by chaining arcs of different radii and reducing `pensize` stepwise — this produces a tapered, layered trunk effect.

8. **Head top and crown area**

```python
tur.color("red")
goto(-90,290)
tur.right(230)
tur.pendown()
tur.circle(-100,50)
tur.circle(200,20)
# more arcs...
```

* Positioning with `goto()` and drawing compound arcs creates the crown and top head silhouette.

9. **Filled decorations (tilak, crown base, crown jewel, necklace, legs)**

```python
# tilak
tur.goto(0,200)
tur.color("red")
tur.pensize(3)
tur.setheading(90)
tur.forward(15)

# crown (filled semicircle)
tur.goto(-60,250)
tur.color("gold")
tur.begin_fill()
tur.circle(60,180)
tur.end_fill()

# crown jewel
tur.goto(-5,310)
tur.color("red")
tur.begin_fill()
tur.circle(10)
tur.end_fill()

# necklace
tur.goto(-50,50)
tur.color("yellow")
tur.pensize(4)
tur.circle(60,180)
```

* `begin_fill()` / `end_fill()` fill the enclosed shape with current fill color. Use `fillcolor()` to specify fill separately from pen color.

10. **Eyes detailing (pupils and shines)**

```python
tur.goto(-30,120)   # left eye pupil
tur.color("black")
tur.begin_fill()
tur.circle(5)
tur.end_fill()
tur.goto(-28,123)   # shine
tur.color("white")
tur.begin_fill()
tur.circle(2)
tur.end_fill()
# same for right eye
```

* Small filled circles layered inside the eye arcs create pupils and the white shine specular highlight.

11. **Modak (sweet) and ears inner detailing**

* `goto()` to trunk area and draw small filled circle (`color("orange")`) to represent the modak. Ears inner arcs drawn similarly.

12. **Legs (filled circles)**

```python
tur.goto(-60,-150)
tur.color("red")
tur.begin_fill()
tur.circle(30)
tur.end_fill()
# right leg
```

* Two filled circles placed symmetrically form the legs.

13. **Reusable function — `draw_deepa(x,y)`**

```python
def draw_deepa(x, y):
    tur.penup()
    tur.goto(x, y)
    tur.pendown()
    tur.color("brown")
    tur.begin_fill()
    tur.circle(40,180)  # base bowl
    tur.end_fill()

    # Flame
    tur.penup()
    tur.goto(x, y+40)
    tur.color("orange")
    tur.begin_fill()
    tur.circle(15)
    tur.end_fill()
```

* Encapsulates drawing a diya (lamp) so you can place multiple lamps by calling `draw_deepa` with different coordinates. This is a good start towards modularizing the script.

14. **Placing deepas**

```python
draw_deepa(-200, -250)
draw_deepa(0, -250)
draw_deepa(200, -250)
```

* Three calls place lamps evenly across the bottom.

15. **Title & finish**

```python
tur.penup()
tur.goto(0,350)
tur.color("orange")
tur.pendown()
tur.write("✨ Ganpati Bappa Morya ✨", font=("Arial", 24, "bold"), align="center")

done()
```

* `write()` displays the caption. `done()` ends the turtle program and leaves the window open.

---

**How the code draws Ganesha (step-by-step):**

 1. Initialize the turtle window and set background color and pen size.
 2. Use arcs (`circle`) and straight lines (`forward`) to construct the head outline.
 3. Layer arcs with different pen sizes to shape the trunk and add depth.
 4. Place eyes/pupils using absolute coordinates and filled circles for the pupil and shine.
 5. Draw crown, tilak, necklace, and other decorations using `begin_fill()`/`end_fill()`.
 6. Encapsulate repeated elements (like lamps) in a function for reuse.
 7. Add a title and call `done()` to finish.

---

