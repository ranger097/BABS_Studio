<script>

function link_maker(node) {
  function get_name(title, src) {
  node.innerHTML = `<a href=${src}>${title}</a>`;
  }
 
  function get_style(color) {
  node.style.color = `${color}`;
  }


  return {
  get_name,
  get_style
  };
}

function action_function(node, params) {
let link = link_maker(node);
link.get_name(params.title, params.src);
if (params.color) {
link.get_style(params.color);
}
  
}

</script>

<section class="top_section">
<button class="menu">☰</button>


</section>




<section class="main_section">

<div class="controls">
<button class="play">▶</button>
<button class="pause">&#9208;</button>
</div>

<nav>
<div
use:action_function={{title: 'Home', src: 'www.google.com', color: 'white'}}
></div>
<div
use:action_function={{title: 'About', src: 'www.google.com', color: 'white'}}
></div>
<div
use:action_function={{title: 'Articles', src: 'www.google.com', color: 'white'}}
></div>
<div
use:action_function={{title: 'Contact', src: 'www.google.com', color: 'white'}}
></div>
</nav>


<button class="settings">&#9881;</button>

</section>
<style>


.top_section {
display: flex;
padding: 0px 2vw;
gap: 2vw;
position: fixed;
z-index: 100000000000000;
width: calc(100vw - 4vw);
height: 10vh;
margin: auto;
inset: 0;
margin-top: 2vw;
align-items: center;
justify-content: space-between;
border-radius: 0px;
background-color: transparent;
}


nav {
display: flex;
background: linear-gradient(rgba(190,190,190,0.1));
border: 1px solid rgba(190,190,190,0.5);
gap: 2vw;
margin-bottom: 3vw;
align-items: center;
justify-content: center;
padding: 2vw 3vw;
height: 0px;
border-radius: 100px;
backdrop-filter: blur(15px);
box-shadow: 0px 0px 30px rgba(190,190,190,0.2);
}

nav :global(a) {
color: inherit;
text-decoration: none;
border-radius: 100px;
font-size: clamp(1.5vw, 1.5vw, 1.7vw);
}

.main_section {
display: flex;
padding: 0px 2vw;
gap: 2vw;
position: fixed;
z-index: 100000000000000;
width: calc(100vw - 4vw);
height: 10vh;
margin: auto;
inset: 0;
margin-bottom: 0vh;
align-items: center;
justify-content: space-between;
border-radius: 0px;
background-color: transparent;
}

.controls {
display: flex;
gap: 1vw;
}

.play, .pause, .settings, .menu {
background-color: red;
padding: 2vw;
margin-bottom: 3vw;
font-size: clamp(2vw, 2vw, 3vw);
border-radius: 500px;
height: 3vw;
width: 3vw;
display: flex;
align-items: center;
justify-content: center;
aspect-ratio: 1/1;
background: linear-gradient(rgba(190,190,190,0.1));
border: 1px solid rgba(190,190,190,0.5);
backdrop-filter: blur(15px);
box-shadow: 0px 0px 30px rgba(190,190,190,0.2);
color: white;
}

.play {
padding: 1.9vw 1.9vw 2.1vw 2.1vw;
}

</style>
