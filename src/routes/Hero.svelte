<script>
let main_section;
let window_width;
let window_height;
let panX = 0;
let panY = 0;
let isPaused;

function image_function_changer(adjusted_image) {
  const scale = 0.4 + Math.random() * 0.5; 
  function random_size() {
  adjusted_image.style.scale = `${scale * 2}`;
  }

  function random_margin() {
  adjusted_image.style.margin = `${2 * scale}px`;
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
    movementY -= 0; 
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
  const maxShift = 1000;
  function cursor_panning(e) {
  if (!window_width || !window_height) return;

  const xPercent = (e.clientX / window_width) - 0.5;
  const yPercent = (e.clientY / window_height) - 0.5;

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


function pan_square(node, { x, y, isPaused }) {
  let animation_frame_id = null;

  const MAX_PAN = 5000; 
  const MIN_PAN = -5000;

  function pan_screen() {
    if (!isPaused) {
    let nextX = panX + x;
    let nextY = panY + y;

    if (nextX >= MIN_PAN && nextX <= MAX_PAN) {
      panX = nextX;
    }
    if (nextY >= MIN_PAN && nextY <= MAX_PAN) {
      panY = nextY;
    }
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
      isPaused = newParams.isPaused;
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
  <div class="four_square red" use:pan_square={{ x: 1, y: 1, isPaused }}></div>
  <div class="four_square blue" use:pan_square={{ x: -1, y: 1, isPaused }}></div>
  <div class="four_square orange" use:pan_square={{ x: 1, y: -1, isPaused }}></div>
  <div class="four_square green" use:pan_square={{ x: -1, y: -1, isPaused }}></div>
</div>

<div class="stopMovement" use:pan_square={{ x: 0, y: 0, isPaused: true }}></div>



<main 
bind:this={main_section} 
class="main_section"
use:cursor_panning
>

<div class="title">
<h1>BABs Art</h1>
</div>

<div class="image_container">
{#each artwork as image, i (image.id)}
<img 
class="artwork"
src={image.image_url} 
alt={image.description}
/>
{/each}
</div>


</main>

<style>

* {
  box-sizing: border-box;
}

.title {
  position: fixed;
  margin: auto;
  inset: 0;
  color: white;
  background-color: transparent;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 80vw;
  height: 80vh;
  z-index: 0;
  pointer-events: none;
}

.stopMovement {
  position: fixed;
  margin: auto;
  inset: 0;
  color: white;
  background-color: red;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 90vw;
  height: 90vh;
  z-index: 10;
  opacity: 0.3;
  border-radius: 50%;
  cursor: pointer;
  display: none;
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
  width: 100vw;
  height: 100vh;
  position: fixed;
  margin: auto;
  inset: 0;
  background-color: rgba(0,0,0,0.95);
  will-change: transform;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  scale: 2;
}

.four_square_container {
  background-color: transparent;
  position: fixed;
  inset: 0;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-areas: 
    "red blue"
    "orange green";
  z-index: 5;
  pointer-events: none;
}

.four_square {
  position: relative;
  pointer-events: auto;
  cursor: pointer;
  display: none;
}

.red { grid-area: red; }
.blue { grid-area: blue; }
.orange { grid-area: orange; }
.green { grid-area: green; }

.image_container {
  background-color: transparent;
  width: 80%;
  height: 80%;
  z-index: 1;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  gap: 1vw;
  overflow: hidden;
}

.artwork {
  max-width: 10vw;
  cursor: pointer;
  border: 1px solid white;
  box-shadow: 0px 0px 30px #303030;
  object-fit: cover;
  margin: 0px;
}

.artwork:hover {
  --rotation: 0deg;
  --move: 0px;
  --rot-deg: 0deg;
  scale: 1.1 !important;
}</style>
