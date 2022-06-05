<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';

	let width = 1;
	let height = 0.15;
	let depth = 1.5;
	let spin = 0;

	SC.onFrame(() => {
		spin += 0.01;
	});
</script>

<SC.Canvas
	antialias
	background={new THREE.Color(0x00bfa5)}
	shadows
	fog={new THREE.FogExp2(0x00bfa5, 0.1)}
>
	<SC.Mesh
		geometry={new THREE.BoxGeometry()}
		material={new THREE.MeshStandardMaterial({ color: 0xaa00ff })}
		scale={[width, height, depth]}
		rotation={[0, spin, 0]}
		castShadow
	/>

	<SC.PerspectiveCamera position={[1, 1, 3]} />
	<SC.OrbitControls enableZoom={false} maxPolarAngle={Math.PI * 0.51} />
	<SC.AmbientLight intensity={0.6} />
	<SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} shadow={{ mapSize: [2048, 2048] }} />
	<SC.Group position={[0, -height / 2, 0]}>
		<SC.Mesh
			geometry={new THREE.PlaneGeometry(50, 50)}
			material={new THREE.MeshStandardMaterial({ color: 0x1de9b6 })}
			rotation={[-Math.PI / 2, 0, 0]}
			receiveShadow
		/>

		<SC.Primitive
			object={new THREE.GridHelper(50, 50, 0x444444, 0x555555)}
			position={[0, 0.001, 0]}
		/>
	</SC.Group>
</SC.Canvas>

<style>
</style>
