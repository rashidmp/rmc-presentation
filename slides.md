---
theme: ./theme
class: 'text-center'
highlighter: shiki
lineNumbers: true
info: React Master Class.
  Learn more at [LevelX.in](https://levelx.in)
transition: slide-left
# use UnoCSS
css: unocss
layout: intro
---

# React Mater Class

Build a beutiful website with 3D

<div class="absolute bottom-10">
  <span class="font-700">
    <a href="mailto:dev@levelx.in">Rx</a>
  </span>
</div>
---
layout: intro-image-right
image: './assets/intro.png'
---

# Demo

What we are going to build
<a class="text-blue">link</a>

---
layout: bullets
---

# Installing Node.js


- Visit the official Node.js <a href="https://nodejs.org/en" target="_blank">website</a> .
- Download the appropriate installer for your operating system.
- Run the installer and follow the on-screen instructions.
- Verify that Node.js was installed successfully by opening a terminal or command prompt and running the following command: node -v. This should display the version number of Node.js that was installed.

---
layout: bullets
---

# Create a react app with vitejs

- create a vite app
```bash
npm create vite@latest
```

- Enter the project name
- Select React from framework
<img src="/assets/vite1.png" width="300" />
- Select javascript from varient
<img src="/assets/vite2.png" width="300" />

---
layout: bullets
---

- Navigate into the newly created directory with cd my-app.
- Start the development server by running the following command: npm run dev.
- Your new React app should now be running at http://localhost:5174.

---
layout: section
---

# React <vscode-icons-file-type-reactjs/>

---

# Basic React Components

What are React components?

- Building blocks of React apps
- Encapsulate UI logic and rendering behavior
- Can be reused across multiple applications

---

# Functional Components

- Simplest type of React component
- Defined as a function that returns JSX
- No state or lifecycle methods
- Used for rendering static content

```jsx
function Button(props) {
  return <button>{props.label}</button>;
}
```

---

# Class Components

- More powerful than functional components
- Defined as a class that extends React.Component
- Have state and lifecycle methods
- Used for more complex UI logic and interactions

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </div>
    );
  }
}
```

---

# Props
- Short for "properties"
- Data passed from a parent component to a child component
- Immutable and read-only within the child component
- Used for customizing component behavior and appearance
```jsx
function Card(props) {
  return (
    <div>
      <h2>{props.title}</h2>
      <p>{props.content}</p>
    </div>
  );
}
```

---

# State
- Internal data of a component
- Can be changed by calling setState()
- Changes trigger re-rendering of the component and its children
- Used for managing dynamic content and interactions

```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isOn: false };
  }
  handleClick() {
    this.setState({ isOn: !this.state.isOn });
  }
  render() {
    return (
      <button onClick={() => this.handleClick()}>
        {this.state.isOn ? "ON" : "OFF"}
      </button>
    );
  }
}
```

---

# Conclusion
- Functional components and class components are the two basic types of React components
- Props are used for passing data from parent to child components
- State is used for managing internal data and triggering re-renders

---
layout: section
---

# The Box 📦

---

# Install Dependencies
before starting install the required dependencies

```bash
npm install three @types/three @react-three/fiber @react-three/drei
```

## what are these ?

- three: This is the core 3D rendering library that provides the underlying functionality for creating 3D scenes in the browser.
- @types/three: This is the TypeScript type definition for three, which enables you to write TypeScript code with three.
- @react-three/fiber: This is a lightweight wrapper around three that allows you to create and manipulate 3D scenes in a React-like way.
- @react-three/drei: This is a collection of useful helpers and abstractions for @react-three/fiber that simplifies some common tasks like adding lights, cameras, or 3D models to your scene.

---

# Displaying a Box with React Three Fiber

```jsx
<Canvas>
  <ambientLight intensity={0.5} color="white" />
  <spotLight
    position={[10, 15, 10]}
    angle={0.15}
    penumbra={1}
    intensity={1}
    distance={100}
    shadow-mapSize-width={1024}
    shadow-mapSize-height={1024}
    shadow-camera-near={0.1}
    shadow-camera-far={150}
    shadow-camera-fov={45}
  />
  <mesh rotation={[0, Math.PI / 4, 0]}>
    <boxBufferGeometry args={[1, 1, 1]} />
    <meshStandardMaterial color="orange" />
  </mesh>
  <OrbitControls enableZoom={false} />
</Canvas>
```

---

## Here's what's happening in the code:

- `<Canvas>` creates a canvas element in the DOM and initializes the Three.js renderer.
- `<ambientLight>` creates a light source that affects all objects in the scene equally. It has an intensity of 0.5 and a white color.
- `<spotLight>` creates a single light source that originates from a single point and illuminates in a cone shape. It has an intensity of 1 and a position of [10, 15, 10]. It casts shadows with a map size of 1024x1024 and has a near and far camera range of 0.1 to 150, respectively. The field of view of the camera is 45 degrees.
- `<mesh>` creates a 3D mesh with a boxBufferGeometry that has a width, height, and depth of 1 unit. It has a rotation of [0, Math.PI / 4, 0] and a meshStandardMaterial with an orange color.
- `<OrbitControls>` adds orbit controls to the camera so that the user can rotate the scene with their mouse. The enableZoom prop is set to false, which disables zooming with the mouse wheel.

---

## Mesh, Geometry, and Material in React Three Fiber

- In React Three Fiber, `Mesh` is a component that represents a 3D object in the scene.
- A `Geometry` defines the shape and structure of the Mesh.
- A `Material` defines the appearance of the Mesh.
- Here is an example
```jsx
 <mesh rotation={[0, Math.PI / 4, 0]}>
    <boxBufferGeometry args={[1, 1, 1]} />
    <meshStandardMaterial color="orange" />
  </mesh>
```

---

## Animating the Cube
```jsx
import { useFrame } from '@react-three/fiber';
import { useRef } from 'react';
export function Box() {
  const ref = useRef();
  useFrame((state) => {
    const t = state.clock.getElapsedTime();
    ref.current.rotation.set(t, t, t);
  });
  return (
    <mesh ref={ref}>
      <boxGeometry />
      <meshStandardMaterial color={'hotpink'} />
    </mesh>
  );
}
```

- `useFrame` hook allows updating the scene on every frame of the render loop
- `useRef` hook is used to create a reference to the mesh object so we can update it on each frame
- `ref` is passed to the `mesh` object
- `rotation` property of `ref.current` is updated on each frame with a time variable to create an animation effect

---
layout: section
---

# The Shoe-configurator 👟⚙️

---
layout: section
---

# Loading GLB Files

---
layout: bullets
---

# What is GLB?
- GLB is a file format used for 3D models
- It's a binary version of the glTF format
- It's widely used for web-based 3D graphics because it's compact and efficient
- [link](https://sketchfab.com/)

<div class="h-8"></div>

# What is gltfjsx?
- gltfjsx is a tool that generates React components from GLTF files
- It uses react-three-fiber to create Three.js-based 3D scenes
- It simplifies the process of importing 3D models into React applications
- [link](https://github.com/pmndrs/gltfjsx)

---

# Using gltfjsx

- To use gltfjsx, run this command in your terminal
```bash
npx gltfjsx path/to/file.glb
```
- It will generate a React component based on the GLB file
- You can then import the component and use it in your React application
```jsx
import Model from './Shoe';

function App() {
  return (
    <div>
      <Canvas>
        <Shoe />
      </Canvas>
    </div>
  );
}
```

---
layout: section
---

# Changing the color 🎨

---

# What is [Valtio](https://github.com/pmndrs/valtio)?
- Valtio is a tiny and efficient state management library for React
- It allows to manage the state of a React application using a proxy object
- It provides a simple and easy-to-use API for creating and updating state
```jsx
import { proxy, useSnapshot } from 'valtio';

export const state = proxy({
  current: null,
  items: {
    laces: '#ffffff',
    mesh: '#ff0000',
    caps: '#000000',
    inner: '#ffffff',
    sole: '#000000',
    stripes: '#ffffff',
    band: '#ffffff',
    patch: '#ffffff',
  },
});
```

---

- To use this state
```jsx
  const snap = useSnapshot(state);
```

<div class="h-8"></div>

# What is [React Colorful](https://omgovich.github.io/react-colorful/)?
React Colorful is a simple and easy-to-use color picker library for React
It provides different types of color pickers, including the HexColorPicker used in this example

```bash
npm install react-colorful
```

- Usage
```jsx
import { HexColorPicker } from "react-colorful";

const YourComponent = () => {
  return <HexColorPicker color={color} onChange={setColor} />;
};
```

----

# Picker Component
```jsx
import { useSnapshot } from 'valtio';
import { HexColorPicker } from 'react-colorful';

export function Picker() {
  const snap = useSnapshot(state);
  return (
    <div
      className="color-container"
      style={{ display: snap.current ? 'flex' : 'none' }}
    >
      <HexColorPicker
        className="picker"
        color={snap.items[snap.current]}
        onChange={(color) => (state.items[snap.current] = color)}
      />
      <h1>{snap.current}</h1>
    </div>
  );
}
```

---
layout: bullets
---

# Links
-  Source code - [link](https://github.com/rashidmp/shoe-configurator)
- React three fiber -[link](https://docs.pmnd.rs/react-three-fiber/getting-started/introduction)
- Drei -[link](https://github.com/pmndrs/drei#readme)

---
layout: intro
---


# Thank You! 🙏
We hope you found this presentation helpful. For more information, tutorials, and courses, please visit [levelx.in](https://levelx.in).

Thank you for your time and happy coding!

<>