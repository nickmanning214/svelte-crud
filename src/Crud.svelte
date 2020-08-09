<script>

	function arraysEqual(a, b) {
  if (a === b) return true;
  if (a == null || b == null) return false;
  if (a.length != b.length) return false;

  // If you don't care about the order of the elements inside
  // the array, you should sort both arrays here.
  // Please note that calling sort on an array will modify that array.
  // you might want to clone your array first.

  for (var i = 0; i < a.length; ++i) {
    if (a[i] !== b[i]) return false;
  }
  return true;
}


	import {createEventDispatcher} from 'svelte';
	const dispatch = createEventDispatcher();
	
	import DraggableList from '@nickmanning214/svelte-draggable-list/src/DraggableList.svelte';

	import SpanEditable from '@nickmanning214/svelte-span-editable/src/SpanEditable.svelte';

	import enableContentEditable from '@nickmanning214/svelte-action-enable-content-editable/src/enableContentEditable.js'

	import arrayMove from 'array-move';
	import pullAt from 'lodash.pullat';

    let onEditInfo;
	export let arr;
	export let defaultItem = function(){
		return 'New';
	}
	
	function onEdit(item,index,e){
		arr[index] = e.detail.value
		arr = arr;
		dispatch('edit',{item:arr[index],index});
		dispatch('change',{arr})
	}
	


	
	function del(index){
		const deleted = pullAt(arr,index)[0];
		arr=arr;
		dispatch('delete',{deleted,index});
		dispatch('change',{arr})
	}

	function onClickDelete(index){
		if (!isDragging) del(index);
	}
	
	function add(){
		const newItem = defaultItem();
		arr = [...arr,newItem];
		dispatch('add',{item:newItem,index:arr.length-1});
		dispatch('change',{arr})
	}

	let isDragging = false;

	function onStartDrag(){
		isDragging = true;
	}

	function onFinishDrag(e){
		isDragging = false;
		if (!arraysEqual(arr,e.detail.data)){
			arr = e.detail.data;
			dispatch('reorder',{arr,startIndex:e.detail.startIndex,finishIndex:e.detail.finishIndex,});
			dispatch('change',{arr})

		}
	}
	
	

	function onLongPress(){
		console.log('lp')
	}

</script>

<DraggableList data={arr} let:item let:index on:startDrag={onStartDrag} on:finishDrag={onFinishDrag}>
	<slot item={item} index={index}>

		<!--default input-->
		<span use:enableContentEditable on:disable={onEdit.bind(null,item,index)}>{item}</span> 
			
	</slot>
	<span on:mouseup={onClickDelete.bind(null,index)}>[Del]</span>
</DraggableList>
<button on:click={add}>
	Add
</button>







<style>

</style>
