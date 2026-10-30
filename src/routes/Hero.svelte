<script>
let main_section;
let window_width;
let window_height;

function image_function_changer(adjusted_image) {
  let scale = 0.4 + Math.random() * 0.1; 
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
    adjusted_image.addEventListener("pointerleave", pause);
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


let artwork = [
{ id: "0",
  image_url: "wallhaven-4yge8x.jpg",
  description: "some random artwork",
  tags: "random, art, yep"
},
{ id: "1",
  image_url: "wallhaven-4yge8x.jpg",
  description: "some random artwork",
  tags: "random, art, yep"
},
{ id: "2",
  image_url: "wallhaven-4yge8x.jpg",
  description: "some random artwork",
  tags: "random, art, yep"
}
];



</script>

<svelte:window bind:innerWidth={window_width} bind:innerHeight={window_height} />


<main bind:this={main_section} class="main_section">
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
font-size: 5rem;
}

.main_section {
background-color: rgba(0,0,0,0.95);
}


.artwork {
position: static;
  width: 40vw;
  cursor: pointer; 
  transform: 
    translateX(var(--move, 0px)) 
    translateY(var(--move, 0px)) 
    rotateX(var(--rot-deg, 45deg))
    rotate(var(--rotation, 0deg));
  border: 2px solid white;
  box-shadow: 0px 0px 30px #303030;
}

.artwork:hover {
  --rotation: 0deg;
  --move: 0px;
  --rot-deg: 0deg;
  scale: 1 !important;
  z-index: 10000000000 !important;
}

</style>
