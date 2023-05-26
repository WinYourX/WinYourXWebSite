<template>
  <div ref="container"></div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'

const loader = new GLTFLoader()

let raycaster = new THREE.Raycaster()
let mouse = new THREE.Vector2()

const container = ref()
// 初始化渲染器
const renderer = new THREE.WebGLRenderer()
let camera = null
let cube = null
let model = null
// 1、创建场景
const scene = new THREE.Scene()
onMounted(() => {
  // 2、创建相机
  camera = new THREE.PerspectiveCamera(
    45,
    container.value.clientWidth / window.innerHeight,
    0.1,
    100
  )

  // 设置相机位置
  camera.position.set(10, 10, 10)
  scene.add(camera)

  // 添加物体
  // 创建几何体
  const cubeGeometry = new THREE.BoxGeometry(1, 1, 1)
  const cubeMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 })
  // 根据几何体和材质创建物体
  cube = new THREE.Mesh(cubeGeometry, cubeMaterial)
  console.log(cube)
  // 将几何体添加到场景中
  scene.add(cube)

  // 设置渲染的尺寸大小
  renderer.setSize(container.value.clientWidth, window.innerHeight)
  // console.log(renderer);
  // 将webgl渲染的canvas内容添加到body
  container.value.appendChild(renderer.domElement)

  // 使用渲染器，通过相机将场景渲染进来
  // renderer.render(scene, camera)
  // 创建轨道控制器
  const controls = new OrbitControls(camera, renderer.domElement)

  // 添加坐标轴辅助器
  const axesHelper = new THREE.AxesHelper(5)
  scene.add(axesHelper)

  const color = 0xffffff
  const intensity = 1
  const light = new THREE.AmbientLight(color, intensity)
  scene.add(light)

  const planeSize = 40

  const TextureLoader = new THREE.TextureLoader()
  const texture = TextureLoader.load('src/assets/img/Ground-127x127.png')
  texture.wrapS = THREE.RepeatWrapping
  texture.wrapT = THREE.RepeatWrapping
  texture.magFilter = THREE.NearestFilter
  const repeats = planeSize / 2
  texture.repeat.set(repeats, repeats)

  const planeGeo = new THREE.PlaneGeometry(planeSize, planeSize)
  const planeMat = new THREE.MeshPhongMaterial({
    map: texture,
    side: THREE.DoubleSide
  })
  const mesh = new THREE.Mesh(planeGeo, planeMat)
  mesh.rotation.x = Math.PI * -0.5
  scene.add(mesh)

  loader.load(
    'static/3d/ThreeJs.glb',
    function (gltf) {
      model = gltf.scene
      scene.add(model)
      render()
    },
    undefined,
    function (error) {
      console.error(error)
    }
  )

  window.addEventListener(
    'click',
    () => {
      //通过鼠标点击的位置计算出raycaster所需要的点的位置，以屏幕中心为原点，值的范围为-1到1.
      mouse.x = (event.clientX / window.innerWidth) * 2 - 1
      mouse.y = -(event.clientY / window.innerHeight) * 2 + 1

      // 通过鼠标点的位置和当前相机的矩阵计算出raycaster
      raycaster.setFromCamera(mouse, camera)

      // 获取raycaster直线和所有模型相交的数组集合
      let intersects = raycaster.intersectObjects(scene.children)
      console.log(intersects)

      //将所有的相交的模型的颜色设置为红色，如果只需要将第一个触发事件，那就数组的第一个模型改变颜色即可
      // TODO:诡异的点击事件
      // for (let i = 0; i < intersects.length; i++) {
      //   intersects[i].object.material.color.set(0xff0000)
      // }
    },
    false
  )
})

// 设置时钟
const clock = new THREE.Clock()

function render() {
  let time = clock.getElapsedTime()
  let t = time % 5
  cube.position.y = t
  cube.position.x = t
  model.position.y = t
  cube.rotation.y += 0.1
  model.rotation.y += 0.2
  if (cube.position.y > 5) {
    cube.position.y = 0
  }
  renderer.render(scene, camera)
  // 渲染下一帧的时候就会调用render函数
  requestAnimationFrame(render)
}
</script>

<style scoped>
#container {
  width: 100%;
  height: 100vh;
}
</style>
