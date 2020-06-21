<script>
	import Crud from './Crud.svelte';
	let arr = ['One','Two','Three','Four','Five','Six','Seven','Eight','Nine','Ten','Eleven','Twelve'];
	let changeCount = 0;
	let clickedItem = null;
	let clickedIndex = null;


	function onChange(e){
		changeCount++;
		arr = e.detail.arr;
	}
	function onClickItem(e){
		clickedItem = e.detail.item;
		clickedIndex = e.detail.index
	}
</script>
<events>
	changeCount: {changeCount}
</events>
<main>
	<Crud 
		arr={arr} 
		on:change={onChange}
		on:clickItem={onClickItem}
	></Crud>
</main>
<div>
	[{arr}]
</div>
<div>
	{clickedItem} {clickedIndex}
</div>
<style>
	events{
		height:30px;
		border-bottom:1px solid black;
		display:block;
	}
	main{
		position:relative;
	}
</style>
