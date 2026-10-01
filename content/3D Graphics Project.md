---
tags:
cssclasses:
---
# Intro
After creating a barebones 3D cube spinner in C, I've been wanting to explore graphics programming using a proper API, and have landed on Vulkan. I'm not sure as of yet how far the project will grow, but the project has potential for learning in a wide area and large depth of individual fields. 

I'll keep a tally going of progress made and avenues to explore in the goals section

# Goals
Obviously, improvement in graphics processing and understanding of GPUs is a given. I'd like to and will gain this experience simply by way of working on the fundamental aspects of the renderer itself. The additional learning will come from the direction I intend to take the project. 

I'd like to create a physics visualization sim but also a game engine. Something like a game engine will create the opportunity to dive deep in memory management and more architecture decisions, but a sim will allow for easier immediate directive to optimizations and time to better understand some cool physics concepts. It's entirely possible I'll fork it and implement both, but my decision will come down to which specific learning goals I'll be fulfilling.
## Progress
- [x] ***Hello World*** - Basic renderer architecture with fundamental rendering capabilities (UBOs, SSBOs, etc... ) <a href="#progress.helloworld">Done!</a>
	- [x] Triangle App 
	- [x] VBOs and IBOs [PR](https://github.com/Landwhich/gvis/commit/8bdc7101b83289807943bcef7fbcf7a0c9040f41)
	- [x] UBOs
	- [x] Textures
	- [x] Depth Testing [PR](https://github.com/Landwhich/gvis/commit/fa93c40fe92ec478579840a6928be03bd8d09ef5)
- [ ] ***Polishing the Basics*** - Additional much needed features (MSAA, Mipmaps, and more to add) <a href="#progress.polishingthebasics">Under construction...</a>
	- [ ] Simple Model Loads
	- [ ] Mipmaps
	- [ ] MSAA
- [ ] ***Hello World II***  - Improvements on fundamental architecture, like dynamic pipeline for compute shaders)
	- [ ] Separate Compute Shader Pipeline 
	- [ ] Improved Pipelining "Hotswap"
	- [ ] Renderer Resources
		- [ ] Mesh Objects
		- [ ] Materials
		- [ ] Extending UBOs
- [ ] ***Make it Pretty*** - Minimal Application complete with object rendering and GUI for runtime customization (GLFW + IMGUI)
- [ ] ***Debug-ability*** - Proper internal debugging and profiling tooling
- [ ] ***Hello World III***  - Final steps to a cohesive and extensible core system and architecture (render graphing and improved resource management)
- [ ] ***Make it Fast*** - Multithreading infrastructure with extensibility for new features 
	- [ ] Shadow Maps 
	- [ ] Light Baking 
- [ ] ***Make it Performant** - Object Instancing and easy optimizations
- [ ] ***Raycasting??*** - Implementing raycasting would be really fun, and has applications for both the physics and game engine project
- [ ] ***Physics!??*** - Basic physics and rigidbody?
### Game Engine
- [ ] ***Camera System***
	- [ ] Culling 
	- [ ] Input capture
	- [ ] Syncing input to view matrix
- [ ] ***Game Architecture***
	- [ ] Object instancing
	- [ ] Component-based system
### Sim
- [ ] Emulation of particles, electrons and neutrons
- [ ] Complete Electrical simulation 
# Design

## Hello World
<tag id="progress.helloworld"></tag>As outlined in the goals section, this portion of development consists of designing a robust and semi-efficient [[Graphics Pipeline]]. The core of this design stage started with the basics, following a very basic Vulkan pipeline layout just to get the part where we can render a Triangle via VBOs.

After setting up VBOs and IBOs, having simplistic UBOs for easy vector transforms was a logical step next. There I learnt a little about memory mapping, GPU descriptors and alignment (using `alignas(x)` and `#define GLM_FORCE_DEFAULT_ALIGNED_GENTYPES`)

Simple texturing is done by directly copying pixels from a buffer to a texture and using pipeline barriers to mediate synchronization of devices during transitions and r/w ops. Faster I hear -> https://developer.nvidia.com/vulkan-memory-management. Texels can be read directly from shader code, but this is uncommon due to the typical desire to filtering textures beforehand. I liked these images that displayed the need for filtering from vulkan and how the `vkSampler` objects worked, so I've included them in this section. They cover both cases of I) not enough texels for a given set of fragments and II) excess texels for a given set of fragments (especially in repeated sampling)
 
![[vulkanwikianisotropicfiltering.png|368]]![[vulkanwikibilinearfiltering.png|244]]
*\[1] -  (left) showing advantages of anisotropic filtering for excess of texels; (right) showing advantages of bilinear filtering for reduced texel set*
![[vulkanwikisamplertransforms.png|611]]
*\[1] - Additional transformation work done by sampler*

Finished this Section up with some simple depth buffering and 3D vertex descriptions
## Polishing the Basics
<tag id="progress.polishingthebasics"></tag>

# So How Did I Do?

# Handy Resources 
- \[1] - [Vulkan Doc Tutorials](https://docs.vulkan.org/tutorial/latest/00_Introduction.html)