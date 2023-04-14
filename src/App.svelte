<script>
	
	function dragMe(node) {
		 let moving = false;
		 let left = 300;
		 let top = 100;

		 node.style.position = 'absolute';
		 node.style.top = `${top}px`;
		 node.style.left = `${left}px`;
		 node.style.cursor = 'move';
		 node.style.userSelect = 'none';

		 node.addEventListener('mousedown', () => {
			 moving = true;
		 });
		 
		window.addEventListener('mousemove', (e) => {
			  if (moving) {
					 left += e.movementX;
					 top += e.movementY;
					 node.style.top = `${top}px`;
					 node.style.left = `${left}px`;
				}
		 });
		
		 window.addEventListener('mouseup', () => {
			 moving = false;
		 });
	
	}
</script>

<style>
	.nft-col {
		border: solid 1px rgb(34, 0, 255);
    background-color:blue;
    border-radius: 20px;
    font-size: 20pt;
    width: 200px;
    height: 150px;
	}
  .img-col {
		border: solid 1px rgba(34, 0, 255, 0.242);
    background-color:rgba(255, 0, 0, 0.401);
    border-radius: 20px;
    font-size: 20pt;
    width: 120px;
    height: 50px;
	}
</style>

	<div class="nft-col" use:dragMe >
		NFT Collection
  </div>
	<div class="img-col" use:dragMe >
		ImageList
  </div>

