
<!DOCTYPE html>
<html lang="en">
	<head>
		<title>three.js webgl - геометрические фигуры</title>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
		<link type="text/css" rel="stylesheet" href="https://threejs.org/examples/main.css">
	</head>
	<body>
		<div id="info">
			АкулининаТВ М31с 1 вариант - Трехмерные фигуры
		</div>

		<script type="module">

			import * as THREE from 'https://threejs.org/build/three.module.js';

			import { OrbitControls } from 'https://threejs.org/examples/jsm/controls/OrbitControls.js';

			var camera, scene, renderer;
			var controls;
			var ambientLight, light;
			init();
			animate();

			function init() {

				var container = document.createElement( 'div' );
				document.body.appendChild( container );

				// CAMERA
				camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 1, 8000 );
				camera.position.set( 300, 700, 900 );

				// LIGHTS
				ambientLight = new THREE.AmbientLight( 0x333333 );	// 0.2

				light = new THREE.DirectionalLight( 0xFFFFFF, 1.0 );
				light.position.set( 1, 1, 1 );				
				// direction is set in GUI

				// RENDERER
				renderer = new THREE.WebGLRenderer( { antialias: true } );
				renderer.setPixelRatio( window.devicePixelRatio );
				renderer.setSize( window.innerWidth, window.innerHeight );
				container.appendChild( renderer.domElement );

				// EVENTS
				window.addEventListener( 'resize', onWindowResize, false );

				// CONTROLS
				controls = new OrbitControls( camera, renderer.domElement );
				controls.addEventListener( 'change', render );
				//controls.rotateSpeed = 1; 
				controls.enableZoom = true;  
				controls.zoomSpeed = 0.5;  

				controls.minDistance = 500;
				controls.maxDistance = 2500;
				
				controls.enableDamping = true;

				// scene itself
				scene = new THREE.Scene();
				scene.background = new THREE.Color( 0xD3D3D3 );

				scene.add( ambientLight );
				scene.add( light );
			

				// scene objects
					var x = 0;var y = 0;var z = 0;
					//конус
					var radiusTop = 0; var radiusBottom = 100;
					var heigth = 150; var segments = 3;
					var geometry = new THREE.CylinderGeometry( radiusTop, radiusBottom, heigth, segments );
					var material = new THREE.MeshPhongMaterial( { color: 0x66ff33 } );
					var Cylinder = new THREE.Mesh( geometry, material );
					Cylinder.position.set( x-500, y+300, z );
					//Cube.rotation.y = Math.PI / 6;
					scene.add( Cylinder ); 
					var geometry = new THREE.SphereGeometry(100, 50, 50); 
					var material = new THREE.MeshPhongMaterial( { color: 0x1E3AC4 } );
					var Sphere1 = new THREE.Mesh( geometry, material );
					Sphere1.position.set( x-500, y-300, z );
					scene.add( Sphere1 );

				var textureLoader = new THREE.TextureLoader();
				var texture = textureLoader.load( 'kot.jpg' );
				var material = new THREE.MeshBasicMaterial( { map: texture } );
	
			//	var material = new THREE.MeshPhongMaterial( { color: 0x177245 } );	
					var geometry = new THREE.BoxGeometry( 150, 150, 150 );
					var Cube = new THREE.Mesh( geometry, material );
					Cube.position.set( x-200, y, z );
					//Cube.rotation.y = Math.PI / 6;
					scene.add( Cube );				


				
//конус
					var radiusTop = 0; var radiusBottom = 100;
					var heigth = 200; var segments = 30;
					var geometry = new THREE.CylinderGeometry( radiusTop, radiusBottom, heigth, segments );
					var material = new THREE.MeshPhongMaterial( { color: 0x99e6ff } );
					var Cylinder = new THREE.Mesh( geometry, material );
					Cylinder.position.set( x+100, y, z );
					//Cube.rotation.y = Math.PI / 6;
					scene.add( Cylinder ); 

var radiusTop = 80;
var radiusBottom = 80;
var heigth = 190; var segments = 3;
var geometry = new THREE.CylinderGeometry(
radiusTop, radiusBottom, heigth, segments );
var material = new THREE.MeshPhongMaterial( { color: 0xff0000 } );
var prism = new THREE.Mesh( geometry, material );
prism.position.set( x-200, y-300, z );
prism.rotation.x = Math.PI/-2;
scene.add( prism );


					//Цилиндр
					var radiusTop = 50; var radiusBottom = 50;
                                        var heigth = 150; var segments = 16;
					var geometry = new THREE.CylinderGeometry( radiusTop, radiusBottom, heigth, segments );
					var material = new THREE.MeshPhongMaterial( { color: 0xFF4500 } );
					var Cylinder = new THREE.Mesh( geometry, material );
					Cylinder.position.set( x+100, y-300, z  );
					//Cube.rotation.y = Math.PI / 6;
					scene.add( Cylinder );

					

					
					var radiusTop = 100; var radiusBottom = 100;
					var heigth = 150; var segments = 6;
					
					var geometry = new THREE.CylinderGeometry( 
						radiusTop, radiusBottom, heigth, segments );
						
					var material = new THREE.MeshPhongMaterial( { color: 0xb399ff } );
					var piramida = new THREE.Mesh( geometry, material );
					piramida.position.set( 400, y-300, z ); 
					//piramida.rotation.x = -Math.PI/2; 					
					
					scene.add( piramida );

				
                       var textureLoader = new THREE.TextureLoader();
				var texture = textureLoader.load( 'kote.png' );
			//	var material = new THREE.MeshBasicMaterial( { map: texture } );
	
				var material = new THREE.MeshPhongMaterial( { color: 0xffff00 } );	
					var geometry = new THREE.BoxGeometry( 150, 250, 150 );
					var Cube = new THREE.Mesh( geometry, material );
					Cube.position.set( x+400, y+200, z );
					//Cube.rotation.y = Math.PI / 6;
					scene.add( Cube );
	}
			

			// EVENT HANDLERS


			function onWindowResize() {

				camera.aspect = window.innerWidth / window.innerHeight;
				camera.updateProjectionMatrix();

				renderer.setSize( window.innerWidth, window.innerHeight );

			}

			//

			function animate() {

				requestAnimationFrame( animate );
				controls.update(); //
				render();

			}

			function render() {

				renderer.render( scene, camera );

			}			


		</script>

	</body>
</html>
