<script>
	import Crud from './Crud.svelte';
	let arr = ['One','Two','Three','Four','Five','Six','Seven','Eight','Nine','Ten','Eleven','Twelve'];
	function onChange(e){
		console.log('on change')
		arr = e.detail.arr;
	}
</script>

<Crud arr={arr} on:change={onChange}></Crud>

<div>
	[{arr}]
</div>
