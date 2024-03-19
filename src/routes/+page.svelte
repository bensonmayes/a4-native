<script>
	import '../style.css'
	let todoItem= '';
	let todoList = [];

	function addToArray() {
		if (todoItem =='') {
			return;
		}
		todoList.push(todoItem);
		todoList = todoList;
		console.log(todoList);
		todoItem = '';
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<h1>todoapp!</h1>

<form on:submit|preventDefault={addToArray}>
	<input type="text" bind:value={todoItem}>
	<button type="submit">Add</button>
</form>

<ul>

</ul>