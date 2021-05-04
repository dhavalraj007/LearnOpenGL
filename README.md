Tutorials Notes from [LearnOpengl.com](https://learnopengl.com/)
# Notes
## Getting Started

### OpenGL
* OpenGL by itself is not an API, but merely a specification, developed and maintained by the Khronos Group.
* The people developing the actual OpenGL libraries are usually the graphics card manufacturers.
* in OpenGL's core-profile mode, which is a division of OpenGL's specification that removed all old deprecated functionality.
* All future versions of OpenGL starting from 3.3 add extra useful features to OpenGL without changing OpenGL's core mechanics.
* Whenever a graphics company comes up with a new technique or a new large optimization for rendering this is often found in an extension implemented in the drivers
* OpenGL is by itself a large state machine: a collection of variables that define how OpenGL should currently operate
* The state of OpenGL is commonly referred to as the OpenGL context.
* When working in OpenGL we will come across several state-changing functions that change the context and several state-using functions that perform some operations based on the current state of OpenGL.
* An object in OpenGL is a collection of options that represents a subset of OpenGL's state.

### CreatingWindow
* GLFW allows us to create an OpenGL context, define window parameters, and handle user input.
* GLAD defines all the opengl functions definitions and also makes OS-specific calls to retrieve the address of those fucntions and assigns them to the function pointer when you call gladGLLoader func.
  * We pass GLAD the function to load the address of the OpenGL function pointers which is OS-specific. GLFW gives us glfwGetProcAddress that defines the correct function based on which OS we're compiling for.
* to get started with OpenGL do the following:
  1. set up OpenGL context and window (set up glfw) and make context current
   ``` cpp
    glfwInit();
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);  // version 3.3
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE); // core profile
    
    GLFWwindow* window = glfwCreateWindow(800, 600, "LearnOpenGL", NULL, NULL); //window and context
    glfwMakeContextCurrent(window);  //make context current on the window
   ```
  2. get those funciton pointers from the drivers (set up glad)
    ``` cpp
    gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)
    ```
  3. add the render loop 
    ``` cpp
     while (!glfwWindowShouldClose(window))
      {
        // input
        processInput(window);

        // render
        glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
        glClear(GL_COLOR_BUFFER_BIT);

        // glfw: swap buffers and poll IO events (keys pressed/released, mouse moved etc.)
        glfwSwapBuffers(window);
        glfwPollEvents();
      }

    ```
  4. Free up all the glfw resources
    ``` cpp
    glfwTerminate();
    ```
### Hello Triangle
#### [Graphics pipeline](https://learnopengl.com/img/getting-started/pipeline.png) brief
* **The graphics pipeline** can be divided into two large parts: the first transforms your 3D coordinates into 2D coordinates and the second part transforms the 2D coordinates into actual colored pixels.
* So the **graphics pipeline** of OpenGL manages the process of transforming 3D coordinates -> 2D colored pixels.
* The graphics pipeline can be divided into several steps where each step requires the output of the previous step as its input. All of these steps are highly specialized (they have one specific function) and can easily be executed in parallel.
* The processing cores run small programs on the GPU for each step of the pipeline. These small programs are called **shaders**.
* Shaders are written in the OpenGL Shading Language (**GLSL**).

* Only Vertex-shader , geometry-shader and fragment shader can be user defined.
* **Vertex** is a collection of data per 3D coordinate. That vertex's data is represented using vertex attributes that can contain any data we'd like(eg. 3D coords and Color).
* OpenGL requires you to hint what kind of render types you want to form with the Vertex data.Those hints are called **primitives**. Some of these hints are GL_POINTS, GL_TRIANGLES and GL_LINE_STRIP.
* A fragment in OpenGL is all the data required for OpenGL to render a single pixel.

| stage | brief |
|:----- | :----- |
| Vertex-shader | takes a single vertex as a input. The vertex shader transforms 3D coords into different 3D coords (more on that later) and allows us to do some basic processing on the vertex attribs. | 
| Shape-assembly | takes as input all the vertices (or vertex if GL_POINTS is chosen) from the vertex shader that form a primitive and assembles all the point(s) in the primitive shape given. |
| Geometry-shader | The geometry shader takes as input a collection of vertices that form a primitive and has the ability to generate other shapes by emitting new vertices to form new (or other) primitive(s). |
| Rasterization | it maps the resulting primitive(s) to the corresponding pixels on the final screen, resulting in fragments for the fragment shader to use. Before the fragment shaders run, clipping is performed. Clipping discards all fragments that are outside your view, increasing performance. |
| Fragment-shader | The main purpose of the fragment shader is to calculate the final color of a pixel and this is usually the stage where all the advanced OpenGL effects occur. Usually the fragment shader contains data about the 3D scene that it can use to calculate the final pixel color (like lights, shadows, color of the light and so on). |
| alpha Tests and Blending | This stage checks the corresponding depth (and stencil) value of the fragment and uses those to check if the resulting fragment is in front or behind other objects and should be discarded accordingly. The stage also checks for alpha values (the opacity of an object) and blends the objects accordingly. |



*Old notes*
* Textures
* Tex coords
* Sampling of texture
* Texture Wrapping
* Texture Filtering : defines stretegy for big objs and small res images (stretegy for scaling and downscaling : GL_NEAREST,GL_LINEAR )
* Mipmaps : solves problem of small objs(respect to camera pos.) and high res images (thus only used when downscaling texture)
