<script>
  import { Canvas, useFrame } from '@threlte/core';
  import { PerspectiveCamera, OrbitControls } from '@threlte/extras';
  import { onMount } from 'svelte';

  let cube;

  onMount(() => {
    cube.rotation.x = Math.PI / 4;
    cube.rotation.y = Math.PI / 4;
  });

  useFrame(({ clock }) => {
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
  });
</script>

<Canvas>
  <PerspectiveCamera position={[0, 0, 5]} />
  <OrbitControls />
  <mesh bind:this={cube}>
    <boxGeometry args={[1, 1, 1]} />
    <meshStandardMaterial color="orange" />
  </mesh>
</Canvas>

<style>
  canvas {
    display: block;
  }
</style>
