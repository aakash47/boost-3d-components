<template>
<div>
  <div>
    <h1>input</h1>
    <form @submit.prevent="appear"  action="">
       <input v-model="models" type="text">
      <input type="submit" value="search"  >
      <!-- {{models}} -->
      <div class="object" id="scene-container" ref="sceneContainer">
      </div>
    </form>
   
  </div>
  
  
      
      
  </div>
  
</template>

<script>import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader'
// import Stats from 'stats.js'
export default {
    name:"Input",
    data(){
        return{
      size:1,
      models:"",
      container: null,
      scene: null,
      camera: null,
      controls: null,
      renderer: null,
      map:null,
      
        } 
    },
    methods:{
      
        appear(){
              if (this.models == "white house"){
              this.size=0.13
              }
              if (this.models == "taj mahal"){
              
              this.size=0.04
              }
              if (this.models == "usa flag"){
              
              this.size=0.003
              }
              if (this.models == "michigan central station"){
              
              this.size=0.07
              }
              if (this.models == "india flag"){
              this.size=2.4
              }
              if (this.models == "obama"){
              this.size=16
              }
              if (this.models == "boat"){
              this.size=3
              }
      const model_div = document.getElementById('scene-container');
      model_div.innerHTML = '';
      this.container = null
      this.container = this.$refs.sceneContainer

      console.log(this.container)


      // add camera
      const fov = 60 // Field of view
      const aspect = this.container.clientWidth / this.container.clientHeight
      const near = 0.1 // the near clipping plane
      const far = 30 // the far clipping plane
      const camera = new THREE.PerspectiveCamera(fov, aspect, near, far)
      camera.position.set(0, 5, 10)
      this.camera = camera

      // create scene
      this.scene = new THREE.Scene()
      this.scene.background = new THREE.Color('skyblue')

      // add lights
      const ambientLight = new THREE.HemisphereLight(
        0xffffff, // bright sky color
        0x222222, // dim ground color
        1 // intensity
      )
      const mainLight = new THREE.DirectionalLight(0xffffff, 4.0)
      mainLight.position.set(10, 10, 10)
      this.scene.add(ambientLight, mainLight)

      // add controls
      this.controls = new OrbitControls(this.camera, this.container)

      // create renderer
      this.renderer = new THREE.WebGLRenderer({ antialias: true })
      this.renderer.setSize(this.container.clientWidth, this.container.clientHeight)
      this.renderer.setPixelRatio(window.devicePixelRatio)
      this.renderer.gammaFactor = 2.2
      this.renderer.outputEncoding = THREE.sRGBEncoding
      this.renderer.physicallyCorrectLights = true
      this.container.appendChild(this.renderer.domElement)

      // set aspect ratio to match the new browser window aspect ratio
      this.camera.aspect = this.container.clientWidth / this.container.clientHeight
      this.camera.updateProjectionMatrix()
      this.renderer.setSize(this.container.clientWidth, this.container.clientHeight)
      const loader = new GLTFLoader()

      loader.load(
        `/three-assets/${this.models}/scene.gltf`,
        gltf => {
            // this.reload()
            this.scene.add(gltf.scene)
            this.map =gltf.scene.children[0];
            this.map.scale.set(this.size,this.size,this.size);
            this.models=""
                              // this.map.position.set(2,1,0)
        },
                            

        undefined,
        undefined
      )

      this.renderer.setAnimationLoop(() => {
        // this.reload()
        this.render()
        
              // this.renderer="";

      })
    },
    render () {
      this.renderer.render(this.scene, this.camera)
    },
    
   
        },
    }


</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#scene-container {
  height: 100vh;
}
</style>
