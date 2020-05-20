# Foundation of Computer Graphics HOMEWORK 4

## CONTRIBUTOR 
Nijat Mursali <br>


## Introduction 

MYOH (1 person, easy), make your own homework:
  1. make small to large environment to show off Yocto/GL that we can use for next year homeworks
  2. these environments should show off the rendering features we demonstrated
  3. we are particularly interested in subdiv examples, displacement maps, etc
  4. the scenes should be compelling and of quality similar to the ones proposed this year
  5. remember to use CC licensed assets only, and include the license for them


## Development 

As mentioned in introduction part, the idea here was to create a scene that had the features that we have mentioned. The following picture shows the model I have created using Blender 2.8 where you can find information from the following [link](https://skfb.ly/6SJpx). 

![Model in Blender][scr1]

In order to start project, we first needed to add library from the actual yocto which you can find [here](https://github.com/xelatihy/yocto-gl). You need to get `ysceneproc` from `apps` and import it to the homework. This is crucial step because you also need to add `add_subdirectory(ysceneproc)` to the `apps/CMakeLists.txt`. When you do this, you just need to run `build.sh` file from the `scripts/build.sh` by just putting `./scripts/build.sh`. When it builds your `ysceneproc` file in `bin/ysceneproc` you can simply write the following command in bash


```
./bin/ysceneproc ./models/room/scene.gltf -o tests/room/file.json
```

What this script simply does is that it gets the `gltf` extension model and exports the `json` into another folder which we called tests. 

After you export the model, you can add them into the `run.sh` file in scripts folder. You just need to copy the following code and add to the `/scripts/run.sh` file. 


```
./bin/yscenetrace tests/room/file.json -o out/lowres/room.jpg -t path -s 256 -r 720
```

The following code is for `./scripts/run-highres.sh` which gives the better render, but slower than `run.sh`


```
./bin/yscenetrace tests/room/file.json -o out/highres/room.jpg -t path -s 1024 -r 1280
```

The following image is the result from the `./scripts/run.sh` execution. 
![Render with Yocto][scr2]



[scr1]: https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_1.png?raw=true "Model in Blender"
[scr2]: https://github.com/nijatmursali/FundamentalsofComputerGraphics/blob/master/HOMEWORK1-4/HW4/screenshots/screenshot_2.jpg?raw=true "Render with Yocto"

