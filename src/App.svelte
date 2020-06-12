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
<Crud arr={arr} on:change={onChange}></Crud>

<div>
	[{arr}]
</div>
