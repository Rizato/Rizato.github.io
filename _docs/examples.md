---
layout: doc
title: Examples
description: Example programs written in Ragelang
order: 3
---

# Ragelang Examples

This page contains example programs demonstrating various features of Ragelang. Use these as learning resources or starting points for your own projects.


## Note

Not human review or tested.

Additionally, the examples don't have supports, so they won't run in the current state.

## Table of Contents

- [Hello World](#hello-world)
- [Bouncing Ball](#bouncing-ball)
- [Platformer](#platformer)
- [Particle System](#particle-system)
- [Simple Menu](#simple-menu)
- [Collision Detection](#collision-detection)
- [Pattern Matching](#pattern-matching)

---

## Hello World

The simplest Ragelang program:

```rage
draw {
  clear("#1a1a2e")
  text("Hello, World!", 200, 200, 32, "#ffffff")
}
```

With animation:

```rage
time = 0
draw {
  clear("#1a1a2e")
  
  // Animated color using time
  hue = (time * 50) % 360
  color = hsl(hue, 80, 60)
  
  text("Hello, Ragelang!", 150, 200, 36, color)
}

update(dt) {
    time = time + 1
}
```

---

## Bouncing Ball

A classic bouncing ball animation:

```rage
// Ball state
ball_x = 300
ball_y = 200
vel_x = 150
vel_y = 100

draw {
  clear("#1a1a2e")
  circle(ball_x, ball_y, 20, "#ff3366")
  text("Bouncing Ball", 10, 30, 24, "#ffffff")
}

update(dt) {
  // Move ball
  ball_x = ball_x + vel_x * dt
  ball_y = ball_y + vel_y * dt
  
  // Bounce off right/left walls
  if (ball_x > 580) {
    vel_x = -vel_x
    ball_x = 580
  }
  if (ball_x < 20) {
    vel_x = -vel_x
    ball_x = 20
  }
  
  // Bounce off bottom/top walls
  if (ball_y > 380) {
    vel_y = -vel_y
    ball_y = 380
  }
  if (ball_y < 20) {
    vel_y = -vel_y
    ball_y = 20
  }
}
```

---

## Platformer

A simple platformer with controls, gravity, and a jump trail effect:

```rage
// Player setup
player = prototype()
player.x = 100
player.y = 300
player.vel_y = 0
player.on_ground = true

// Physics constants
gravity = 800
jump_force = -400
move_speed = 200

// World
ground_y = 350

// Trail system for visual effect
trail = []
trail_max = 8

// Apply gravity to player
fun apply_gravity(dt) {
  if (player.on_ground == false) {
    player.vel_y = player.vel_y + gravity * dt
  }
}

// Update trail when jumping
fun update_trail() {
  if (player.on_ground == false) {
    pos = prototype()
    pos.x = player.x
    pos.y = player.y
    push(trail, pos)
    
    // Limit trail length
    loop {
      if (len(trail) <= trail_max) {
        break
      }
      trail = trail[1:]
    }
  }
}

draw {
  clear("#2d3436")
  
  // Draw ground
  rect(0, ground_y, 600, 50, "#636e72")
  
  // Draw trail when jumping
  if (len(trail) > 0) {
    i = 0
    loop {
      if (i >= len(trail)) {
        break
      }
      pos = trail[i]
      t = i / trail_max
      alpha = cos(t * 1.5708) * 0.6
      rect(pos.x, pos.y, 32, 32, "#00cec9", alpha)
      i = i + 1
    }
  }
  
  // Draw player
  rect(player.x, player.y, 32, 32, "#00cec9")
  
  // Instructions
  text("Arrows/WASD to move, Space to jump", 10, 30, 16, "#dfe6e9")
}

update(dt) {
  apply_gravity(dt)
  
  // Horizontal movement
  if (key_held("ArrowLeft") or key_held("a")) {
    player.x = player.x - move_speed * dt
  }
  if (key_held("ArrowRight") or key_held("d")) {
    player.x = player.x + move_speed * dt
  }
  
  // Jump
  if (key_pressed(" ") and player.on_ground) {
    player.vel_y = jump_force
    player.on_ground = false
    trail = []  // Clear trail on new jump
  }
  
  update_trail()
  
  // Apply vertical velocity
  player.y = player.y + player.vel_y * dt
  
  // Keep in bounds horizontally
  if (player.x < 0) {
    player.x = 0
  }
  if (player.x > 568) {
    player.x = 568
  }
  
  // Ground collision
  if (player.y > ground_y - 32) {
    player.y = ground_y - 32
    player.vel_y = 0
    player.on_ground = true
    trail = []
  }
}
```

---

## Particle System

A simple particle system with gravity and fading:

```rage
// Particle array
particles = []

// Create a new particle at position
fun spawn_particle(x, y) {
  p = prototype()
  p.x = x
  p.y = y
  p.vel_x = randomInt(-100, 100)
  p.vel_y = randomInt(-200, -50)
  p.life = 1.0
  p.color_h = randomInt(0, 360)
  push(particles, p)
}

// Spawn multiple particles
fun spawn_burst(x, y, count) {
  i = 0
  loop {
    if (i >= count) {
      break
    }
    spawn_particle(x, y)
    i = i + 1
  }
}

draw {
  clear("#0d0d1a")
  
  // Draw all particles
  i = 0
  loop {
    if (i >= len(particles)) {
      break
    }
    p = particles[i]
    color = hsla(p.color_h, 80, 60, p.life)
    size = 4 + p.life * 8
    circle(p.x, p.y, size, color)
    i = i + 1
  }
  
  text("Click to spawn particles!", 150, 30, 20, "#ffffff")
  text("Particles: " + len(particles), 10, 380, 14, "#888888")
}

update(dt) {
  // Spawn on click
  if (mouse_pressed(0)) {
    spawn_burst(mouse_x(), mouse_y(), 20)
  }
  
  // Update particles
  gravity = 300
  i = 0
  loop {
    if (i >= len(particles)) {
      break
    }
    p = particles[i]
    
    // Apply physics
    p.x = p.x + p.vel_x * dt
    p.y = p.y + p.vel_y * dt
    p.vel_y = p.vel_y + gravity * dt
    
    // Decay life
    p.life = p.life - dt * 0.8
    
    // Remove dead particles
    if (p.life <= 0) {
      // Remove by replacing with last and popping
      particles[i] = particles[len(particles) - 1]
      pop(particles)
    } else {
      i = i + 1
    }
  }
}
```

---

## Simple Menu

A menu system with keyboard navigation:

```rage
// Menu state
menu_items = ["Start Game", "Options", "Credits", "Quit"]
selected = 0
title_wave = 0

draw {
  clear("#1a1a2e")
  
  // Animated title
  title_wave = time() * 2
  title_y = 80 + sin(title_wave) * 5
  text("MY AWESOME GAME", 150, title_y, 36, "#e74c3c")
  
  // Draw menu items
  i = 0
  loop {
    if (i >= len(menu_items)) {
      break
    }
    
    y = 180 + i * 50
    
    if (i == selected) {
      // Selected item - highlight
      rect(180, y - 5, 240, 40, "#e74c3c", 0.3)
      text("> " + menu_items[i], 200, y, 24, "#ffffff")
    } else {
      text(menu_items[i], 220, y, 20, "#888888")
    }
    
    i = i + 1
  }
  
  // Instructions
  text("↑↓ Navigate   Enter Select", 170, 380, 14, "#555555")
}

update(dt) {
  // Navigate up
  if (key_pressed("ArrowUp") or key_pressed("w")) {
    selected = selected - 1
    if (selected < 0) {
      selected = len(menu_items) - 1
    }
  }
  
  // Navigate down
  if (key_pressed("ArrowDown") or key_pressed("s")) {
    selected = selected + 1
    if (selected >= len(menu_items)) {
      selected = 0
    }
  }
  
  // Select
  if (key_pressed("Enter")) {
    print("Selected: " + menu_items[selected])
  }
}
```

---

## Collision Detection

Demonstrating rectangle collision detection:

```rage
// Player (controllable box)
player = {x: 100, y: 200, w: 40, h: 40}
speed = 200

// Static obstacles
obstacles = [
  {x: 250, y: 150, w: 80, h: 80, color: "#e74c3c"},
  {x: 400, y: 250, w: 60, h: 100, color: "#3498db"},
  {x: 150, y: 300, w: 100, h: 50, color: "#2ecc71"}
]

// Collision state
colliding = false

draw {
  clear("#1a1a2e")
  
  // Draw obstacles
  i = 0
  loop {
    if (i >= len(obstacles)) {
      break
    }
    o = obstacles[i]
    rect(o.x, o.y, o.w, o.h, o.color)
    i = i + 1
  }
  
  // Draw player
  player_color = "#ff0000"
  if (!colliding) {
    player_color = "#ffffff"
  }
  rect(player.x, player.y, player.w, player.h, player_color)
  
  // UI
  status = "No collision"
  if (colliding) {
    status = "COLLISION!"
  }
  text(status, 10, 30, 20, "#ffffff")
  text("Arrow keys to move", 10, 380, 14, "#888888")
}

update(dt) {
  // Movement
  if (held("left")) {
    player.x = player.x - speed * dt
  }
  if (held("right")) {
    player.x = player.x + speed * dt
  }
  if (held("up")) {
    player.y = player.y - speed * dt
  }
  if (held("down")) {
    player.y = player.y + speed * dt
  }
  
  // Check collisions
  colliding = false
  i = 0
  loop {
    if (i >= len(obstacles)) {
      break
    }
    o = obstacles[i]
    
    if (rect_overlap(player.x, player.y, player.w, player.h,
                     o.x, o.y, o.w, o.h)) {
      colliding = true
      break
    }
    
    i = i + 1
  }
}
```

---

## Pattern Matching

Demonstrating enums and pattern matching:

```rage
// Define player states
enum PlayerState {
  Idle,
  Walking(speed),
  Jumping(height, velocity),
  Attacking(damage)
}

// Current state
state = Idle
state_time = 0

// Player position
player_x = 300
player_y = 250

draw {
  clear("#2d3436")
  
  // Get state description using match
  description = match state {
    Idle => "Standing still",
    Walking(s) => "Walking at " + s,
    Jumping(h, v) => "Jumping! Height: " + round(h),
    Attacking(d) => "Attack! Damage: " + d,
    _ => "Unknown"
  }
  
  // Get player color based on state
  color = match state {
    Idle => "#00ff00",
    Walking(s) => "#00ffff",
    Jumping(h, v) => "#ffff00",
    Attacking(d) => "#ff0000",
    _ => "#ffffff"
  }
  
  // Draw player
  rect(player_x - 20, player_y - 40, 40, 40, color)
  
  // Draw ground
  rect(0, player_y, 600, 150, "#636e72")
  
  // UI
  text("State: " + description, 10, 30, 18, "#ffffff")
  text("Press: I=Idle, W=Walk, J=Jump, A=Attack", 10, 380, 14, "#888888")
}

update(dt) {
  state_time = state_time + dt
  
  // State changes via keyboard
  if (key_pressed("i")) {
    state = Idle
    state_time = 0
  }
  if (key_pressed("w")) {
    state = Walking(100)
    state_time = 0
  }
  if (key_pressed("j")) {
    state = Jumping(50, -200)
    state_time = 0
  }
  if (key_pressed("a")) {
    state = Attacking(25)
    state_time = 0
  }
  
  // Process current state
  match state {
    Walking(speed) => {
      player_x = player_x + speed * dt
      if (player_x > 550) {
        player_x = 50
      }
    },
    Attacking(damage) => {
      // Auto-return to idle after attack
      if (state_time > 0.5) {
        state = Idle
      }
    },
    _ => {
      // Idle and other states
    }
  }
}
```

---

## More Examples

### Rainbow Circle

```rage
draw {
  clear("#000000")
  
  t = time()
  i = 0
  loop {
    if (i >= 12) {
      break
    }
    angle = rad(i * 30) + t
    x = 300 + cos(angle) * 100
    y = 200 + sin(angle) * 100
    hue = (i * 30 + t * 50) % 360
    circle(x, y, 20, hsl(hue, 80, 60))
    i = i + 1
  }
}
```

### Mouse Follower

```rage
target_x = 300
target_y = 200
follower_x = 300
follower_y = 200

draw {
  clear("#1a1a2e")
  
  // Draw line between follower and target
  line(follower_x, follower_y, target_x, target_y, "#333333", 2)
  
  // Draw target (mouse position)
  circle(target_x, target_y, 10, "#e74c3c")
  
  // Draw follower
  circle(follower_x, follower_y, 15, "#3498db")
  
  text("Move your mouse!", 220, 30, 16, "#ffffff")
}

update(dt) {
  // Update target to mouse position
  target_x = mouse_x()
  target_y = mouse_y()
  
  // Smooth follow using lerp
  follower_x = lerp(follower_x, target_x, 5 * dt)
  follower_y = lerp(follower_y, target_y, 5 * dt)
}
```

### Starfield

```rage
// Create stars
stars = []
i = 0
loop {
  if (i >= 100) {
    break
  }
  star = {
    x: randomInt(0, 600),
    y: randomInt(0, 400),
    z: random() * 3 + 0.5,
    brightness: random()
  }
  push(stars, star)
  i = i + 1
}

draw {
  clear("#000005")
  
  i = 0
  loop {
    if (i >= len(stars)) {
      break
    }
    s = stars[i]
    size = s.z
    alpha = s.brightness * (0.5 + sin(time() * 2 + i) * 0.5)
    circle(s.x, s.y, size, rgba(255, 255, 255, alpha))
    i = i + 1
  }
}

update(dt) {
  // Move stars
  i = 0
  loop {
    if (i >= len(stars)) {
      break
    }
    s = stars[i]
    s.x = s.x - s.z * 50 * dt
    
    // Wrap around
    if (s.x < 0) {
      s.x = 600
      s.y = randomInt(0, 400)
    }
    
    i = i + 1
  }
}
```
