<h1 align="center">
<img src="https://logos-download.com/wp-content/uploads/2019/07/Sapienza_Roma_Logo.png"
      alt="Sapienza" width="80%" />
</h1>

<h2 align="center">Artificial Intelligence and Robotics</h2>

<h3 align="center">Foundation of Computer Graphics</h3>

<h4 align="center">2020 June</h4>

<h4 align="center">Nijat Mursali | 1919669</h4>

<h4 align="center">HOMEWORK 4 - SCENE CREATION PROJECT</h4>

---



<div align="center">
  <h3>
    <a href="https://skfb.ly/6SJpx">
      MY MODELS
    </a>
    <span> | </span>
    <a href="https://skfb.ly/6RzJX">
      OTHER MODELS
    </a>

  </h3>
</div>

## Table of Contents
- [Introduction](#introduction)
- [Development](#development)
- [Results](#results)
- [Conclusion](#conclusion)


## Introduction 

The fundamental idea of this project was that this project helped us to understand the [Yocto tools](https://github.com/xelatihy/yocto-gl) to render our models. In order to make the project more interesting, we have checked the same scene with Blender 2.8 Cycles render engine to see how powerful Yocto can be to render the images. Thus, as mentioned in the project list, this homework helped us to make environment to show off Yocto/GL by demostrating the rendering features we have demonstrated. In our models, we have added [subdivision surface modifier](https://docs.blender.org/manual/en/latest/modeling/modifiers/generate/subdivision_surface.html) and others. For this project, we have used only one outside asset that mentioned above, all other models included in scene are our own models. 

## Development 

As mentioned in introduction part, the idea here was to create a scene that had the features that we have mentioned. The following picture shows the model I have created using Blender 2.8 where you can find information from the following [link](https://skfb.ly/6SJpx). 

<p align="center">
  <img src = "https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_1.png?raw=true">
</p>

In order to start project, we first needed to add library from the actual yocto which you can find [here](https://github.com/xelatihy/yocto-gl). You need to get **ysceneproc** from **apps** and import it to the homework. This is crucial step because you also need to add `add_subdirectory(ysceneproc)` to the `apps/CMakeLists.txt` which your final **CMakeLists.txt** inside the **app** directory will look like this.

```js
add_subdirectory(yscenetrace)
add_subdirectory(ysceneproc)

if(YOCTO_OPENGL)
add_subdirectory(ysceneitraces)
endif(YOCTO_OPENGL)
```

When you do this, you just need to run `build.sh` file from the `scripts/build.sh` by just putting `./scripts/build.sh`. Following code shows the `build.sh` file. 
 
```bash
# for OSX and Linux
mkdir -p build
cd build
env CXX=/usr/bin/clang++ cmake ..
make -j 12
```

When it finishes, it simply creates the `ysceneproc` file inside the **bin** folder. To make our life easy, we simply created new bash script to convert our GLTF files into JSON format. With the following code you can simply create bash script and run the application in order to convert the files:


```bash
./bin/ysceneproc ./models/room_camera1/Scene1.gltf -o tests/room_camera1/file.json
./bin/ysceneproc ./models/room_camera2/Scene1.gltf -o tests/room_camera2/file.json
./bin/ysceneproc ./models/room_camera3/Scene1.gltf -o tests/room_camera3/file.json
./bin/ysceneproc ./models/room_camera4/Scene1.gltf -o tests/room_camera4/file.json
./bin/ysceneproc ./models/room_camera5/Scene1.gltf -o tests/room_camera5/file.json
```

What this script simply does is that it gets the `gltf` extension model and exports the `json` into another folder which we called tests. 

After you export the model, you can add them into the `run.sh` file in scripts folder. You just need to copy the following code and add to the `/scripts/run.sh` file. 


```bash
./bin/yscenetrace tests/room_camera1/file.json -o out/lowres/room_camera1.jpg -t path -s 256 -r 720
./bin/yscenetrace tests/room_camera2/file.json -o out/lowres/room_camera2.jpg -t path -s 256 -r 720
./bin/yscenetrace tests/room_camera3/file.json -o out/lowres/room_camera3.jpg -t path -s 256 -r 720
./bin/yscenetrace tests/room_camera4/file.json -o out/lowres/room_camera4.jpg -t path -s 256 -r 720
./bin/yscenetrace tests/room_camera5/file.json -o out/lowres/room_camera5.jpg -t path -s 256 -r 720

```

The following code is for `./scripts/run-highres.sh` which gives the better render, but slower than `run.sh`.


```bash
./bin/yscenetrace tests/room_camera1/file.json -o out/highres/room_camera1.jpg -t path -s 1024 -r 1280
./bin/yscenetrace tests/room_camera2/file.json -o out/highres/room_camera2.jpg -t path -s 1024 -r 1280
./bin/yscenetrace tests/room_camera3/file.json -o out/highres/room_camera3.jpg -t path -s 1024 -r 1280
./bin/yscenetrace tests/room_camera4/file.json -o out/highres/room_camera4.jpg -t path -s 1024 -r 1280
./bin/yscenetrace tests/room_camera5/file.json -o out/highres/room_camera5.jpg -t path -s 1024 -r 1280
```

## Results 

The following image is the result from the `./scripts/run.sh` execution. We have added as many images as possible in order to show the different camere angles for all objects. We will also add the high resolution images of renders. 

<p align="center">
  <img src = "https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_2.jpg?raw=true">
</p>

<p align="center">
  <img src = "https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_3.jpg?raw=true">
</p>

<p align="center">
  <img src = "https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_4.jpg?raw=true">
</p>

<p align="center">
  <img src = "https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_5.jpg?raw=true">
</p>

<p align="center">
  <img src = "https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_6.jpg?raw=true">
</p>

<p align="center">
  <img src = "https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_7.jpg?raw=true">
</p>


## Conclusion

This document has been created to show how exactly we have created our scene using Yocto/GL tools. For this reason, we would like to thank professor Fabio Pellacini for teaching all the great content during this semester. Before this course, I was just using the Blender 2.8 without knowing the algorithm behind the tools, but within this course I learned a lot. For the future development, I would like test this library to make renders and conversions. 

