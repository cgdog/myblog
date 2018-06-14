---
title: Understanding Skinning - The Vital Step for Any Rigging Project
id: 634
categories:
  - CG
date: 2016-10-24 09:54:10
tags:
  - mesh
---

### What is Skinning?

_See more detail:_[http://blog.digitaltutors.com/understanding-skinning-vital-step-rigging-project/](http://blog.digitaltutors.com/understanding-skinning-vital-step-rigging-project/)

Skinning is the process of binding the actual 3D mesh to the joint setup you created. This means that the joints you setup will have influence on the vertices of your model and move them accordingly. The difficulty with this is that typically a rig will consist of hundreds of individual joints, and most joints will need to have influence on only certain parts of the mesh.

For instance, the joint in the wrist of a character should most likely only control that area of the model. If you were to move the wrist joint, and it would influence the shoulder of the character that would obviously not look correct.

That is where skinning comes into play. Skinning is vital for not only creating a model that moves accurately in all the right places, but also so it deforms properly.

If you’re a Maya user, you’re probably aware of the Smooth Bind command. This will actually bind the entire skeleton to the mesh with the click of a button. Of course, things are not that easy and Smooth Bind is only the first step in skinning the skeleton to the 3D mesh.

By default Smooth Bind works by finding vertices closest to the joints and assigning the influence based on distance. This is all well and good, but the computer doesn’t do the best job which means once you’ve bound the mesh to the skeleton it’s up to you to finish the task, and manually assign the proper influence.

Wouldn’t it be nice if the job could be finished with one button? Sadly that’s not the case, so by binding the skeleton to the mesh that really just gives you a place to start.

Part of the skinning process is called weight painting, which you may be aware of. Painting the weights is actually what allows you to start assigning the proper influence that each joint has on your mesh and is a vital part of the skinning process.

Another useful link:[http://web.stanford.edu/class/cs248/pdf/class_13_skinning.pdf](http://web.stanford.edu/class/cs248/pdf/class_13_skinning.pdf)

[http://blog.digitaltutors.com/](http://blog.digitaltutors.com/)这个网站的内容挺有用的。