# ThreeDThings.js

## Overview
ThreeDThings.js is a JavaScript library that consolidates 2D and 3D matrix operations and WebGL utility functions into a single ES6 module. It combines the functionality of `m3.js`, `m4.js`, and `webgl-utils.js` from the [WebGL Fundamentals](https://webglfundamentals.org/) project, refactored into a modern ES6 class structure for easier use in WebGL applications.

## Features
- **m3**: A collection of 2D matrix operations for transformations such as projection, translation, rotation, and scaling.
- **m4**: A collection of 3D matrix operations for advanced transformations including perspective projection, look-at matrices, and quaternion-based operations.
- **webGLUtils**: Utility functions for WebGL, including buffer creation, shader management, and vertex array object handling.

## Installation
To use ThreeDThings.js in your project, include the file and import the `ThreeDThings` class:

```javascript
import ThreeDThings from './ThreeDThings.js';
```

Ensure your project supports ES6 modules. If using a bundler like Webpack or Rollup, configure it to handle ES6 module syntax.

## Usage
Create an instance of the `ThreeDThings` class to access its methods:

```javascript
const threeD = new ThreeDThings();

// Example: Using m3 for 2D matrix operations
const projectionMatrix = threeD.m3.projection(800, 600);
const translatedMatrix = threeD.m3.translate(projectionMatrix, 100, 200);

// Example: Using m4 for 3D matrix operations
const perspectiveMatrix = threeD.m4.perspective(Math.PI / 3, 1, 0.1, 100);
const lookAtMatrix = threeD.m4.lookAt([0, 0, 5], [0, 0, 0], [0, 1, 0]);

// Example: Using webGLUtils for WebGL operations
const gl = canvas.getContext('webgl');
threeD.webGLUtils.resizeCanvasToDisplaySize(canvas);
const bufferInfo = threeD.webGLUtils.createBufferInfoFromArrays(gl, arrays);
```

## Methods
### m3
- `degToRad(d)`: Converts degrees to radians.
- `distance(x1, y1, x2, y2)`: Calculates the distance between two 2D points.
- `dot(x1, y1, x2, y2)`: Computes the dot product of two 2D vectors.
- `identity(dst)`: Returns a 3x3 identity matrix.
- `inverse(m, dst)`: Computes the inverse of a 3x3 matrix.
- `multiply(a, b, dst)`: Multiplies two 3x3 matrices.
- `normalize(x, y)`: Normalizes a 2D vector.
- `projection(width, height, dst)`: Creates a 2D projection matrix.
- `radToDeg(r)`: Converts radians to degrees.
- `reflect(ix, iy, nx, ny)`: Reflects a 2D vector over a normal.
- `rotation(angleInRadians, dst)`: Creates a 2D rotation matrix.
- `rotate(m, angleInRadians, dst)`: Rotates a matrix by an angle.
- `scaling(sx, sy, dst)`: Creates a 2D scaling matrix.
- `scale(m, sx, sy, dst)`: Scales a matrix.
- `transformPoint(m, v)`: Transforms a 2D point by a matrix.
- `translation(tx, ty, dst)`: Creates a 2D translation matrix.
- `translate(m, tx, ty, dst)`: Translates a matrix.
- `project(m, width, height, dst)`: Applies a projection transformation.

### m4
- `copy(src, dst)`: Copies a 4x4 matrix.
- `lookAt(cameraPosition, target, up, dst)`: Creates a look-at matrix.
- `addVectors(a, b, dst)`: Adds two 3D vectors.
- `subtractVectors(a, b, dst)`: Subtracts two 3D vectors.
- `scaleVector(v, s, dst)`: Scales a 3D vector.
- `distance(a, b)`: Calculates the distance between two 3D points.
- `distanceSq(a, b)`: Calculates the squared distance between two 3D points.
- `normalize(v, dst)`: Normalizes a 3D vector.
- `compose(translation, quaternion, scale, dst)`: Composes a matrix from translation, quaternion, and scale.
- `cross(a, b, dst)`: Computes the cross product of two 3D vectors.
- `decompose(mat, translation, quaternion, scale)`: Decomposes a matrix into translation, quaternion, and scale.
- `dot(a, b)`: Computes the dot product of two 3D vectors.
- `identity(dst)`: Returns a 4x4 identity matrix.
- `transpose(m, dst)`: Transposes a 4x4 matrix.
- `length(v)`: Calculates the length of a 3D vector.
- `lengthSq(v)`: Calculates the squared length of a 3D vector.
- `orthographic(left, right, bottom, top, near, far, dst)`: Creates an orthographic projection matrix.
- `frustum(left, right, bottom, top, near, far, dst)`: Creates a frustum projection matrix.
- `perspective(fieldOfViewInRadians, aspect, near, far, dst)`: Creates a perspective projection matrix.
- `translation(tx, ty, tz, dst)`: Creates a 4x4 translation matrix.
- `translate(m, tx, ty, tz, dst)`: Translates a 4x4 matrix.
- `xRotation(angleInRadians, dst)`: Creates a rotation matrix around the X-axis.
- `yRotation(angleInRadians, dst)`: Creates a rotation matrix around the Y-axis.
- `zRotation(angleInRadians, dst)`: Creates a rotation matrix around the Z-axis.
- `xRotate(m, angleInRadians, dst)`: Rotates a matrix around the X-axis.
- `yRotate(m, angle