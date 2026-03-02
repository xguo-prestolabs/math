# TODO — Future Visualizations

Each item is a self-contained HTML page following the same conventions as `index.html`.

---

## Physics simulations

### Projectile motion (`projectile.html`)
Connect parametric equations to real kinematics. The trajectory of a launched object is itself a parametric curve:

```
x(t) = v₀ cos(θ) · t
y(t) = v₀ sin(θ) · t − ½ g t²
```

**Adjustable parameters:**
- Initial speed `v₀`
- Launch angle `θ`
- Gravity constant `g` (so users can compare Earth vs Moon vs Mars)
- Initial height `y₀`

**Show:** the full parabolic arc, the live position dot, velocity vector arrow, max height marker, and range annotation. Animate in real time so t feels like real elapsed seconds.

### Simple pendulum (`pendulum.html`)
A pendulum is approximate SHM for small angles but diverges for large ones — a great way to show when linear approximations break down.

```
θ(t) solved via Euler integration of  θ'' = −(g/L) sin θ
```

**Parameters:** length `L`, gravity `g`, initial angle `θ₀`, optional damping coefficient. Show the bob on its string and simultaneously plot `θ` vs `t` on a side graph.

### Spring–mass system (`spring.html`)
Canonical second-order ODE. Shows SHM, damping regimes (underdamped / critically damped / overdamped), and resonance when a periodic driving force is added.

**Parameters:** spring constant `k`, mass `m`, damping coefficient `b`, optional driving frequency `ω`. Plot displacement vs time alongside the animated spring.

---

## Geometry & curves

### Polar curves (`polar.html`)
Rose curves, cardioids, limaçons — the polar coordinate system from the parametric perspective:

```
x(θ) = r(θ) cos θ,   y(θ) = r(θ) sin θ
```

Show the radius arm sweeping out while the curve is drawn. Great for building intuition before calculus.

### Conic sections (`conics.html`)
Ellipses, parabolas, and hyperbolas unified under one equation. Overlay the focus/directrix construction lines and animate the eccentricity slider from 0 (circle) through 1 (parabola) to >1 (hyperbola). Optionally connect to orbital mechanics (Kepler's first law).

---

## Signals & Fourier

### Fourier series builder (`fourier.html`)
Show how a square wave (or sawtooth, triangle) is approximated by summing harmonics. Slider for number of terms `N`. Watching Gibbs phenomenon appear and shrink as N grows is very satisfying.

### Epicycles (`epicycles.html`)
Rotating circles stacked on rotating circles — the mechanical way to draw any closed curve. Generalizes Fourier series visually. Users draw a shape with their mouse; the app decomposes it into epicycles and replays the drawing.

---

## Calculus concepts

### Derivative as slope (`derivative.html`)
Plot any of a small library of functions. A draggable point shows the tangent line, with the slope value displayed. A "zoom in" button shows local linearity — the curve becomes indistinguishable from its tangent under magnification.

### Riemann sums (`riemann.html`)
Choose left, right, or midpoint sums. Slider for number of rectangles `n`. Show the signed area value converging to the definite integral as `n` increases.

---

## Notes

- All pages should be single-file, no build step, consistent with the `:root` CSS variables in `index.html`.
- Physics simulations should use Euler or RK4 integration stepped in `requestAnimationFrame`, not closed-form solutions where the goal is to show the ODE being solved live.
- Every page should include a short plain-English explanation of the math concept in the panel, not just the formula.
