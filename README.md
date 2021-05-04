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




*Old notes*
* Textures
* Tex coords
* Sampling of texture
* Texture Wrapping
* Texture Filtering : defines stretegy for big objs and small res images (stretegy for scaling and downscaling : GL_NEAREST,GL_LINEAR )
* Mipmaps : solves problem of small objs(respect to camera pos.) and high res images (thus only used when downscaling texture)
