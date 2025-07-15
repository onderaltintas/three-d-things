# ThreeDThings.js

## Overview
ThreeDThings.js is a JavaScript library designed to simplify 3D graphics programming with WebGL. It consolidates utilities from `webgl-utils.js`, `m3.js`, and `m4.js` into a single module, providing tools for matrix operations, WebGL buffer management, shader handling, and more. This library enables developers to create 3D graphics applications in the browser with ease.

Originally developed by GFXFundamentals and modified by Önder Altıntaş, the library has been refactored to use modern ES6+ syntax, including `const`/`let` declarations, arrow functions, and module exports, improving readability and maintainability while preserving the original functionality.

## Features
- **Matrix Operations**: Includes `m3` for 2D transformations (e.g., rotation, scaling, translation) and `m4` for 3D transformations (e.g., perspective, look-at, quaternion-based operations).
- **WebGL Utilities**: Offers tools for creating and managing WebGL buffers, vertex arrays, shaders, and programs.
- **Augmented Typed Arrays**: Simplifies the creation and manipulation of typed arrays for WebGL attribute data.
- **Shader and Program Management**: Streamlines loading, compiling, and linking shaders, as well as setting up uniforms and attributes.
- **Flexible and Reusable**: Designed to be modular and reusable across various WebGL-based projects.

## Installation
To use ThreeDThings.js in your project, include the script in your HTML file or import it as an ES module:

```html
<script src="path/to/ThreeDThings.js"></script>
```

or

```javascript
import ThreeDThings from './ThreeDThings.js';
```

Ensure you have a WebGL-compatible browser and a WebGL context initialized in your application.

## Usage
Here’s a basic example of using ThreeDThings.js to set up a WebGL program and perform matrix transformations:

```javascript
import ThreeDThings from './ThreeDThings.js';

const gl = canvas.getContext('webgl');
const threeD = new ThreeDThings();

// Create a simple vertex and fragment shader
const vertexShaderSource = `
  attribute vec4 a_position;
  uniform mat4 u_matrix;
  void main() {
    gl_Position = u_matrix * a_position;
  }
`;
const fragmentShaderSource = `
  precision mediump float;
  void main() {
    gl_FragColor = vec4(1, 0, 0, 1); // Red color
  }
`;

// Create program
const programInfo = threeD.webGLUtils.createProgramInfo(gl, [vertexShaderSource, fragmentShaderSource]);

// Set up buffer with triangle vertices
const arrays = {
  position: { numComponents: 3, data: [0, 0, 0, 1, 0, 0, 0, 1, 0] },
};
const bufferInfo = threeD.webGLUtils.createBufferInfoFromArrays(gl, arrays);

// Create a perspective matrix
const aspect = gl.canvas.clientWidth / gl.canvas.clientHeight;
const projectionMatrix = threeD.m4.perspective(Math.PI / 4, aspect, 1, 100);

// Set up the scene
gl.useProgram(programInfo.program);
threeD.webGLUtils.setBuffersAndAttributes(gl, programInfo.attribSetters, bufferInfo);
threeD.webGLUtils.setUniforms(programInfo.uniformSetters, { u_matrix: projectionMatrix });
threeD.webGLUtils.drawBufferInfo(gl, bufferInfo);
```

## API Reference

### m3 (2D Matrix Operations)
- `degToRad(degrees)`: Converts degrees to radians.
- `identity(dst)`: Creates a 3x3 identity matrix.
- `inverse(m, dst)`: Computes the inverse of a 3x3 matrix.
- `multiply(a, b, dst)`: Multiplies two 3x3 matrices.
- `projection(width, height, dst)`: Creates a 2D projection matrix.
- `rotation(angleInRadians, dst)`: Creates a 2D rotation matrix.
- `translate(m, tx, ty, dst)`: Applies translation to a 3x3 matrix.
- ... and more.

### m4 (3D Matrix Operations)
- `perspective(fieldOfViewInRadians, aspect, near, far, dst)`: Creates a perspective projection matrix.
- `lookAt(cameraPosition, target, up, dst)`: Creates a view matrix.
- `translate(m, tx, ty, tz, dst)`: Applies translation to a 4x4 matrix.
- `xRotation(angleInRadians, dst)`: Creates a rotation matrix around the X-axis.
- `inverse(m, dst)`: Computes the inverse of a 4x4 matrix.
- `transformPoint(m, v, dst)`: Transforms a 3D point using a 4x4 matrix.
- ... and more.

### webGLUtils
- `createProgramInfo(gl, shaderSources)`: Creates a WebGL program with associated uniform and attribute setters.
- `createBufferInfoFromArrays(gl, arrays)`: Creates buffer information from array data.
- `drawBufferInfo(gl, bufferInfo)`: Draws a buffer using WebGL.
- `resizeCanvasToDisplaySize(canvas, multiplier)`: Resizes a canvas to match its display size.
- `setUniforms(setters, values)`: Sets uniform values for a WebGL program.
- ... and more.

## License
The software is provided under the following terms, as specified by GFXFundamentals:

- **Redistribution and use** in source and binary forms, with or without modification, are permitted provided that:
  - The source code retains the original copyright notice, conditions, and disclaimer.
  - Binary distributions reproduce the copyright notice, conditions, and disclaimer in the documentation or other materials.
  - The name of GFXFundamentals or its contributors may not be used to endorse or promote products derived from this software without specific prior written permission.
- The software is provided "AS IS" without any express or implied warranties, including but not limited to merchantability or fitness for a particular purpose.
- The copyright holders and contributors are not liable for any direct, indirect, incidental, special, exemplary, or consequential damages arising from the use of this software.

For the full license text, refer to the copyright notice at the top of the `ThreeDThings.js` file.

Copyright © 2021 GFXFundamentals.

## Modifications
This version of the library was created by Önder Altıntaş with the following modifications:
- Combined `webgl-utils.js`, `m3.js`, and `m4.js` into a single file.
- Refactored the codebase to use ES6+ syntax, including `const`/`let`, arrow functions, and module exports.

## Contributing
Contributions are welcome! Please submit pull requests or issues to the repository (if available) or contact the maintainer for suggestions and improvements. Ensure compliance with the licensing terms when contributing.

## Contact
For questions or feedback, reach out to the original author or maintainer as noted in the source code.