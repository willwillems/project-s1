<script>
  import { onMount } from 'svelte'
  import * as THREE from 'three';

  import Stats from 'three/examples/jsm/libs/stats.module.js';
  import { GUI } from 'three/examples/jsm/libs/dat.gui.module.js';

  import { STLLoader } from 'three/examples/jsm/loaders/STLLoader.js';
  import { TrackballControls } from 'three/examples/jsm/controls/TrackballControls.js';

  const heightRatio = 1

  let mouseDown = false
  document.body.addEventListener('mousedown', () => { mouseDown = true });
  document.body.addEventListener('mouseup',   () => { mouseDown = false });


  let renderCanvas;

  var radius = 3; 

  var perspectiveCamera, controls, scene, renderer, stats;

  var frustumSize = 400;

  onMount(() => {
    init();
    animate();
  })

  function init() {

    var aspect = window.innerWidth / (window.innerHeight * heightRatio);

    perspectiveCamera = new THREE.PerspectiveCamera( 35, window.innerWidth / (window.innerHeight * heightRatio), 1, 15 );
    perspectiveCamera.position.set( 0, 0, 3 );

    // world

    scene = new THREE.Scene();
    scene.background = new THREE.Color( 0x000000 );
    // scene.fog = new THREE.FogExp2( 0xcccccc, 0.002 );

    var geometry = new THREE.CylinderBufferGeometry( 0, 10, 30, 4, 1 );
    var material = new THREE.MeshPhongMaterial( { color: 0xffffff, flatShading: true } );

     // ASCII file

    var loader = new STLLoader();
    loader.load( '/models/s1.stl', function ( geometry ) {

      var material = new THREE.MeshPhongMaterial( { color: 0x444444, specular: 0x111111, shininess: 100 } );
      var mesh = new THREE.Mesh( geometry, material );

      mesh.position.set( 0, 0, 0 );
      mesh.rotation.set( - Math.PI / 3, Math.PI / 16,  Math.PI / 3 );
      mesh.scale.set( 0.15, 0.15, 0.15 );
      mesh.translateX( -0.45 ); mesh.translateY( -1 ); mesh.translateZ( -0.2 )

      mesh.castShadow = true;
      mesh.receiveShadow = true;

      scene.add( mesh );

    } );

    // lights

    var light = new THREE.DirectionalLight( 0xffffff );
    light.position.set( 1, 1, 1 );
    scene.add( light );

    var light = new THREE.DirectionalLight( 0xffbc3d );
    light.position.set( 6, 2, 8 );
    scene.add( light );

    var light = new THREE.AmbientLight( 0x222222 );
    scene.add( light );

    // renderer

    renderer = new THREE.WebGLRenderer( { canvas: renderCanvas, antialias: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, (window.innerHeight * heightRatio) );

    //

    window.addEventListener( 'resize', onWindowResize, false );

    createControls( perspectiveCamera );

  }

  function createControls( camera ) {

    controls = new TrackballControls( camera, document.body ); // document.getElementById('main') );

    controls.rotateSpeed = 1.0;
    controls.zoomSpeed = 1.2;
    controls.panSpeed = 0.8;
    controls.noZoom = true;

    controls.keys = [ 65, 83, 68 ];

  }

  function onWindowResize() {

    var aspect = window.innerWidth / (window.innerHeight * heightRatio);

    perspectiveCamera.aspect = aspect;
    perspectiveCamera.updateProjectionMatrix();

    renderer.setSize( window.innerWidth, (window.innerHeight * heightRatio) );

    controls.handleResize();

  }

  function animate() {
    if (!mouseDown) {
      const angle = Math.acos(perspectiveCamera.position.x / radius) + 0.001
      perspectiveCamera.position.x = radius * Math.cos( angle );  
      perspectiveCamera.position.z = radius * Math.sin( angle )
    }

    requestAnimationFrame( animate );

    controls.update();

    render();

  }

  function render() {

    var camera = perspectiveCamera;

    renderer.render( scene, camera );

  }
</script>

<canvas id="three" bind:this={renderCanvas}></canvas>

<style>
canvas#three {
  position: fixed;
  top: 0;
  z-index: -1;
}
</style>