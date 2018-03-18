<img src="https://vuejs.org/images/logo.png" width="100">

# Lightning Talk Topic: Three.js

<a> https://docs.google.com/presentation/d/1R-9t3ssWW_zU580zUxHVcHSLYyRq1xk7FTqxbSuRQ8w/edit?usp=sharing </a>

Questions:
- What problem does this technology solve?
- How do you use it? (Is there a "cheatsheet" you found or made that others can reference?)
- What did you build?

<br>

- Probelm Solved:

Three.js is an open sourced Javascript Library created by for drawing 3d graphics on the web. Originally it was created as a renderer agnostic API so it had a 2d canvas and SVG renderer in the beginning. Then WebGL as became available it was added to it. This helped the popularity of both three.js and WebGL because it made it more accessible to developers.


- Here's how I used it:

So to get three.js you can go to website that has a bunch of examples of places its used in production websites on the web. 
On the left side you can download the library and use it. Also link to their Github and go through the source code and submit issues or track the progress of the library in its development. 

Also have link to Stack Overflow where you can get support and ask people questions in the community. 
There’s also documentation which goes through the API and the properties you can manipulate in the different classes within the library itself and what you can use it for. 

Probably the most important thing that they have on here is their examples because there is a slew of very thorough and advanced examples of what you can do with three.js. You can see they have some really cool simulation examples with physics and flocking algorithms as well as dynamic water simulations using different shaders. 

A great way to learn this is to go through the examples and the source code and looking at how people create different effects and playing around with them. 


##Demo of what I built using three.js

Before You Start:
In order to use Three.js, you need to reference its latest version in your HTML document.
Head over to the official three.js website. Then, download the latest version of Three.js and include it in your HTML like you would any other JS file.


```html
<div id="info">
  <p>Test </p>
  <p>Test </p>
</div>
```


```js
  app.get('/api/taquerias', function (req, res) {
    res.json(taquerias);
  });
```


```html
<html>
   <head>
      <title>My first Three.js app</title>
      &lt;style>canvas { width: 100%; height: 100% }</style>
   </head>
   <body>
      <script src="js/three.min.js"></script>
      <script>
         // Our Javascript will go here.
      </script>
   </body>
</html>
```

That's all. All the code we’re going to create will go into the empty <script> tag.

Creating the Scene:
To display anything with Three.js, you’re required to create three things: A scene, a camera and a renderer.

Doing so, you’ll be able to render the scene with camera. Let’s start with a scene:


```js
var scene = new THREE.Scene();
After setting up the scene, you’ve to create a camera. Consider it as the viewpoint that users are looking from.
```

```js
var camera = new THREE.PerspectiveCamera(75,window.innerWidth/window.innerHeight, 1,10000);
```

Let me explain what’s going on here. Three.js has a few different cameras, but in order to keep the code simple, I’ve used a PerspectiveCamera.

In the above code, there are four attributes: the first is the vertical field of view (from bottom to top) in degrees. The second one is the aspect ratio where the height of the element divides the width. The next is the near clipping plane, and the last is the far clipping plane. The near and far attributes control the rendering of objects. That means the object that is too far or too close to the camera won't be rendered.

After creating the camera, now I’m going to set up the WebGLRenderer. In addition to the WebGLRenderer, Three.js has some other renderers - like CanvasRenderer – which can be used as fallbacks for users whose browsers don’t support WebGL for some reason.

```js
var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
```

As you can see, in addition to creating an instance of the renderer, we also have to set the size at which we want the renderer to display our app. In this case, I’ve used the width and height of the browser window. Finally, I’ve added the renderer element to the HTML page. This is a <canvas> element used by the renderer to draw the scene.

Creating the 3D Cube:
After setting up the stage, now I’m going to create a 3D cube. For creating a cube, we need to use the BoxGeometry object that contains all the vertices and faces of the cube.

```js
var geometry = new THREE.BoxGeometry(700, 700, 700, 10, 10, 10);
```

This method takes five constructor parameters: the first is the width of the sides of the cube on the X axis, the second is height of sides of the cube on the Y axis, and the third is the depth of the sides of the cube on Z axis. The last three optional parameters, whose default value is 1, are the number of segmented faces along the width, height, and depth of the sides respectively.

I’ve set up the geometry of the cube, now we need to color it using a material. Three.js comes with numerous materials, but I’m using the MeshBasicMaterial here.

```js
var material = new THREE.MeshBasicMaterial({color: 0xfffff, wireframe: true});
```

For simplicity’s sake, I’ve only supplied a color attribute of 0xfffff that is blue. I’ve also set wireframe to true, so you could see the animating cube more clearly. The next thing we need is a Mesh.

```js
var cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

In the above code, the mesh object takes two parameters: the first is the geometry and the second is a material applied to it. Finally, I’ve added the cube to the scene.

By default, when we call function scene.add(), it adds the cube to the to the coordinates (0,0,0). This causes both the cube and the camera to be inside each other. To avoid this situation, we need to set the camera position before rendering the scene.

```js
camera.position.z = 1000;
```

As you can see, whatever code we’ve written above is extremely simple, that’s because Three.js keeps you away from all the complex stuff.

Rendering the Scene:
If you paste the above code into the HTML file (which I created in the first step of this tutorial), and test it in the browser, you’ll see nothing. That’s because we haven’t actually told the scene to render anything yet. To render the scene, we need a render loop.

```js
function render() {
   requestAnimationFrame(render);
   renderer.render(scene, camera);
}
render();
```

This code creates a loop that instructs the renderer to draw the scene. Here, you may get confused why didn’t I just use setInterval? That’s because using requestAnimationFrame instead of setInterval is beneficial in many ways. Most importantly, it pauses when a user moves to another tab in the browser, hence saving their precious resources.

A Practical Guide to Three.js with Live Demo

Animating the Cube:
If you test the file in your browser, now you’ll see a blue box without any animation. Let's make it more exciting by rotating it. Just add the following right below the requestAnimationFrame(render) in the render function. This will run every frame and add a nice rotation animation to the cube.

```js
cube.rotation.x += 0.01;
cube.rotation.y += 0.01;
```
The Result:
Congratulations! You have successfully built your first Three.js app. Here is the full code:

```html
<html>
<head>
<title>My first Three.js app</title>
&lt;style>canvas { width: 100%; height: 100% }</style>
</head>
<body>
<script src="js/three.min.js"></script>
<script>
var scene = new THREE.Scene();
var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 1, 10000);
var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
var geometry = new THREE.BoxGeometry(700, 700, 700, 10, 10, 10);
var material = new THREE.MeshBasicMaterial({color: 0xfffff, wireframe: true});
var cube = new THREE.Mesh(geometry, material);
scene.add(cube);
camera.position.z = 1000;        
function render() {
requestAnimationFrame(render);
cube.rotation.x += 0.01;
cube.rotation.y += 0.01;
renderer.render(scene, camera);
};
render();
</script>
</body>
</html>
```

Conclusion:

If you open up your index.html in your web browser, you will see the rotating cube in effect. By following the documentation online, I was able to build my first rotating cube using three.js! :D

## Sources:


**Resources**
- [ ] Three.js - https://threejs.org/
- [ ] Ricardo Cabello - http://ricardocabello.com/
- [ ] WebGL - https://www.khronos.org/webgl/
- [ ] WebVR - https://webvr.info/
