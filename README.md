<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Baby Yoda 3D Viewer</title>
    <style>
        body { margin: 0; overflow: hidden; background-color: #1a1a1a; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script type="importmap">
        {
            "imports": {
                "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
                "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
            }
        }
    </script>

    <script type="module">
        import * as THREE from 'three';
        import { OBJLoader } from 'three/addons/loaders/OBJLoader.js';
        import { MTLLoader } from 'three/addons/loaders/MTLLoader.js';
        import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

        // 1. SCENE & CAMERA SETUP
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0x222222); 

        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(20, 20, 20); // Zoomed out starting position

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // 2. LIGHTING
        scene.add(new THREE.AmbientLight(0xffffff, 1.2));
        const sun = new THREE.DirectionalLight(0xffffff, 1.5);
        sun.position.set(10, 20, 10);
        scene.add(sun);

        // 3. SMOOTH ZOOM CONTROLS
        const controls = new OrbitControls(camera, renderer.domElement);
        controls.enableDamping = true;   
        controls.dampingFactor = 0.05;   
        controls.zoomSpeed = 0.5; // Slower, smoother zoom per your request

        // 4. LOADING YOUR MODEL
        // Using your specific file name here
        const modelName = 'babyyoda'; 

        const mtlLoader = new MTLLoader();
        mtlLoader.load(`${modelName}.mtl`, (materials) => {
            materials.preload();
            const objLoader = new OBJLoader();
            objLoader.setMaterials(materials);
            objLoader.load(`${modelName}.obj`, (object) => {
                
                // Auto-center the model so it rotates correctly
                const box = new THREE.Box3().setFromObject(object);
                const center = box.getCenter(new THREE.Vector3());
                object.position.sub(center); 
                
                scene.add(object);
            }, undefined, (err) => console.error("Error loading OBJ", err));
        }, undefined, (err) => console.error("Error loading MTL", err));

        // 5. ANIMATION LOOP
        function animate() {
            requestAnimationFrame(animate);
            controls.update(); // Smooths the zoom and rotation
            renderer.render(scene, camera);
        }
        animate();

        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
