<script>
	import DraggableList from '@nickmanning214/svelte-draggable-list/src/DraggableList.svelte';
	
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
		console.log("works")
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

	let isDragging = false;

	function onStartDrag(){
		isDragging = true;
	}

	function onFinishDrag(e){
		isDragging = false;
		arr = e.detail.data;
	}
	
</script>

<height>
<DraggableList data={arr} let:item let:index on:mousedown={onMouseDown} on:change={onChange} on:startDrag={onStartDrag} on:finishDrag={onFinishDrag}>
	<SpanEditable on:edited={onEdit.bind(null,item,index)} disabled={isDragging}>{item}</SpanEditable>
	<span on:click={()=>{del(index)}}>[Del]</span>
</DraggableList>
</height>
<button on:click={add}>
	Add
</button>
<div>
[{arr}]
currentChangeIndex: {from} {to}
</div>
<style>
height{
	display:block;
	height:500px;
}
</style>
