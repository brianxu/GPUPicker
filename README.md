# GPUPicker
========
#### color picking based approach for fast searches ####
The goal of this project is to implement a fast way to select an object in the scene for the [THREE.js WebGL library](http://mrdoob.github.com/three.js/).   
  
```html
This build is built up on THREE.js ~r72dev
```
## Features (+ [Example](http://brianxu.github.io/GPUPicker/))

* support points/lines/triangle meshes
* retunr intersection object like the one returned from raycaster
* Fast! See the example to compare the framerates bettween raycaster and GPUPicker
    
## TODOs
* A cheap way to update the picking scene instead of set the scene
* Despose picking geometry when the rendering geometry is disposed

## Usage

Download the [script](https://github.com/brianxu/GPUPicker/blob/master/GPUPicker.js) and include it in your html after the [THREE.js WebGL library](http://mrdoob.github.com/three.js/).

```html
<script src="js/three.min.js"></script>
<script src="js/GPUPicker.js"></script>
```

#### Initialize

```html
gpuPicker = new THREE.GPUPicker({renderer:renderer, debug: false});
gpuPicker.setFilter(function (object) {return true;});
gpuPicker.setScene(scene);
gpuPicker.setCamera(camera);
```
#### Pick object
An example:
```html
function onMouseMove( e ) {
    if(e.which != 0)
        return;
    mouse.x = e.clientX;
    mouse.y = e.clientY;
    var raymouse = new THREE.Vector2();
    raymouse.x = ( e.clientX / window.innerWidth ) * 2 - 1;
    raymouse.y = - ( e.clientY / window.innerHeight ) * 2 + 1;
    raycaster.setFromCamera( raymouse, camera );
    var intersect;
    intersect = gpuPicker.pick(mouse, raycaster);
}
```

#### Update
When the scene camera has some change set the .needUpdate to be true to rerender the picking scene.
```html
gpuPicker.needUpdate = true;
```

When the window size changes, resize the texture.
```html
gpuPicker.resizeTexture( newWidth, newHeight );
```

When the scene changes, reset the scene.
```html
gpuPicker.setScene(scene);
```

##[Example](http://brianxu.github.io/GPUPicker/)
