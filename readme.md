# Space Garden

## Setup

Download [Node.js](https://nodejs.org/en/download/).
Run this followed commands:

```bash
# Install dependencies (only the first time)
npm install

# Run the local server at localhost:8080
npm run dev

# Build for production in the dist/ directory
npm run build
```

## About

I call this project Space Garden, as from the early childhood I have been told the story of paradise and heaven up in the sky. So, I used my creativity and Three.js skills to build up imagination.

## Tools

##### THREE.js

This is project is based on [THREE.js](https://threejs.org/). Three.js is a cross-browser JavaScript library and application programming interface (API) used to create and display animated 3D computer graphics in a web browser using WebGL. The source code is hosted in a repository on GitHub.

##### Webpack

[webpack](https://webpack.js.org/) is an open-source JavaScript module bundler. It is made primarily for JavaScript, but it can transform front-end assets such as HTML, CSS, and images if the corresponding loaders are included. webpack takes modules with dependencies and generates static assets representing those modules.

##### dat.GUI

[dat.GUI](https://opensource.google/projects/datgui) is a lightweight controller library for JavaScript. dat.GUI is a lightweight graphical user interface developed by the Google Data Arts Team.

> Note: **_Though dat.GUI is used for tweaking the properties and is used in development, but I am keeping it on, so that you can play the properties._**

## Working

As I have mentioned the Project is build using Three.js which basically works with three major Compenents.

- Scene

  - It contains all the geometry, shapes, mesh and other displayable content of the component.

- Camera

  - It sets the view of the end user. Depending upon the type of camera used we can view our component from different angles

- Rendered
  - As the name suggests, it mounts all the content we build in Three.js into our targeted component in DOM.

> **Light** is also a very important component for Three.js project. Alomost in every project of Three.js Lights play the a very important role. Depending upon the type of light used; shadows, reflection, brightness and graphical properties can be implemented.

##### Components Used:

- Perspective Camera

  - This projection mode is designed to mimic the way the human eye sees. It is the most common projection mode used for rendering a 3D scene.

  ```js
  PerspectiveCamera(fov, aspectRatio, near, far); // Constructor

  /* fov is Camera frustum Field of View which basically
   the mapping from 3D points in the world as they are
   seen from of a pinhole camera, to 2D points of the viewport. */

  /* aspectRatio: We generally specify it as width/height of the component */

  // Example (Used in this project)
  const camera = new THREE.PerspectiveCamera(
    45,
    sizes.width / sizes.height,
    0.1,
    100
  );
  ```

- WebGLRenderer

  - It renders our Three.js build elements in our targeted component. It uses WebGL under the hood.

  ```js
  // Example
  const renderer = new THREE.WebGLRenderer({
    canva: { targetCanvaElement },
    otherProps,
  });

  //We can specify some props, such as: (I have used in this project)

  renderer.outputEncoding = THREE.sRGBEncoding;
  // It is used for rendering consistent color as colors may be get hindered by lights.

  renderer.setSize(sizes.width, sizes.height);
  //set the size of the rendering component.

  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  /* This is usually used for HiDPI device to prevent bluring output canvas.
  Some devices have high HiDPI which may consumpe more GPU power therefore
  I have used min of (window.devicePixelRatio, 2) as 2 is enough for
  smooth rendering */
  ```

- Texture Loader

  - It loads the texture for our geometries.

  ```js
  // Example
  const textureLoader = new THREE.TextureLoader();
  const myTexture = textureLoader.load('{your-texture-file}');
  ```

- DRACOLoader

  - Its is used for compressing and decompressing 3D meshes and point clouds.

  ```js
  // Example
  const dracoLoader = new DRACOLoader();
  dracoLoader.setDecoderPath('draco/');
  ```

- GLTFLoader

  - It is used delivery and loading of 3D content. Assets may be provided either in JSON (.gltf) or binary (.glb) format.

  ```js
  // Example
  const gltfLoader = new GLTFLoader();
  ```

- Material

  - It describes the apperance of the elements. Such as smoothness, brightness, reflection, opacity etc.

  - I have used two Materials MeshBasicMaterial and ShaderMaterial

  ```js
  //Example for MeshBasicMaterial
  const myMaterial = new THREE.MeshBasicMaterial({
    map: { yourMap },
    color: { yourColor },
    otherProps,
  });

  // Example ShaderMaterial
  const myMaterial = new THREE.ShaderMaterial({
    uniforms: {
      uPixelRatio: { value: Math.min(window.devicePixelRatio, 2) },
      otherProps,
    },
    otherProps,
  });
  ```

- Geometry

  - It defines the shape of our components.
  - I have used BufferGeometry

  ```js
  const myGeometry = new THREE.BufferGeometry();
  /* A representation of mesh, line, or point geometry.
   Includes vertex positions, face indices, normals, colors, UVs, and
   custom attributes within buffers, reducing the cost of passing all this data
   to the GPU.*/

  const myPosition = new Float32Array(myCount * 3);
  // Float32Array is used to store x,y,z index of points of our geometry.
  ```

- OrbitControls

  - It describes the camera movement around the component. It gives 3D movement.

  ```js
  const myControls = new OrbitControls(cameraObject, domElement);
  /*
  cameraObject: The camera to be controlled. The camera must not be a child of another object,
  unless that object is the scene itself.
  
  domElement: The HTML element used for event listeners.
  */
  ```
