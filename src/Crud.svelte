<script>
	import DraggableList from '@nickmanning214/svelte-draggable-list/src/Index.svelte';//have to debug this
	
	import SpanEditable from '@nickmanning214/svelte-span-editable/src/SpanEditable.svelte';
	import arrayMove from 'array-move';
	import pullAt from 'lodash.pullat';

    let onEditInfo;
    export let arr;
	function onEdit(item,index,e){
		arr[index] = e.detail.value
		arr = arr;
	}
	
	let currentDraggedIndex = null
	let from;
	let to;
	function onMouseDown(e){
		currentDraggedIndex = e.detail.i;
	}
	function onChange(e){

		arr = e.detail.newData;
	}
	
	function del(index){
		console.log('del')
		pullAt(arr,index);
		arr=arr;
	}
	
	function add(){
		arr = [...arr,'New'];
	}
	
</script>

<DraggableList data={arr} let:item let:index on:mousedown={onMouseDown} on:change={onChange}>
	<SpanEditable on:edited={onEdit.bind(null,item,index)}>{item}</SpanEditable>
	<span on:click={del.bind(null,index)}>[Del]</span>
</DraggableList>
<button on:click={add}>
	Add
</button>
<div>
[{arr}]
currentChangeIndex: {from} {to}
</div>
