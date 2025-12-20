<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>FE!N - Super Wide Smoke</title>
    <style>
        body { margin: 0; overflow: hidden; background-color: #000; }
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

        // 1. SETUP
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 30, 100); 

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // 2. LIGHTING
        scene.add(new THREE.AmbientLight(0xffffff, 0.4));
        const strobeLight = new THREE.PointLight(0xffffff, 0, 300); 
        strobeLight.position.set(0, 40, 50);
        scene.add(strobeLight);

        const controls = new OrbitControls(camera, renderer.domElement);
        controls.enableDamping = true;

        // 3. SUPER WIDE SMOKE SYSTEM
        const smokeParticles = [];
        const smokeGeometry = new THREE.SphereGeometry(1.5, 8, 8); 
        const smokeMaterial = new THREE.MeshBasicMaterial({ 
            color: 0x999999, 
            transparent: true, 
            opacity: 0.4 
        });

        for (let i = 0; i < 80; i++) { // More particles for thickness
            const particle = new THREE.Mesh(smokeGeometry, smokeMaterial.clone());
            particle.visible = false;
            scene.add(particle);
            smokeParticles.push(particle);
        }

        function resetParticle(p) {
            // START POSITION: Much wider (25) and higher up (15)
            p.position.set((Math.random() - 0.5) * 25, 15, (Math.random() - 0.5) * 25);
            p.scale.set(1, 1, 1);
            p.material.opacity = 0.4;
        }

        // 4. MODEL LOADING
        let travisNormal = null, travisSmoke = null;

        function loadModel(name, callback) {
            const mtlLoader = new MTLLoader();
            mtlLoader.load(`${name}.mtl`, (materials) => {
                materials.preload();
                const objLoader = new OBJLoader();
                objLoader.setMaterials(materials);
                objLoader.load(`${name}.obj`, (object) => {
                    const box = new THREE.Box3().setFromObject(object);
                    const center = box.getCenter(new THREE.Vector3());
                    object.position.sub(center); 
                    
                    if (name === 'fien') {
                        object.rotation.x = 40 * (Math.PI / 180); 
                    } else {
                        object.rotation.x = 0; // Standing up
                    }
                    
                    object.visible = false;
                    scene.add(object);
                    callback(object);
                });
            });
        }

        loadModel('fien', (obj) => { travisNormal = obj; travisNormal.visible = true; });
        loadModel('fien_smoke', (obj) => { travisSmoke = obj; });

        // 5. ANIMATION LOOP
        const clock = new THREE.Clock();

        function animate() {
            requestAnimationFrame(animate);
            const elapsed = clock.getElapsedTime();
            const isSmokingTime = Math.floor(elapsed / 10) % 2 === 1;

            if (travisNormal && travisSmoke) {
                travisNormal.visible = !isSmokingTime;
                travisSmoke.visible = isSmokingTime;

                travisNormal.rotation.y += 0.12;
                travisSmoke.rotation.y += 0.01;

                // Super Wide Smoke Logic
                smokeParticles.forEach((p) => {
                    if (isSmokingTime) {
                        p.visible = true;
                        p.position.y += 0.18; // Slightly faster rise
                        p.scale.x += 0.1;    // Rapid horizontal growth
                        p.scale.z += 0.1;
                        p.scale.y += 0.05;
                        p.material.opacity -= 0.002; // Fades very slowly to stay massive

                        if (p.material.opacity <= 0) resetParticle(p);
                    } else {
                        p.visible = false;
                        resetParticle(p);
                    }
                });

                strobeLight.intensity = (Math.sin(elapsed * 30) > 0.7) ? 60 : 0;
            }

            controls.update(); 
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
