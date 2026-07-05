<script setup lang="ts">
import { onMounted, onBeforeUnmount, ref } from 'vue'

const canvas = ref<HTMLCanvasElement | null>(null)
let raf = 0

onMounted(() => {
  const c = canvas.value
  if (!c) return
  const ctx = c.getContext('2d')
  if (!ctx) return

  const dpr = Math.min(window.devicePixelRatio || 1, 2)
  const size = 400
  c.width = size * dpr
  c.height = size * dpr
  ctx.scale(dpr, dpr)

  const cx = size / 2
  const cy = size / 2
  const R = 138
  const N = 42
  const pts: { x: number; y: number; z: number; big: boolean }[] = []
  for (let i = 0; i < N; i++) {
    const u = Math.random()
    const v = Math.random()
    const theta = 2 * Math.PI * u
    const phi = Math.acos(2 * v - 1)
    const r = R * Math.cbrt(Math.random() * 0.85 + 0.15)
    pts.push({
      x: r * Math.sin(phi) * Math.cos(theta),
      y: r * Math.sin(phi) * Math.sin(theta),
      z: r * Math.cos(phi),
      big: Math.random() < 0.28,
    })
  }

  let t = 0
  const draw = () => {
    t += 0.0025
    ctx.clearRect(0, 0, size, size)
    const cosY = Math.cos(t)
    const sinY = Math.sin(t)
    const cosX = Math.cos(t * 0.4)
    const sinX = Math.sin(t * 0.4)
    const proj = pts.map((p) => {
      let x = p.x * cosY - p.z * sinY
      let z = p.x * sinY + p.z * cosY
      let y = p.y * cosX - z * sinX
      z = p.y * sinX + z * cosX
      const persp = (z + R * 1.7) / (R * 2.7)
      return { sx: cx + x * persp, sy: cy + y * persp, depth: persp, big: p.big }
    })

    // connections
    for (let i = 0; i < proj.length; i++) {
      for (let j = i + 1; j < proj.length; j++) {
        const dx = proj[i].sx - proj[j].sx
        const dy = proj[i].sy - proj[j].sy
        const d = Math.sqrt(dx * dx + dy * dy)
        if (d < 74) {
          const a = (1 - d / 74) * 0.5 * Math.min(proj[i].depth, proj[j].depth)
          ctx.strokeStyle = 'rgba(99,102,241,' + a.toFixed(3) + ')'
          ctx.lineWidth = 0.8
          ctx.beginPath()
          ctx.moveTo(proj[i].sx, proj[i].sy)
          ctx.lineTo(proj[j].sx, proj[j].sy)
          ctx.stroke()
        }
      }
    }

    // points
    proj.sort((a, b) => a.depth - b.depth)
    proj.forEach((p) => {
      const rad = (p.big ? 3.4 : 2.1) * p.depth + 0.6
      const alpha = 0.35 + p.depth * 0.6
      const g = ctx.createRadialGradient(p.sx, p.sy, 0, p.sx, p.sy, rad * 3.4)
      g.addColorStop(0, 'rgba(99,102,241,' + alpha.toFixed(3) + ')')
      g.addColorStop(1, 'rgba(99,102,241,0)')
      ctx.fillStyle = g
      ctx.beginPath()
      ctx.arc(p.sx, p.sy, rad * 3.4, 0, 7)
      ctx.fill()
      ctx.fillStyle = 'rgba(255,255,255,' + Math.min(1, alpha + 0.25).toFixed(3) + ')'
      ctx.beginPath()
      ctx.arc(p.sx, p.sy, rad * 0.62, 0, 7)
      ctx.fill()
    })

    raf = requestAnimationFrame(draw)
  }
  draw()
})

onBeforeUnmount(() => {
  if (raf) cancelAnimationFrame(raf)
})
</script>

<template>
  <div class="orb-float">
    <div class="orb">
      <canvas ref="canvas" class="orb-canvas" />
      <div class="orb-gloss" />
      <div class="orb-ring" />
    </div>
  </div>
</template>

<style scoped>
.orb-float {
  animation: rflFloat 7s ease-in-out infinite;
}
.orb {
  position: relative;
  width: 400px;
  height: 400px;
  max-width: 100%;
  border-radius: 50%;
  background: radial-gradient(130% 130% at 32% 26%, #ffffff 0%, #fbfbfe 44%, #eef0fe 100%);
  box-shadow:
    0 40px 90px -30px rgba(99, 102, 241, 0.45),
    inset 0 1px 2px rgba(255, 255, 255, 0.9),
    inset -18px -22px 60px rgba(99, 102, 241, 0.1);
  overflow: hidden;
}
.orb-canvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}
.orb-gloss {
  position: absolute;
  inset: 0;
  border-radius: 50%;
  background: radial-gradient(60% 45% at 30% 22%, rgba(255, 255, 255, 0.85), rgba(255, 255, 255, 0) 60%);
  pointer-events: none;
}
.orb-ring {
  position: absolute;
  inset: 0;
  border-radius: 50%;
  border: 1px solid rgba(255, 255, 255, 0.7);
  pointer-events: none;
}
@keyframes rflFloat {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-14px);
  }
}
@media (max-width: 900px) {
  .orb {
    width: 320px;
    height: 320px;
  }
}
</style>
