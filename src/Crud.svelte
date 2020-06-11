<script>

	import {createEventDispatcher} from 'svelte';
	const dispatch = createEventDispatcher();
	
	import DraggableList from '@nickmanning214/svelte-draggable-list/src/DraggableList.svelte';
	
	import SpanEditable from '@nickmanning214/svelte-span-editable/src/SpanEditable.svelte';
	import arrayMove from 'array-move';
	import pullAt from 'lodash.pullat';

    let onEditInfo;
	export let arr;
	
	
	function onEdit(item,index,e){
		arr[index] = e.detail.value
		arr = arr;
		dispatch('change',{arr})
	}
	


	
	function del(index){
		pullAt(arr,index);
		arr=arr;
		dispatch('change',{arr})
	}
	
	function add(){
		arr = [...arr,'New'];
		dispatch('change',{arr})
	}

	let isDragging = false;

	function onStartDrag(){
		isDragging = true;
	}

	function onFinishDrag(e){
		isDragging = false;
		arr = e.detail.data;
		dispatch('change',{arr})
	}
	
</script>

<height>
	<DraggableList data={arr} let:item let:index on:startDrag={onStartDrag} on:finishDrag={onFinishDrag}>
		<SpanEditable on:edited={onEdit.bind(null,item,index)} disabled={isDragging}>{item}</SpanEditable>
		<span on:click={()=>{del(index)}}>[Del]</span>
	</DraggableList>
</height>
<button on:click={add}>
	Add
</button>







<style>

</style>
