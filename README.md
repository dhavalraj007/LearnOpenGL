# LearnOpenGL
Tutorials from LearnOpengl.com

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






*Old notes*
* Textures
* Tex coords
* Sampling of texture
* Texture Wrapping
* Texture Filtering : defines stretegy for big objs and small res images (stretegy for scaling and downscaling : GL_NEAREST,GL_LINEAR )
* Mipmaps : solves problem of small objs(respect to camera pos.) and high res images (thus only used when downscaling texture)
