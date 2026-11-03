<script>
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

function accordian(node) {
  const children = Array.from(node.children);
  const total = children.length;
  const radius = 500;

  children.forEach((child, i) => {
    const angle = (i * 2 * Math.PI) / total;
    
    const x = radius * Math.cos(angle);
    const y = radius * Math.sin(angle);
    
    child.style.position = 'absolute';
    child.style.left = '50%';
    child.style.top = '50%';
    child.style.transform = `translate(-50%, -50%) translate(${x}px, ${y}px)`;
  });
}
</script>

<main class="main_section">
  <div class="image_container" use:accordian>
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
  .main_section {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #111;
  }

  .image_container {
    position: relative;
    width: 100vw;
    height: 100vh;
  }

  .artwork {
    width: 20vw;
    height: 20vw;
    border-radius: 100%;
    object-fit: cover;
    border: 2px solid black;
    box-shadow: -4px 4px 10px rgba(0,0,0,0.5);
    margin-top: 60vh;
    cursor: pointer;
  }

  .artwork:hover {
border: 2px solid white;
box-shadow: 0 4px 10px rgba(255,255,255,0.5);

  }
</style>
