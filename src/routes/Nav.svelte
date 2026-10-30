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
<nav>
<div
use:action_function={{title: 'Home', src: 'www.google.com', color: 'blue'}}
></div>
<div
use:action_function={{title: 'About', src: 'www.google.com', color: 'yellow'}}
></div>
<div
use:action_function={{title: 'Articles', src: 'www.google.com', color: 'green'}}
></div>
<div
use:action_function={{title: 'Contact', src: 'www.google.com', color: 'purple'}}
></div>

</nav>
<style>

nav {
display: flex;
padding: 0px;
background: linear-gradient( transparent );
gap: 30px;
position: fixed;
z-index: 100000000000000;
width: 100vw;
margin: auto;
inset: 0;
margin-bottom: 0px;
align-items: flex-end;
justify-content: center;
padding-bottom: 5vh;
}

nav :global(a) {
color: inherit;
text-decoration: none;
padding: 10px 20px;
background-color: rgba(150, 150, 150, 0.5);
border-radius: 100px;
backdrop-filter: blur(20px);
}

</style>
