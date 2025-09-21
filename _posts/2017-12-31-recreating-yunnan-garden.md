---
title: "[URECA] Recreating Yunnan Garden"
date: 2017-12-31
---

![Result](/assets/imgs/yunnan-garden/1620012159520.jpeg)

Cultural Heritages are facing internal changes like natural ageing and chemical degrading. Nowadays, artefacts are created in a pace as never before, and they are unprecedently prone to external changes, such as natural disasters, city replanning and expansion. It is hard for traditional terrestrial methods such as hand survey or theodolite measurement to keep up the pace with the changes. Without a fast and reliable way to record and documenting heritages, we may never be able to access them in the future and they will be buried into history.



Some other concerns when we document the heritage sites include: 

1. Ease of archiving. Using a computer or a server with permanent storage. Little to no maintenance is needed after the development is done.

2. Easy of access. The audiences that have trouble travelling the world (update in 11/5/2021: it is what we are facing now in the global pandemic) will be able to access the database with a finger click. 

3. The eco-friendliness.

4. Recreating by 3D printing. 

In our project, the foremost principle was to maintain the accuracy of the subjects. In addition, we focused a lot on the graphics. On the other hand, the optimization and accessibility were less focused.

### Photogrammetry

In our case, we are using the software program with the photogrammetry methods and developed especially for 3D modelling. The general idea of the program is to use an algorithm for finding the common points from a large number of images. First, it generates a point cloud from the input images, and then it builds various kinds of mesh or ortho-images out of it.

The basic procedures of photogrammetry include:

1. Image capturing

2. Image processing

3. Reconstruction

4. Remeshing

There are some general limitations of photogrammetry software:

1. It cannot deal with objects with thin edges or transparency.

2. It cannot deal with reflective surfaces, like the metal covers on cars, mirrors etc.

3. It cannot deal with moving objects or pictures with too many moving objects as the background.

### Modelling of the Ornamental Rock

I tried to model the ornamental rock in Yunnan Garden with photogrammetry. It was about 1.3 meter in height.

The photos were taken from 6:35 pm to 6:53 pm and the weather was fine and cloudless. The lighting was diffused in most of the photos but became darker and darker when it was approaching 7 pm.

I used iPhone 6 as the camera. It has an 8-megapixel 1/3-inch sensor with a 1.5μm pixel size. I took 206 photos in total from all angles.

I used Photoscan for the first try and set the quality to high. It took about 10 hours until the result came out.

The missing of certain camera angles caused the failure of generating point cloud at some surfaces. However, the program had the option of automatically filling the holes in the final mesh. Despite this, the result was surprisingly detailed. The mesh contains 992,064 faces and 497,731 vertices, and the texture file was 4096*4096 in size.

![Rock_1](/assets/imgs/yunnan-garden/image-5.png "Figure 1. Scanned Rock with 182,230 vertices")
_Figure 1. Scanned Rock with 182,230 vertices_
![Rock_2](/assets/imgs/yunnan-garden/image-6.png "Figure 2. Meshed Rock")
_Figure 2. Meshed Rock_
![Rock_3](/assets/imgs/yunnan-garden/image-7.png "Figure 3. Textured Rock")
_Figure 3. Textured Rock_

For the second try, the photos were uploaded to Autodesk cloud through Autodesk Recap Photo. It features a fully automatic cloud build method, which gives less freedom of options, but easier to use and does not require local computation power.

The process cost about 8 hours and the result was similar to the previous one with Photoscan, but with fewer faces and vertices due to the quality setting.

![Rock_4](/assets/imgs/yunnan-garden/image-8.png "Figure 4. Audodesk Recap Version")
_Figure 4. Audodesk Recap Version_

### Modelling of the Monument

I used DJI Phantom 3 professional equipped with a 4K camera for photo-taking. The drone was made to orbit around the monument at a certain radius. I manually triggered the shutter of the drone camera as the drone was automatically piloting around the subject. The drone was adjusted to different heights for pictures of different perspectives. I took 658 photos in total with two rounds of shooting across two days between 2 to 3 pm.

I chose Agisoft Photoscan as the photogrammetry software for our project, taking advantages of its freedom of choices. The monument mesh was built on the local machine in about 10 hours. The quality was set to medium. The final mesh had 228,124 faces and 114,883 vertices.

![Monument_1](/assets/imgs/yunnan-garden/image-9.png "Figure 5. Scanned Monument with 330,555 points")
_Figure 5. Scanned Monument with 330,555 points_
![Monument_2](/assets/imgs/yunnan-garden/image-10.png "Figure 6. Meshed Monument")
_Figure 6. Meshed Monument_
![Monument_3](/assets/imgs/yunnan-garden/image-11.png "Figure 7. Textured Monument")
_Figure 7. Textured Monument_
![Monument_4](/assets/imgs/yunnan-garden/image-12.png "Figure 8. Inscriptions on the monument")
_Figure 8. Inscriptions on the monument_

### Models Created Manually

In contrast, the pavilion, the main gate, the ramp, the stairs, benches and trash bins were created manually by 3D artists. A matte painter helped us create a matte painting of the Chinese Heritage Centre as the background.

![Asset_1](/assets/imgs/yunnan-garden/image-13.png "Figure 9. Pavilion model (created by Mohamed Ziyaad Bin Mohd Siddique)")
_Figure 9. Pavilion model (created by Mohamed Ziyaad Bin Mohd Siddique)_
![Asset_2](/assets/imgs/yunnan-garden/image-14.png "Figure 10. Gate model (created by Gerald Wee)")
_Figure 10. Gate model (created by Gerald Wee)_
![Asset_3](/assets/imgs/yunnan-garden/image-15.png "Figure 11. Ramp and stairs (created by Kou Ying)")
_Figure 11. Ramp and stairs (created by Kou Ying)_
![Asset_4](/assets/imgs/yunnan-garden/image-16.png "Figure 12. Benches, trash bins (created by Toh Jia Hui)")
_Figure 12. Benches, trash bins (created by Toh Jia Hui)_
![Asset_5](/assets/imgs/yunnan-garden/image-17.png "Figure 13. Chinese Heritage Centre Matte-painting (created by Ada Chan)")
_Figure 13. Chinese Heritage Centre Matte-painting (created by Ada Chan)_

### Aerial Mapping

With the help of photogrammetry and drone mapping, I generated an orthomosaic aerial map as a lay-out reference of the garden. Note that I only map and recreate the vertical slice of the garden in the middle for this project.

![Aerial_1](/assets/imgs/yunnan-garden/image-18.png "Figure 14. Project set up for drone navigation.")
_Figure 14. Project set up for drone navigation._
![Aerial_2](/assets/imgs/yunnan-garden/image-19.png "Figure 15. The orthomosaic map generated by Photoscan")
_Figure 15. The orthomosaic map generated by Photoscan_

### Final Outcome

See the video for the final outcome rendered in real-time in Unreal Engine 4.

{% include embed/youtube.html id='IPRR4yb0FWc' %}

I am really grateful for my very down-to-earth supervisors Assoc Prof Benjamin Seide and Asst Prof Dr Elke Reinhuber. They generously provided every resources I need during this project. Their support opens up the opportunities for me to get into the real-time rendering and virtual reality industry.