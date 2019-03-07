# Pine
Pine is an aimbot powered by real-time object detection with neural networks.

This software can be tweaked to work smoothly in CS:GO, Fortnite, and Overwatch. Pine also has built-in support for Nvidia's CUDA toolkit and is optimized to achieve extremely high object-detection FPS. It is GPU accelerated, cross-platform, and blazingly fast.


### Why Neural Networks?

Well, neural network aimbots are great for a lot of reasons... Probably most importantly, they never access the memory of the game, so they are practically invisible to "Anti-Cheat" sofware. Additionally, they can abstract their capabilities to many different games without code modifications. The only issue:

Neural Network Aimbots have always had one big problem: their target detection is okay, but their inference time is *terrible*. Even HAAR Cascades are a bad fit, since they have decent speed but horrible accuracy. MobileNetSSD and Faster R-CNN were *sorta ok* if you had a Nvidia Titan X with CUDA drivers. But let's be honest, who the hell can afford a Titan?

Enter YOLOv3, tiny edition. Detection scores are decent, and inference times are... *WHAT? **220 FPS WITH A 33% mAP?!*** For reference of how absolutely insane this is, SSD513 gets about 8 FPS with 50% mAP.


![YOLO Network Speed Graph](https://pjreddie.com/media/image/map50blue.png)


Finally, a real-time object-detection network that will run on my dinky AMD M370X from 2015! This network is what inspired me to build Pine.



## Architecture

### YOLOv3: The Internal Object-Detection Engine

At its core, Pine's internal object detection system relies on a modified version of the [YOLOv3](https://pjreddie.com/media/files/papers/YOLOv3.pdf) neural network architecture. The detection network is trained on a combination of video game images and the COCO dataset. It is optimized to recognize human-like objects as quickly as possible. This is useful because the decection engine can be abstracted to many FPS games, including CS:GO, TF2, and more.

![YOLO Neural Network](https://i.imgur.com/0edTFBP.jpg)

YOLO's inference time puts RetinaNet to shame...


### OpenCV: GPU-Enabled Image Processing

OpenCV is at the heart of Pine's image processing capabilities. Not only does it provide an abstraction layer for working with the screen capture data, but it it also allows us to harness the power of GPU hardware by interfacing CUDA and OpenCL. After Pine takes a capture of the user's screen, it uses OpenCV to process that image into a form that is recognizable to the object-detection engine.

![OpenCV Image Processing Architecture](https://i.imgur.com/n3LgS6T.png)
