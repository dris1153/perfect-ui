# Three.js Integration Patterns for Landing Pages

How to add a 3D layer to a Next.js landing without tanking performance or vibe cohesion.

## When to Add 3D

3D earns its place when it does one of these:
1. **Express the product** — rotating headphones, animated chart, GLB of the actual app
2. **Express the vibe** — particle field for retro-futuristic, glass forms for glass-tech
3. **Reward interaction** — draggable element, scroll-linked camera move

3D is a **cost** when:
- Adds ≥150KB to bundle for decorative purpose only
- Plays at >30% CPU on mid-range mobile
- Replaces what a static SVG could express

## Stack: React Three Fiber (RTF)

In Next.js, ALWAYS use `@react-three/fiber` + `@react-three/drei`. NEVER raw Three.js. RTF gives:
- Declarative scene = readable code
- Automatic disposal of geometries/materials
- Built-in Suspense + loaders integration
- `drei` helpers for cameras/controls/loaders

### Install
```bash
npm i three @react-three/fiber @react-three/drei
npm i -D @types/three
```

### Boilerplate
```tsx
// app/components/three/scene.tsx
'use client';
import { Canvas } from '@react-three/fiber';
import { Environment, OrbitControls } from '@react-three/drei';
import { Suspense } from 'react';

export const Scene = () => (
  <Canvas
    dpr={[1, 2]}
    gl={{ antialias: true, alpha: true }}
    camera={{ position: [0, 0, 5], fov: 45 }}
    frameloop="demand"
  >
    <Suspense fallback={null}>
      <ambientLight intensity={0.4} />
      <directionalLight position={[3, 3, 3]} intensity={1} />
      <Environment preset="studio" />
      {/* scene contents */}
    </Suspense>
  </Canvas>
);
```

### Lazy import in page
```tsx
// app/page.tsx
import dynamic from 'next/dynamic';
const Scene = dynamic(
  () => import('@/components/three/scene').then((m) => m.Scene),
  { ssr: false, loading: () => <ScenePoster /> }
);
```

## Pattern 1: Hero 3D Scene

**Use when:** Phase 2d returned `hero-scene`.

Full-bleed canvas behind or beside hero copy. Vibe-driven content:
- Retro-futuristic → particle field, grid-of-dots, wireframe shapes
- Brutalist → primitive geometry (cubes/cones) at sharp angles, harsh lighting
- Luxury → rotating product GLB on glass podium with HDRI
- Glass-tech → volumetric refractive forms

### Layout
```tsx
<section className="relative min-h-[100dvh]">
  <div className="absolute inset-0">
    <Scene />
  </div>
  <div className="relative z-10 max-w-[1280px] mx-auto px-8 pt-32">
    <h1>Display headline...</h1>
  </div>
</section>
```

### Search examples
```bash
python3 ~/.claude/skills/threejs/scripts/search.py "hero scene particle abstract" -n 5
python3 ~/.claude/skills/threejs/scripts/search.py "rotating product gltf" -n 5
python3 ~/.claude/skills/threejs/scripts/search.py "wireframe geometry" -n 5
```

### Performance budget
- Bundle: 3D code ≤ 200KB gzipped (excluding GLB assets)
- GLB assets ≤ 500KB total, served as Draco-compressed
- Frame loop: `demand` if scene is mostly static, `always` only if perpetual animation
- Mobile: degrade to poster image at viewport < 768px (use `useMediaQuery`)

## Pattern 2: Scroll-Triggered 3D

**Use when:** Phase 2d returned `scroll-triggered`.

3D element animates as user scrolls. Common variants:
- Camera fly-through different scene states
- Object rotates / morphs at section boundaries
- Materials shift color/opacity to match section

### Stack
- `@react-three/fiber` for scene
- `gsap` + `ScrollTrigger` for scroll math (better than scroll-linked CSS)
- OR `framer-motion` `useScroll` + `useTransform`

### Recipe (framer-motion)
```tsx
'use client';
import { Canvas, useFrame } from '@react-three/fiber';
import { useScroll } from 'framer-motion';
import { useRef } from 'react';
import * as THREE from 'three';

function ScrollObject() {
  const ref = useRef<THREE.Mesh>(null);
  const { scrollYProgress } = useScroll();

  useFrame(() => {
    if (!ref.current) return;
    ref.current.rotation.y = scrollYProgress.get() * Math.PI * 2;
    ref.current.position.y = scrollYProgress.get() * -3;
  });

  return (
    <mesh ref={ref}>
      <torusKnotGeometry args={[1, 0.3, 128, 16]} />
      <meshStandardMaterial color="currentAccent" />
    </mesh>
  );
}
```

### Performance
- `useFrame` runs at 60fps — keep math cheap (no `new THREE.Vector3()` per frame)
- Use `scrollYProgress.get()` not state subscription (avoid React re-renders)
- Pause when off-screen via `IntersectionObserver`

## Pattern 3: Interactive Accent

**Use when:** Phase 2d returned `interactive-accent`.

Small 3D widget — a draggable card, a 3D logo that follows the cursor, a hover-to-rotate product preview.

### Recipe (cursor-tracking 3D logo)
```tsx
'use client';
import { Canvas, useFrame } from '@react-three/fiber';
import { useRef, useState } from 'react';

function LogoMark() {
  const ref = useRef<THREE.Group>(null);
  const [pointer, setPointer] = useState({ x: 0, y: 0 });

  useFrame(() => {
    if (!ref.current) return;
    ref.current.rotation.y += (pointer.x * 0.5 - ref.current.rotation.y) * 0.05;
    ref.current.rotation.x += (pointer.y * 0.5 - ref.current.rotation.x) * 0.05;
  });

  return (
    <group
      ref={ref}
      onPointerMove={(e) => setPointer({ x: e.point.x, y: e.point.y })}
    >
      {/* logo geometry */}
    </group>
  );
}
```

### Sizing
Accent canvases sit in a fixed-size box: `w-[400px] h-[400px]` or similar. Use `Canvas`'s `style` prop. Don't full-bleed.

## Vibe-Matched 3D Recipes

### Retro-futuristic: Particle Field
```bash
python3 ~/.claude/skills/threejs/scripts/search.py "particle field gpu compute" -n 3
```
Use `BufferGeometry` with 5000 points, instanced. Animate with TSL or compute shader. Color from accent palette.

### Brutalist: Primitive Cluster
Place 5-7 unsmoothed primitives (cubes, cones, cylinders) at hard angles. Single directional light, hard shadow. Material: `MeshBasicMaterial` (flat, no PBR).

### Luxury: Rotating Product GLB
Load product GLB with Draco compression. `<Environment preset="studio" />` for HDRI. Rotate slowly (0.001 rad/frame) on demand. Add `<ContactShadows />` underneath.

### Glass-tech: Refractive Forms
Use `<MeshTransmissionMaterial />` from `drei`. Single accent-colored light behind forms for glow-through. Background should be slight gradient, not flat.

### Organic: Flowing Geometry
`PlaneGeometry` with `meshStandardMaterial` + custom vertex shader for wave displacement. Subtle motion. Material color tinted to organic accent (moss, clay).

## Forbidden Three.js Patterns

- ❌ `OrbitControls` enabled by default — feels like a 3D viewer demo, not a landing
- ❌ Default `MeshNormalMaterial` rainbow — pure AI-default 3D fingerprint
- ❌ Stock physically-correct grass/water — overused
- ❌ Stats overlay (`<Stats />`) shipped to production
- ❌ `frameloop="always"` for static scenes — burns CPU
- ❌ No fallback / poster — Suspense without `<Loader />` or static image

## Performance Checklist

Before declaring 3D done:

- [ ] `dpr={[1, 2]}` set (cap pixel ratio)
- [ ] `frameloop="demand"` if scene only animates on input/scroll
- [ ] Geometries reused (don't create new in `useFrame`)
- [ ] GLB assets Draco-compressed (`gltfpack -i input.glb -o output.glb -cc`)
- [ ] Lazy-loaded with `dynamic` + `ssr: false`
- [ ] Poster image fallback while loading
- [ ] Pauses when `document.hidden` or off-screen
- [ ] Mobile fallback (degrade to static image at <768px viewport)
- [ ] Lighthouse mobile score ≥ 80

## Skipping 3D

If Phase 2d returned `none`, do NOT add 3D for "polish" or "engagement". Skip Phase 5 entirely. The cohesion rules in visual-direction.md will deliver a landing that doesn't need it.
