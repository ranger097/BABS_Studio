<script>
let main_section;
let window_width;
let window_height;
let panX = 0;
let panY = 0;

function image_function_changer(adjusted_image) {
  const scale = 0.4 + Math.random() * 0.1; 
  function random_size() {
  adjusted_image.style.scale = `${scale * 2}`;
  }

  function random_margin() {
  adjusted_image.style.margin = `${100 * scale}px`;
  }

  function random_rotation() {
  adjusted_image.style.setProperty(
  "--rotation", `${scale * -1}deg`
  );
  }
  
  let frame_id;
    function random_move() {
    let paused = false;
    let movementY = window_height;
    let image_height = adjusted_image.offsetHeight;
    function animate(time) {
    if (!paused) {
    movementY -= 0.5; 
    adjusted_image.style.setProperty("--move", `${movementY}px`);
    adjusted_image.style.setProperty("--rot-deg", `${0}deg`);
    }
    if ( movementY < -image_height ) {
      movementY = window_height;
    }
    frame_id = requestAnimationFrame(animate);

    }
        
    function pause() {
      paused = true;
    }

    function resume() {
      paused = false;
    }

    adjusted_image.addEventListener("pointerenter", pause);
    adjusted_image.addEventListener("pointerleave", resume);
    frame_id = requestAnimationFrame(animate);

 return {
     destroy() {
    cancelAnimationFrame(frame_id);
    adjusted_image.removeEventListener("pointerenter", pause);
        adjusted_image.removeEventListener("pointerleave", resume);
      }
    };
  } 

  return {
  random_size,
  random_margin,
  random_rotation,
  random_move
  };

}

function move_background(node) {
  const maxShift = 100;
  function cursor_panning(e) {
  if (!window_width || !window_height) return;

  const xPercent = (e.clientX / window_width) - 0.6;
  const yPercent = (e.clientY / window_height) - 0.6;

  const moveX = -xPercent * maxShift;
  const moveY = -yPercent * maxShift;

  node.style.transform = `translate(calc(${moveX}px + ${panX}px), calc(${moveY}px + ${panY}px))`;
  }

  window.addEventListener('mousemove', cursor_panning);

  return {
    destroy() {
      window.removeEventListener('mousemove', cursor_panning);
    }
  };
}


function pan_square(node, { x, y }) {
  let animation_frame_id = null;

  const MAX_PAN = 200; 
  const MIN_PAN = -200;

  function pan_screen() {
    let nextX = panX + x;
    let nextY = panY + y;

    if (nextX >= MIN_PAN && nextX <= MAX_PAN) {
      panX = nextX;
    }
    if (nextY >= MIN_PAN && nextY <= MAX_PAN) {
      panY = nextY;
    }
    
    if (main_section) {
      main_section.style.transform = `translate(${panX}px, ${panY}px)`;
    }
    
    if ((x > 0 && panX < MAX_PAN) || (x < 0 && panX > MIN_PAN) ||
        (y > 0 && panY < MAX_PAN) || (y < 0 && panY > MIN_PAN)) {
      animation_frame_id = requestAnimationFrame(pan_screen);
    } else {
      animation_frame_id = null;
    }
  }

  function start(e) {
    e.stopPropagation();
    if (!animation_frame_id) {
      animation_frame_id = requestAnimationFrame(pan_screen);
    }
  }

  function stop() {
    if (animation_frame_id) {
      cancelAnimationFrame(animation_frame_id);
      animation_frame_id = null;
    }
  }

  node.addEventListener('pointerenter', start);
  node.addEventListener('pointerleave', stop);

  return {
    update(newParams) {
      x = newParams.x;
      y = newParams.y;
    },

    destroy() {
      stop();
      node.removeEventListener('pointerenter', start);
      node.removeEventListener('pointerleave', stop);
    }
  };
}


function random_size(node) {
image_function_changer(node).random_size();
}

function random_margin(node) {
image_function_changer(node).random_margin();
}

function random_rotation(node) {
image_function_changer(node).random_rotation();
}

function random_move(node) {
return image_function_changer(node).random_move();
}

function cursor_panning(node) {
return move_background(node);
}

let artwork = [
{ id: "0", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "1", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "2", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "3", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "4", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "5", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "6", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "7", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "8", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "9", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "10", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "11", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "12", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "13", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "14", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "15", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "16", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "17", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "18", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "19", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "20", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "21", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "22", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "23", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "24", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "25", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "26", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "27", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "28", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "29", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "30", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "31", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" },
{ id: "32", image_url: "wallhaven-4yge8x.jpg", description: "some random artwork", tags: "random, art, yep" }
];
</script>

<svelte:window bind:innerWidth={window_width} bind:innerHeight={window_height} />

<div class="four_square_container">
  <div class="four_square red" use:pan_square={{ x: 1, y: 1 }}></div>
  <div class="four_square blue" use:pan_square={{ x: -1, y: 1 }}></div>
  <div class="four_square orange" use:pan_square={{ x: 1, y: -1 }}></div>
  <div class="four_square green" use:pan_square={{ x: -1, y: -1 }}></div>
</div>

<main 
bind:this={main_section} 
class="main_section"
use:cursor_panning
>
<div class="title">
<h1>BABs Art</h1>
</div>
{#each artwork as image, i (image.id)}
<img 
class="artwork"
src={image.image_url} 
alt={image.description}
use:random_size
use:random_move
use:random_margin
use:random_rotation />
{/each}
</main>

<style>
.title {
  position: fixed;
  color: white;
  margin: auto;
  inset: 0;
  background-color: transparent;
  display: flex;
  align-items: center;
  justify-content: center;
}

h1 {
  font-size: 6rem;
  color: #202020;
}

h1:hover {
  color: #404040;
  text-shadow: 0px 0px 40px rgba(190,190,190,0.1);
  transition: all 3s ease-in-out;
}

.main_section {
    width: 300vw;
    height: 300vh;
    top: -100vh;
    left: -100vw;
    background-color: rgba(0,0,0,0.95);
    will-change: transform;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    position: fixed;
}

.four_square_container {
  background-color: transparent;
  position: relative;
  inset: 0;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-areas: 
    "red blue"
    "orange green";
  z-index: 1000000000000;
  pointer-events: none;
}

.four_square {
  position: relative;
  pointer-events: auto;
  cursor: pointer;
}

.red {
  grid-area: red;
  opacity: 0.3;
  background-color: transparent;
}

.blue {
  grid-area: blue;
  opacity: 0.3;
  background-color: transparent;
}

.orange {
  grid-area: orange;
  opacity: 0.3;
  background-color: transparent;
}

.green {
  grid-area: green;
  opacity: 0.3;
  background-color: transparent;
}

.artwork {
  width: 30vw;
  cursor: pointer; 
  transform: 
    translateX(var(--move, 0px)) 
    translateY(var(--move, 0px)) 
    rotateX(var(--rot-deg, 45deg))
    rotate(var(--rotation, 0deg));
  border: 2px solid white;
  box-shadow: 0px 0px 30px #303030;
  transition: all 3s linear;
  z-index: 100000;
}

.artwork:hover {
  --rotation: 0deg;
  --move: 0px;
  --rot-deg: 0deg;
  scale: 1 !important;
  z-index: 10000000000 !important;
}
</style>
