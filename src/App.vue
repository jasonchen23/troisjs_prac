<template>
  <Renderer ref="renderer" antialias :orbit-ctrl="{ enableDamping: true, target }" resize shadow>
    <Camera :position="{ x:100, y: 30, z: 100 }" />
    <Scene ref="scene" background="#a0a0a0">
      <HemisphereLight :intensity="0.6" />

      <DirectionalLight
        :position="{ x: 100, y: 200, z: 100 }"
        cast-shadow :shadow-camera="{ top: 180, bottom: -120, left: -120, right: 30 }"
      />

      <!-- <Plane :width="2000" :height="2000" :rotation="{ x: -Math.PI / 2 }" receive-shadow>
        <PhongMaterial color="#999999" :props="{ depthWrite: false }" />
      </Plane> -->

      <GltfModel src="/src/assets/untitled.gltf" @load="onLoad" @error="onError" />
    </Scene>
  </Renderer>
</template>

<script>
// Model from mixamo.com
import { AnimationMixer, Clock, Fog, GridHelper, Vector3 } from 'three';
import {
  AmbientLight,
  Camera,
  DirectionalLight,
  GltfModel,
  HemisphereLight,
  Renderer,
  PhongMaterial,
  Plane,
  Scene,
} from 'troisjs';
export default {
  components: {
    AmbientLight,
    Camera,
    DirectionalLight,
    GltfModel,
    HemisphereLight,
    Renderer,
    PhongMaterial,
    Plane,
    Scene,
  },
  data() {
    return {
      target: new Vector3(20, 20, 20),
    };
  },
  mounted() {
    const renderer = this.$refs.renderer.renderer;
    renderer.setSize( window.innerWidth, window.innerHeight );
    const scene = this.$refs.scene.scene;
    scene.fog = new Fog(0xa0a0a0, 200, 1000);
    const grid = new GridHelper(2000, 200, 0x000000, 0x000000);
    grid.material.opacity = 0.5;
    grid.material.transparent = true;
    this.$refs.scene.add(grid);
  },
  methods: {
    onLoad(object) {
      // this.mixer = new AnimationMixer(object);
      // const action = this.mixer.clipAction(object.animations[0]);
      // action.play();
    //   object.traverse(function (child) {
    //     if (child.isMesh) {
    //       child.castShadow = true;
    //       child.receiveShadow = true;
    //     }
    //   });
    //   this.clock = new Clock();
    //   this.$refs.renderer.onBeforeRender(this.updateMixer);
    },
    updateMixer() {
      this.mixer.update(this.clock.getDelta());
    },
  },
};
</script>

<style>
canvas{
  width:100%;
  height: 100vh;
}
</style>