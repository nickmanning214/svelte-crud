<script>
	import Crud from './Crud.svelte';
	let arr = ['One','Two','Three','Four','Five','Six','Seven','Eight','Nine','Ten','Eleven','Twelve'];
	let changeCount = 0;
	let addCount = 0;
	let lastAdded = null;
	let deleteCount = 0;
	let lastDeleted = null;
	let reorderCount = 0;
	let lastReordered = null;
	let clickedItem = null;
	let clickedIndex = null;


	function onChange(e){
		changeCount++;
		arr = e.detail.arr;
	}

	function onDelete(e){
		lastDeleted=e.detail
		deleteCount++;
	}

	function onAdd(e){
		lastAdded=e.detail
		addCount++;
	}

	function onReorder(e){
		lastReordered=e.detail
		reorderCount++;
	}


	function onClickItem(e){
		clickedItem = e.detail.item;
		clickedIndex = e.detail.index
	}

	function onClickLastAdded(){
		console.log(lastAdded)
	}
	function onClickLastDeleted(){
		console.log(lastDeleted)
	}
	function onClickLastReordered(){
		console.log(lastReordered)
	}
</script>
<events>
	<event>
		changeCount: {changeCount}
	</event>
	<event>
	addCount: {addCount} <button on:click={onClickLastAdded}>Log last added</button>
	</event>
	<event>
	deleteCount: {deleteCount} <button on:click={onClickLastDeleted}>Log last deleted</button>
	</event>
	<event>
	reorderCount: {reorderCount} <button on:click={onClickLastReordered}>Log last reordered</button>
	</event>
</events>
<main>
	<Crud 
		arr={arr} 
		on:change={onChange}
		on:clickItem={onClickItem}
		on:delete={onDelete}
		on:add={onAdd}
		on:reorder={onReorder}
		
		let:item={item}
	
	>
		<select>
			<option>{item}!!!</option>
			<option>B</option>
			<option>C</option>
		</select>
		[Drag]
	</Crud>
</main>
<div>
	[{arr}]
</div>
<div>
	{clickedItem} {clickedIndex}
</div>
<style>
	events{
		border-bottom:1px solid black;
		display:block;
	}
	event{display:block}
	main{
		position:relative;
	}
</style>
