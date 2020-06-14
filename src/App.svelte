<script>
	import Crud from './Crud.svelte';
	let arr = ['One','Two','Three','Four','Five','Six','Seven','Eight','Nine','Ten','Eleven','Twelve'];
	let changeCount = 0;
	function onChange(e){
		changeCount++;
		arr = e.detail.arr;
	}
</script>
<events>
	changeCount: {changeCount}
</events>
<main>
	<Crud arr={arr} on:change={onChange}></Crud>
</main>
<div>
	[{arr}]
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
