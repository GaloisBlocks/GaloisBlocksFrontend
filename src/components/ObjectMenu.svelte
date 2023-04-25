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
  .icon {
    font-size: 40px;
    height: 40px;
    background: transparent;
  }
  .menu-window {
    border: dashed 1px rgb(0, 0, 0);
    background-color: rgb(192, 192, 192);
    border-radius: 5px;
    font-size: 10pt;
    font-family: Verdana;
    color: #000;
    width: clamp(150px, 10vw, 10vw);
    height: 90%;
  }
  .menu-objs-box {
    width: 85%;
    height: 95%;
    background-color: rgb(255, 255, 255);
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
    background-color: rgb(123, 123, 123);
    border: solid 1px rgb(0, 0, 0);
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }
</style>
