<template>
  <h3 class="text-4xl tracking-2px text-shadow-sm">
    一个three基本页面架构
  </h3>
  <canvas class="webgl mx-auto" />
</template>

<script setup lang="ts">
import { onMounted } from 'vue'

// 非常有名的GSAP动画库
import gsap from 'gsap'

import * as THREE from 'three'

import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
// 后期特效实例
import { EffectComposer } from 'three/examples/jsm/postprocessing/EffectComposer.js'

onMounted(() => {
  const canvas = document.querySelector('canvas.webgl')
  const scene = new THREE.Scene()

  /**
   * Object
   */
  const geometry = new THREE.BoxGeometry(1, 1, 1)
  const material = new THREE.MeshBasicMaterial({ color: 0xFF0000 })
  const mesh = new THREE.Mesh(geometry, material)
  scene.add(mesh)

  /**
   * 相机和画布设置
   */
  // Sizes:画布尺寸
  const sizes = {
    width: window.innerWidth,
    height: window.innerHeight,
  }
  // 设置相机对象
  // const passrender = THREE.EEffectComposer()
  const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height, 1, 1000)
  camera.position.z = 3

  scene.add(camera)

  // Cursor
  const cursor = {
    x: 0,
    y: 0,
  }
  window.addEventListener('mousemove', (event) => {
    cursor.x = event.clientX / sizes.width - 0.5
    cursor.y = -(event.clientY / sizes.height - 0.5)

    // console.log(cursor.x, cursor.y)
  })

  /**
   * render：渲染
   */
  const renderer = new THREE.WebGLRenderer({
    // 在tsconfig.json中添加如下：
    // "strictNullChecks": false
    antialias: true,
    canvas,
  })
  renderer.setSize(sizes.width, sizes.height)
  // const passrender = new EffectComposer(renderer, renderer)

  // Controls
  const controls = new OrbitControls(camera, canvas)
  controls.enableDamping = true
  // 目标点位置
  controls.target.y = -0.3

  /**
   * Animate update
   */
  // 创建时钟类
  // const clock = new THREE.Clock()

  const tick = () => {
    // Render
    renderer.render(scene, camera)

    // Time
    // const elapsedTime = clock.getElapsedTime()

    // Update objects
    // mesh.position.x = Math.cos(elapsedTime)
    // mesh.position.y = Math.sin(elapsedTime)

    // Update camera
    controls.update()

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
  }

  tick()
})
</script>

<style lang="scss" scoped></style>
