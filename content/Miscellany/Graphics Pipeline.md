---
tags:
  - "#Renderer"
date: 2026-08-27
---
# What is it?

A graphics pipeline is simply the stages a rendering program will go through to turn vertex data into pixels for your screen. You should be able to pick out and name some of the abbreviations in the following image by the end of this note. ---V

![[renderdocpipelinestages.png]]
*\[1] -  taken from RenderDoc Pipeline Stage Panel* 

Graphics pipelines are quite standardized at this point, and follow the same generic process for ease of understanding across different APIs, but can vary wildly in optimizations and different intricate features. The absolute essentials are the following three stages in a pipeline: **Vertex Assembly**, **Rasterization**, and **Fragment Shading**. The other stages aren't fluff and certainly serve a purpose, but generally revolve around the three stages in some way.
## Generic Pipeline Explained
### Vertex Shader
*a.k.a. Vertex Assembler / Input Assembler*

This first stage involves taking vertices from wherever (string of data, parsed model, etc...) and position them in relative space using transformation matrices, things like stretch, squash, orientation across different spaces (e.g. spinning a cube in model space)
### Raster Stage
*a.k.a. Rasterization*

This is involves taking our newly transformed vertices and aliasing a screen's pixel where we have a vertex point in screen space. This is the stage where things like MSAA will happen as it pertains to pixel data and how we determine the weighting on pixels.
### Pixel Shader
*a.k.a. fragment shader*

In super simple shaders, this is just assigning colour data to our rastered pixel using corresponding data from a colour buffer, but this generally includes things like lighting, depth, reflections, and many more effects that can be applied to the pixel. 

So that's really all a basic a pipeline looks like, everything else is just extra polish or additional features.
### Tessellation Stages 
This sits right after the Vertex shader stage and just before the Geometry shader

Tessellation means adding more detail (more vertices) to a specific model or primitive shape. It's like subdividing a cube in blender. 
#### Hull Shader 
This is a **programable pipeline stage**, meaning it allows for user defined behaviour to change how the stage itself will operate. The fragment shader stage is also a programable stage as we can define the behaviour of a specific pixel given we pass it custom fragment shader code.

The hull shader will determine how much detail is desired and in which areas
#### Tessellation 
This is a **fixed pipeline stage**, meaning specific behaviour cannot be defined as it follows a certain set of instructions. defined in hardware. 

This is the stage that actually divides up the areas on the model.
#### Domain Shader 
Operates on the final Tessellation output. This stage transforms the added vertices to ensure they are located properly in the renderer's space, apply any vertex transforms that are required
### Geometry Shader
Between the Tessellation phase and the Rasterization phase is the geometry stage. This is generally used for particles and can manipulate vertices. It's very flexible, but also costly performance-wise, so no longer used very often. It's almost wholly replaced by a mesh shader, which will be discussed later on in the Vulkan-specific section. 
### Output Merger 
The last stage in the graphics Pipeline, the output merger, merges the output from the fragment shader with the render target, this is helpful for things like alpha blending where the final image will be dependant on the data in the underlying target.
### Compute Shader 
Not a part of the traditional graphics pipeline, the compute shader takes advantage of the GPU's ability to process matrix data quickly and allows for much more performant shading like making a particle shader that spawns 1 million+ particles, big advantages of compute shaders arrive when localizing data to the GPU only, which reduces context switching between queues and reduces lag between CPU and GPU.

Given the definitions provided for each stage, and with the understanding that not all stages will be made use of in every given pipeline, we should be able to deduce what each of the stages in this pipeline from RenderDoc, and how those stages may affect each other:

![[renderdocpipelinestages.png]]
*(\[1] taken from RenderDoc)*
Now with the Knowledge that greyed-out stages (Tessellation shader, Geometry shader, Computer shader) are those not used in this rendering instance, we can consider how this pipeline might differ from others.
## Vulkan-Specific Pipelineing
<div style="display: grid; grid-template-columns: 1fr 2fr; gap: 5px;"> 
	<img src="images/vulkangraphicspipeline.png" />
	<div>
	<p>The Vulkan render pipeline is a conceptual extension of the now defined generic render pipeline. Some of the stages defined previously are not often used in practice due to performance reasons, and Vulkan being a newer more performant API means it includes meaningful performant changes that diverge from the traditional pipeline.</p>
	<p>The figure here should effectively demonstrate how the established pipeline works, and we'll soon cover the changes and how they affect the traditional pipeline</p>
	<p>Stages with a green colour are <b>fixed-function</b> stages. These stages allow us to tweak their operations using parameters, but the way they work is predefined.</p>
	<p>Stages with an orange colour instead are <b>programmable</b>, which means that we can upload our own code to the graphics card. This allows the of use fragment shaders, for example, to implement anything from texturing and lighting to ray tracers.</p>
	</div>
</div>

*\[2] - Vulkan Graphics Pipeline*

Unlike other pipeline constructs in other APIs like openGL, Vulkan requires that the pipeline is recreated from scratch if we want to modifying or add for example, a fragment shader requires recreating the pipeline from scratch. 




# Resources
- \[1] [Renderdoc Pipeline Image](https://renderdoc.org/docs/window/pipeline_state.html#pipeline-flowchart)
- \[2]  [Vulkan Graphics Pipeline](https://docs.vulkan.org/tutorial/latest/03_Drawing_a_triangle/02_Graphics_pipeline_basics/00_Introduction.html)