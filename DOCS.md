# Documentation

## .mdl Programs:

An .mdl program consists of a series of 0 or more statements describing the creation of shapes, followed by a `draw` command (see below).  
Shapes can be created through the use of primitive shape constructors or transformation functions, and can be assigned to variables to reference later for either rendering or composing new shapes using the transformation functions.

Example Program:

```
firstShape = createCircle(5, red, outline);
draw(firstShape);
```

## Draw Command:

- Specify a shape "`toDraw`" to render:

```
   void draw(Shape toDraw);
```

## Primitive Shape Constructors:

The following primitive shape constructors can be used to create basic shapes.  
With the exception of circles (which are centered on the origin), all shapes start at the origin and extend towards the right of the render window, along the x-axis.  
Each constructor returns a Shape object, allowing it to be assigned to a variable, used in a transformation, or rendered with `draw`.

`Color` can be `red`, `orange`, `yellow`, `green`, `blue`, `black`, `white`, or a hexadecimal color starting with `#` (e.g. `#ffffff`).  
`Mode` is either `outline` or `solid`.

- Create a circle with a radius, color, and mode:

```
   Shape createCircle(Number radius, Color color, Mode mode);
```

- Create a line with a length and color:

```
   Shape createLine(Number length, Color color);
```

- Create a petal (of scaled width) with a length and color:

```
   Shape createPetal(Number length, Color color, Mode mode);
```

- Create a cardioid with a length and color:
- (Cardioids are shapes defined by trigonometric functions. You can look them up, or just draw one and find out what they look like!)

```
   Shape createCardioid(Number length, Color color, Mode mode);
```

- Create a limacon with a length and color:
- (Limacons are shapes defined by trigonometric functions. You can look them up, or just draw one and find out what they look like!)

```
   Shape createLimacon(Number length, Color color, Mode mode);
```

## Transformation Functions

Transformation functions combine Shape objects to create more complex shapes. The results can be rendered, or used as arguments of transformation functions again to create increasingly detailed shapes.

Similar to primitive shape constructors, transformation functions return a new Shape object, without modifying the shape(s) used as arguments.

- Rotate the shape `toRotate` counter-clockwise around the origin by `degrees`:

```
   Shape rotate(Shape toRotate, Number degrees);
```

- Copy the shape `toRepeat` by `numReps` times. This transformation spreads them out evenly around the origin at a distance of `offset` from the origin.

```
   Shape repeat(Shape toRepeat, Number numReps, Number offset);
```

- Overlay an arbitrary number of shapes on top of each other, where `shape1` is placed on top of `shapeN` (the final shape argument).

```
   Shape overlay(Shape shape1, Shape shape2, ..., Shape shapeN);
```

## Control Blocks

Control blocks can be used to add more complex behavior to the program, such as conditional behavior or repeated behavior.

### For loops:

For loops can be used to create repetitive behavior or shape creation using a numeric loop counter within a specified range, similar to most programming languages.  
**Note:** The `range` and `(` must not have whitespace between them.

```
for <variable> in range(Number start, Number end) {
  <statements, including assignments or other control blocks>
}
```

### If blocks:

If blocks can be used to create conditional behavior or shape creation using a conditional expression (see below).  
**Note:** The else clause is entirely optional, and the `if` and `(` must have not whitespace separating them.

```
if(<condition>) {
  <statements, including assignments or other control blocks>
} else {
  <statements, including assignments or other control blocks>
}
```

### Condition expressions

Condition expressions evaluate to true or false, and act as the decider of which path to take in if blocks.  
They consist of one of the following condition operators in between two expressions that evaluate to a number (numbers, variables that evaluate to numbers, arithmetic expressions):

- Equals: `==`
- Not equals: `!=`
- Greater than: `>`
- Less than: `<`
- Greater than or equals: `>=`
- Less than or equals: `<=`

e.g. `var1 < var2` evaluates to true if var1 is less than var2, where var1 and var2 both evaluate to numbers.

## Arithmetic expressions

Anywhere that a number is used, an arithmetic expression or a variable containing a number can be used.  
Arithmetic expressions are typical math expressions and can be composed of numbers, other arithmetic expressions, and the following infix (between two arguments) arithmetic operators:

- Add: `+`
- Subtract: `-`
- Multiply: `*`
- Divide: `/`
- Modulo: `%`

e.g. `17 % 3` evaluates to 2.

**Note:** Due to time constraints on the implementation, operator precedence is bakck to front, and parenthesis have no impact on operator precedence. **However**, precedence can be enforced using variable assignment and multiple lines.

e.g. The following statements result in `num` being set to 10.

```
num = 17 % 3;
num = num * 5;
```

Whereas `num = 17 % 3 * 5` results in num being set to 2, even if parenthesis are placed around `17 % 3`.

## Other Nitty Gritty

- Variables can be assigned using numbers or arithmetic expressions, or an existing variable representing another number.
- However, variables **cannot** be assigned using an existing variable representing a shape object. This is due to an implementation constraint that could not be rectified given the time limitations.
  - e.g. `var1 = var2;` is only allowed if `var2` represents a number, not a shape.

## Example program:

```
circle1    = createCircle(6, #FF0000, outline);
circle2    = createCircle(3, #FF0000, solid);
rose       = repeat(createPetal(3, black, outline), 6, 0);
rose       = rotate(rose, 30);
lines      = repeat(createLine(3, #FF0000), 8, 3);

mandala    = overlay(circle1, rose, lines, circle2);

radius = 1/2;
for i in range(3,6) {
  if(i%2 == 0) {
    dot = createCircle(radius, black, solid);
  } else {
    dot = createCircle(radius, black, outline);
  }
  dots = repeat(dot, 8, i + 1/2);

  mandala = overlay(dots, mandala);
}

draw(mandala);
```
