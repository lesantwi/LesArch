# LesArch
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Le Pont du Gard - 3D Model</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }
        header {
            background-color: #0077cc;
            color: white;
            padding: 15px;
            font-size: 22px;
            width: 100%;
        }
        #modelContainer {
            width: 80%;
            height: 500px;
            margin: 20px 0;
        }
        .content {
            width: 80%;
            max-width: 800px;
            text-align: left;
            margin-bottom: 20px;
        }
        .back-button {
            display: inline-block;
            padding: 10px 15px;
            background-color: #0077cc;
            color: white;
            text-decoration: none;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <header>Le Pont du Gard - 3D Interactive Model</header>

    <div class="content">
        <h2>About Le Pont du Gard</h2>
        <p>
            The Pont du Gard is an ancient Roman aqueduct bridge located in France.
            Built in the 1st century AD, it was part of a system that supplied water to the city of Nîmes.
            This UNESCO World Heritage site is one of the best-preserved Roman engineering marvels.
        </p>
    </div>

    <div id="modelContainer"></div>

    <a href="index.html" class="back-button">⬅ Back to Map</a>

    <script type="module">
        import * as THREE from 'https://cdn.jsdelivr.net/npm/three@0.158.0/build/three.module.js';
        import { GLTFLoader } from 'https://cdn.jsdelivr.net/npm/three@0.158.0/examples/jsm/loaders/GLTFLoader.js';
        import { OrbitControls } from 'https://cdn.jsdelivr.net/npm/three@0.158.0/examples/jsm/controls/OrbitControls.js';

        // Scene, Camera, Renderer
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(50, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 3, 8);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth * 0.8, 500);
        document.getElementById("modelContainer").appendChild(renderer.domElement);

        // Lighting
        const light = new THREE.AmbientLight(0xffffff, 1);
        scene.add(light);

        const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
        directionalLight.position.set(5, 10, 7).normalize();
        scene.add(directionalLight);

        // Load GLB Model
        const loader = new GLTFLoader();
        loader.load('C:/Users/User/LesArch/models/model.glb', function (gltf) {
            const model = gltf.scene;
            model.scale.set(2, 2, 2);
            scene.add(model);
        }, undefined, function (error) {
            console.error('Error loading the model:', error);
        });

        // Orbit Controls
        const controls = new OrbitControls(camera, renderer.domElement);
        controls.enableDamping = true;
        controls.dampingFactor = 0.05;
        controls.screenSpacePanning = false;
        controls.maxPolarAngle = Math.PI / 2;

        // Render Loop
        function animate() {
            requestAnimationFrame(animate);
            controls.update();
            renderer.render(scene, camera);
        }

        animate();

        // Resize Handling
        window.addEventListener('resize', () => {
            renderer.setSize(window.innerWidth * 0.8, 500);
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
        });

    </script>

</body>
</html>

Archaeological sites locator
