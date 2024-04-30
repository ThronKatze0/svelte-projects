<script lang="ts">
	import { Modal, getModalStore, initializeStores } from '@skeletonlabs/skeleton';
	import type { ModalSettings, ModalComponent, ModalStore } from '@skeletonlabs/skeleton';

	class Todo {
		name: string;
		checked: boolean;
		id: number;

		constructor(name: string) {
			this.name = name;
			this.checked = false;
			this.id = Math.floor(Math.random() * 100);
		}
	}
	initializeStores();

	let inputName: string;
	let todoToEdit: Todo = new Todo('fdfs');
	let modalStore: ModalStore = getModalStore();

	let todos: Array<Todo> = [
		new Todo('Todo1'),
		new Todo('Todo1'),
		new Todo('Todo1'),
		new Todo('Todo1')
	];

	function addTodo() {
		todos = [...todos, new Todo(inputName)];
		inputName = '';
	}
	const editModal: ModalSettings = {
		type: 'prompt',
		title: 'Edit Todo',
		body: 'You can edit your Todo below',
		value: todoToEdit.name,
		valueAttr: { type: 'text', minlength: 3, maxlength: 10, required: true },
		response: (r: string) => {
			todoToEdit.name = r;
			todos = todos;
		}
	};
</script>

<Modal />
<h1 class="h1 text-center mt-8">Todo app</h1>
<div class="flex flex-row justify-center mt-16">
	<input
		class="input w-1/4"
		title="Todo Name"
		type="text"
		placeholder="Todo"
		bind:value={inputName}
	/>
	<button type="submit" class="btn variant-filled ml-3" on:click={addTodo}>Submit</button>
</div>

<div class="grid grid-cols-3 gap-5 mx-20 mt-16">
	{#each todos as todo, i}
		<div class="card card-hover">
			<header class="card-header">
				<div class="flex flex-row justify-between">
					{#if todo.checked}
						<h2 class="h2 line-through">{todo.name}</h2>
						<input class="checkbox p-3.5" type="checkbox" checked bind:value={todo.checked} />
					{:else}
						<h2 class="h2">{todo.name}</h2>
						<input class="checkbox p-3.5" type="checkbox" bind:value={todo.checked} />
					{/if}
				</div>
			</header>
			<section class="p-4">
				<div class="flex flex-row justify-end">
					<button
						type="submit"
						class="btn variant-filled"
						on:click={() => {
							todos.splice(i, 1);
							todos = todos;
						}}>Delete</button
					>
					<button
						type="submit"
						class="btn variant-filled"
						on:click={() => {
							todoToEdit = todo;
							modalStore.trigger(editModal);
						}}>Edit</button
					>
				</div>
			</section>
		</div>
	{/each}
</div>
