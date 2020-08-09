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
	let editedIndex = null;
	let editCount = 0;

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

	function onEdit(e){
		lastEdited = e.detail;
		editCount++;
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

	function selectOnChange(item,index,e){
		console.log('fired',item,index,e)
		arr[index] = e.target.value;
		arr = arr;
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
	<event>
	editCount: {editCount} <button on:click={onClickLastEdited}>Log last edited</button>
	</event>
</events>
<main>
	TODO: scrolling messes this up
	<Crud 
		arr={arr} 
		on:change={onChange}
		on:delete={onDelete}
		on:add={onAdd}
		on:reorder={onReorder}
		on:edit={onEdit}
		
		let:item={item}
		let:index={index}
	
>
	<!--this is messed up logic. You can't explicitly say {item} as an option and then also bind the value-->
		<select value={item} on:change={selectOnChange.bind(null,item,index)}>
			<option>{item}</option>
			<option>{item}!</option>
			<option>{item}?</option>
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
