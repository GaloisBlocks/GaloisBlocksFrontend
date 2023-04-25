<script>
  import "iconify-icon";
  function dragMe(node) {
    let moving = false;
    let left = 50;
    let top = 10;

    let selector = document.getElementById("menu-drag-sel");

    node.style.position = "absolute";
    node.style.top = `${top}px`;
    node.style.left = `${left}px`;
    node.style.cursor = "move";
    node.style.userSelect = "none";

    selector.addEventListener("mousedown", (e) => {
      moving = true;
    });

    window.addEventListener("mousemove", (e) => {
      if (moving) {
        left += e.movementX;
        top += e.movementY;
        if (left < 0) left = 0;
        if (top < 0) top = 0;
        node.style.top = `${top}px`;
        node.style.left = `${left}px`;
      }
    });

    window.addEventListener("mouseup", () => {
      moving = false;
    });
  }
  function drop(event,index){
    console.log(event)
  }
  let list = [1,2,3,4,5]
</script>

<div class="menu-window" use:dragMe>
  <div id="menu-drag-sel">Object Selection</div>
  <div class="menu-objs-box">
    <div class="menu-objs">
      {#each list as index}
        <iconify-icon
          draggable="true"
          on:drop|preventDefault={(event) => drop(event, index)}
          on:dragover|preventDefault
          class="icon"
          icon="mdi:home"
        />
      {/each}
    </div>
  </div>
</div>

<style>
  @import url('https://fonts.cdnfonts.com/css/google-sans');
  .icon {
    font-size: 40px;
    height: 40px;
    outline: 1px solid black;
    border-radius: 3px;
    margin-top: 1px;
    margin-left: 1px;
    transition: 0.2s;
    cursor: pointer;
  }
  .icon:hover{
    background: rgba(0, 255, 255, 0.286);
  }
  .menu-window {
    box-shadow: 0px 0px 3px 3px rgba(0, 23, 14, 0.314);
    background-color: rgba(85, 164, 255, 0.629);
    border-radius: 5px;
    font-size: 11pt;
    font-family: 'Product Sans Medium';
    color: #000;
    width: clamp(150px, 10vw, 10vw);
    height: 90%;
  }
  .menu-objs-box {

    cursor: default;
    width: 85%;
    height: 95%;
    background-color: rgba(0, 24, 110, 0.616);
    border: solid 1px rgb(0, 0, 0);
    margin: auto;
    border-top: none;
  }
  .menu-objs {
    display: inline-flex;
    flex-wrap: wrap;
    padding: 2px;
    justify-content: left;
  }
  #menu-drag-sel {
    background-color: rgba(123, 123, 123, 0.197);
    border: solid 1px rgb(0, 0, 0);
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }
</style>
