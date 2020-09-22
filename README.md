# WebGL Examples

[WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API) enables web content to use an API based on OpenGL ES 2.0 to perform 2D and 3D rendering in an [HTML canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) in browsers that support it without the use of plug-ins. WebGL programs consist of control code written in JavaScript and shader code (GLSL) that is executed on a computer's Graphics Processing Unit (GPU). WebGL elements can be mixed with other HTML elements and composited with other parts of the page or page background.

## The shaders

A `shader` is a program, written using the [OpenGL ES Shading Language (GLSL)](https://www.khronos.org/files/opengles_shading_language.pdf), that takes information about the vertices that make up a shape and generates the data needed to render the pixels onto the screen: namely, the positions of the pixels and their colors.

There are two shader functions run when drawing WebGL content: the `vertex shader` and the `fragment shader`. You write these in GLSL and pass the text of the code into WebGL to be compiled for execution on the GPU. Together, a set of vertex and fragment shaders is called a `shader program`.

### Vertex shader

Each time a shape is rendered, the `vertex shader` is run for each vertex in the shape. Its job is to transform the input vertex from its original coordinate system into the [clip space coordinate system](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_model_view_projection#Clip_space) used by WebGL, in which each axis has a range from -1.0 to 1.0, regardless of aspect ratio, actual size, or any other factors.

The vertex shader must perform the needed transforms on the vertex's position, make any other adjustments or calculations it needs to make on a per-vertex basis, then return the transformed vertex by saving it in a special variable provided by GLSL, called `gl_Position`.

The vertex shader can, as needed, also do things like determine the coordinates within the face's texture of the [texel](<https://en.wikipedia.org/wiki/texel_(graphics)>) to apply to the vertex, apply the normals to determine the lighting factor to apply to the vertex, and so on. This information can then be stored in [varyings](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Data#Varyings) or [attributes](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Data#Attributes) as appropriate to be shared with the fragment shader.

### Fragment shader

The `fragment shader` is called once for every pixel on each shape to be drawn, after the shape's vertices have been processed by the vertex shader. Its job is to determine the color of that pixel by figuring out which texel (that is, the pixel from within the shape's texture) to apply to the pixel, getting that texel's color, then applying the appropriate lighting to the color. The color is then returned to the WebGL layer by storing it in the special variable `gl_FragColor`. That color is then drawn to the screen in the correct position for the shape's corresponding pixel.
