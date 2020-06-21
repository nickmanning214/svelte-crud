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

	function onClickDelete(index){
		if (!isDragging) del(index);
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
		if (!arraysEqual(arr,e.detail.data)){
			arr = e.detail.data;
			dispatch('change',{arr})
		}
	}
	
	function onMouseupSpanEditable(item,index,e){
		dispatch('clickItem',{
			item,index
		})
	}

	function onLongPress(){
		console.log('lp')
	}

</script>

<DraggableList data={arr} let:item let:index on:startDrag={onStartDrag} on:finishDrag={onFinishDrag}>
	<SpanEditable 
		on:click={onMouseupSpanEditable.bind(null,item,index)}
		on:edited={onEdit.bind(null,item,index)} disabled={isDragging}>{item}</SpanEditable>
	<span on:mouseup={onClickDelete.bind(null,index)}>[Del]</span>
</DraggableList>
<button on:click={add}>
	Add
</button>







<style>

</style>
