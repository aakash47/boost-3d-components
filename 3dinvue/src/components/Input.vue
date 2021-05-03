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
      models:"",
      container: null,
      scene: null,
      camera: null,
      controls: null,
      renderer: null,
      // stats: null,
      map:null,
        } 
    },
    methods:{
      
        appear(){
                    // window.location.reload()

            alert(this.models)
             // set container
                    //  this.scene.remove()
      this.container = null
      this.container = this.$refs.sceneContainer
      // delete this.$refs.sceneContainer
      // this.$refs.sceneContainer=0
      // add stats
      // this.stats = new Stats()
    //   this.container.appendChild(this.stats.dom)

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
            this.map.scale.set(4,4,4);
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
      // this.stats.update()
      
            // this.renderer.render(this.scene, this.camera).remove()


            // this.reload()


    },
    
    // reload (){
    // window.location.reload()

    // }
   
        },
       
        // destroyed () {
        //             

        // }
        // beforedestroyed () {
        //  delete this.appear()
        // }
    }


</script>

<style scoped>
/* #scene-container{

  height:100vh ;
} */
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
/* .bg{
  background:#ffffff ;
} */
#scene-container {
  height: 100vh;
}
</style>
