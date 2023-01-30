# lua-vector

2D and 3D vector library for Lua.

## Usage

Declaring new vectors

```lua
A = Vector(3, 4) -- X, Y coordinates
B = Vector(3.4, 1e2, -10) --- X, Y, Z coordinates
```

Manipulating vectors

```lua
A = Vector(23, 5)
B = Vector(0, 0, 5)

C = A + B    -- Addition
C = A:add(B) -- Same result

D = C * 3 / math.pi      -- Scaling
D = C:scale(3 / math.pi) -- Same result

D = A:cross(B) -- Cross product
n = A:dot(B)   -- Dot product

s = #A             -- Vector length (Lua 5.2+)
s = A:length()     -- Same result
U = A:unitVector() -- Unit vector

distance = #(A - B)
angle = A:angleBetween(B)
```

Advanced transformations

```lua
A = Vector(1, 0)

rotated = A:rotate(math.pi/2) -- 2D rotation
rotated = A:rotateZ(math.pi/2) -- same result

rotated_x = A:rotateX(math.pi/2)
rotated_y = A:rotateY(math.pi/2)
```

## Transformation Matrices

Sometimes you want to apply multiple transformations to a vector. Take this example:

> Scale a vector by a factor of 3.0, rotate on the X axis by 20 degrees,
> translate 5 units on the Z axis, rotate -40 degrees on the Y axis, and scale by a factor of 0.5

`Matrix` is a table that represents a 4 by 4 matrix it can be used to scale, rotate, and translate a vector.
They are useful when you want to apply multiple transformations to a single vector, or when you have many vectors to transform.

Our previous example can be solved like this:

```lua
V = Vector(1, 2, 3)

-- We create the matrix
M = Matrix()
    :scale(3)
    :rotateX(math.rad(20))
    :translate{z = 5}         -- We can also pass a Vector as an argument
    :rotateY(math.rad(-40))
    :scale(0.5)

-- and we apply it
newVector = V:transform(M)
```

