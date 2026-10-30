<script>
let main_section;

function image_function_changer(adjusted_image) {
  let scale = 0.4 + Math.random() * 0.1; 
  function random_size() {
  adjusted_image.style.scale = `${scale * 2}`;
  }

  function random_margin() {
  adjusted_image.style.margin = `${10 * scale}px`;
  }

  function random_rotation() {
  adjusted_image.style.setProperty(
  "--rotation", `${scale * -1}deg`
  );
  }
  
  let frame_id;
    function random_move() {
    let paused = false;
    function animate(time) {
    if (!paused) {
    const y = 100 * Math.sin(time / 1000);
    adjusted_image.style.setProperty("--y", `${y}px`);
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

<main bind:this={main_section} class="main_section">
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
.artwork {
  width: 20vw;
  cursor: pointer;
  transform: translateY(var(--y, 0px)) rotate(var(--rotation, 0deg));
}

.artwork:hover {
  --rotation: 0deg;
  --y: 0px;
  scale: 1;
}


</style>
