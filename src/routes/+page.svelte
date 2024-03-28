<script>
	import '../style.css'
	import { writable } from 'svelte/store';
	import snd from '$lib/images/click.mp3';
	let todoItem= '';
	let storedList;
	let todoList = writable([]);

	if (typeof window !== 'undefined' && typeof localStorage !== 'undefined') {
		storedList = localStorage.getItem('storedList');
		if(storedList) {
			$todoList = (JSON.parse(storedList));
		}
	}
	
	function updateList() {
		return storedList = localStorage.setItem('storedList', JSON.stringify($todoList));
	}
	
	$: isDone = $todoList.filter(item => item.done);
	function addToArray() {
		if (todoItem =='') {
			return;
		}
		$todoList = [...$todoList, {
			text: todoItem,
			done: false
		}];
		//console.log(todoList);
		updateList();
		todoItem = '';
	}
	function removeThis(index) {
		$todoList.splice(index,1);
		$todoList = $todoList;
		updateList();
	}
	function clearDone (){

	}
	function clicksound () {
		var audio = new Audio (snd)
		audio.play();
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<header class="header">
<h1>Welcome to Benson's to do app!</h1>
</header>

<form on:submit|preventDefault={addToArray}>
	<input type="text" bind:value={todoItem}>
	<button type="submit" on:click={clicksound}>Add</button>
</form>

<div>
<ul>
	{#each $todoList as item, index}
	<li>
		<input type="checkbox" bind:checked={item.done} on:change={updateList}>
		<span class:done={item.done} >{item.text}</span>
		<span on:click={() => removeThis(index)}
		class="remove" roll="button" tabindex="0">&times;</span>
	</li>
	{/each}
</ul>
</div>



<style>
	ul {
		list-style: none;
	}
	li {
		font-size: 1.3rem;
	}
	.done {
		color: #ccc;
		text-decoration: line-through;
	}
	.remove {
		color: darkred;
		cursor: pointer;
	}
	div {
		width: 20%;
		margin: 0 auto;
	}
</style>