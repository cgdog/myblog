---
title: Skeletal animation
id: 654
categories:
  - CG
date: 2016-11-03 22:07:07
tags:
  - mesh
  - skeleton animation
---

# Skeletal animation

**Skeletal animation** is a technique in computer animation in which a character (or other articulated object) is represented in two parts: a surface representation used to draw the character (called skin or mesh) and a hierarchical set of interconnected bones (called the skeleton or rig) used to animate (pose and keyframe) the mesh.[1] While this technique is often used to animate humans or more generally for organic modeling, it only serves to make the animation process more intuitive and the same technique can be used to control the deformation of any object — a door, a spoon, a building, or a galaxy. When the animated object is more general than for example a humanoid character the set of bones may not be hierarchical or interconnected, but it just represents a higher level description of the motion of the part of mesh or skin it is influencing.

The technique was introduced in 1988 by Nadia Magnenat Thalmann, Richard Laperrière, and Daniel Thalmann.[2] This technique is used in virtually all animation systems where simplified user interfaces allows animators to control often complex algorithms and a huge amount of geometry; most notably through inverse kinematics and other "goal-oriented" techniques. In principle, however, the intention of the technique is never to imitate real anatomy or physical processes, but only to control the deformation of the mesh data.

**Technical**

Frank Hanner, character CG supervisor of the Walt Disney Animation Studios, provided a basic understanding on the technique of character rigging.[3] This technique is used by constructing a series of 'bones,' sometimes referred to as rigging. Each bone has a three-dimensional transformation (which includes its position, scale and orientation), and an optional parent bone. The bones therefore form a hierarchy. The full transform of a child node is the product of its parent transform and its own transform. So moving a thigh-bone will move the lower leg too. As the character is animated, the bones change their transformation over time, under the influence of some animation controller. A rig is generally composed of both forward kinematics and inverse kinematics parts that may interact with each other. Skeletal animation is referring to the forward kinematics part of the rig, where a complete set of bones configurations identifies a unique pose.

Each bone in the skeleton is associated with some portion of the character's visual representation. Skinning is the process of creating this association. In the most common case of a polygonal mesh character, the bone is associated with a group of vertices; for example, in a model of a human being, the 'thigh' bone would be associated with the vertices making up the polygons in the model's thigh. Portions of the character's skin can normally be associated with multiple bones, each one having a scaling factors called vertex weights, or blend weights. The movement of skin near the joints of two bones, can therefore be influenced by both bones. In most state-of-the-art graphical engines, the skinning process is done on the GPU thanks to a shader program.

For a polygonal mesh, each vertex can have a blend weight for each bone. To calculate the final position of the vertex, a transformation matrix is created for each bone which, when applied to the vertex, first puts the vertex in bone space then puts it back into mesh space, the vertex. After applying a matrix to the vertex, it is scaled by its corresponding weight. This algorithm is called matrix palette skinning, because the set of bone transformations (stored as transform matrices) form a palette for the skin vertex to choose from.

> Reference:[https://en.wikipedia.org/wiki/Skeletal_animation](https://en.wikipedia.org/wiki/Skeletal_animation)