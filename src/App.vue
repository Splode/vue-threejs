<template>
  <div id="app">
    <div class="controls">
      <input type="range" v-model="distance" max="10" min="1">
      <input type="range" v-model="rotation">
    </div>
  </div>
</template>

<script>
const THREE = require('three');
export default {
  data() {
    return {
      distance: 5,
      rotation: 1,
    }
  },
  created() {
    const vm = this;

    var scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);

    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    var geometry = new THREE.BoxGeometry(1, 1, 1);
    var material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    var cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    camera.position.z = 5;

    function animate() {
      requestAnimationFrame(animate);
      renderer.render(scene, camera);

      camera.position.z = vm.distance;
      cube.rotation.x = vm.rotation;
      cube.rotation.y = vm.rotation;
    }
    animate();
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: relative;
}

body {
  overflow: hidden;
  margin: 0;
}

canvas {
  width: 100%;
  height: 100%;
}



/* input[type=range] {
  position: absolute;
  bottom: 10;
} */

.controls {
  position: absolute;
}
</style>
