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
<style>

nav {
display: flex;
padding: 0px;
background: linear-gradient(rgba(190,190,190,0.1));
border-top: 1px solid rgba(190,190,190,0.5);
border-left: 1px solid rgba(190,190,190,0.5);
border-right: 1px solid rgba(190,190,190,0.5);
gap: 2vw;
position: fixed;
z-index: 100000000000000;
width: 30vw;
margin: auto;
inset: 0;
margin-bottom: -1vh;
align-items: center;
justify-content: center;
padding: 4vh;
height: 0px;
border-radius: 50px 50px 10px 10px;
backdrop-filter: blur(15px);
box-shadow: 0px 0px 30px rgba(190,190,190,0.2);
}

nav :global(a) {
color: inherit;
text-decoration: none;
border-radius: 100px;
}

</style>
