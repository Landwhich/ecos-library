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
- [ ] ***Hello World*** - Basic renderer architecture with fundamental rendering capabilities (UBOs, SSBOs, proper pipelining with a rendergraph, etc... )
- [ ] ***Polishing the Basics*** - Additional much needed features (compute shaders, MSAA, Mipmaps, and more to add)
- [ ] ***Debugability*** - Proper internal debugging and profiling tooling
- [ ] ***Make it Fast*** - Multithreading infrastructure with extensibility for new features 
- [ ] ***Make it Pretty*** - Minimal Application complete with object rendering and GUI for runtime customization (GLFW + IMGUI)
- [ ] ***Physics!*** - Basic physics and rigidbody?
- [ ] ***Make it Performative*** - Object Instancing and easy optimizations
- [ ] ***Raycasting??*** - Implementing raycasting would be really fun, and has applications for both the physics and game engine project
### Game Engine
- [ ] Basic architecture including a component-based system for effective OOP and game object instancing.
- [ ] Lighting and baking for textures + shadows
### Sim
- [ ] Emulation of particles, electrons and neutrons
- [ ] Complete Electrical simulation 
# Design

## Hello World
As outlined in the goals section, this portion of development consists of designing a robust and semi-efficient [[Graphics Pipeline]]. We'll get started with the basics here, which means following a very basic pipeline layout just to get the part where we can render a Triangle. 

# Assembly

# So How Did I Do?

# Handy Resources 
- 