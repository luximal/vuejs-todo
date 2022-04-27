<template>
	<div class="wrapper" v-cloak>
		<header>{{ title }}
			<a class="octocat" href="https://github.com/luximal/vuejs-todo">
				<svg viewBox="0 0 24 24" height="40px" stroke="currentColor" stroke-width="2" fill="none">
					<path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path>
				</svg>
			</a>
		</header>
		<div class="input-field">
			<input type="text" v-bind:placeholder="placeholderTitle" v-model="inputValue" v-on:keypress.enter="addNewNote"/>
			<button v-on:click="addNewNote">+</button>
		</div>

		<ul class="todoList" v-if="todoList.length !== 0">
			<li v-for="(todo, i) in todoList" v-bind:key="todo.id">
				{{ i + 1 }}.&emsp;{{ todo }}
				<span class="icon" v-on:click="deleteNote(i)">╳</span>
			</li>
		</ul>

		<div class="footer">
			<span>Всего заметок: {{ todoList.length }}</span>
			<button v-on:click="deleteAllNote">Удалить всё</button>
		</div>
	</div>
</template>


<script>
export default {
	data() {
		return {
			title: 'Список дел',
			placeholderTitle: 'Введите новую заметку',
			inputValue: '',
			todoList: [],
		}
	},
	mounted() {
		this.todoList = JSON.parse(localStorage.getItem("todoListData")) || []
	},
	methods: {
		addNewNote() {
			if (this.inputValue != '') {
				this.todoList = JSON.parse(localStorage.getItem("todoListData")) || []
				this.todoList.push(this.inputValue.toUpperCase());
				localStorage.setItem('todoListData', JSON.stringify(this.todoList));
			}
			this.inputValue = '';
		},
		deleteNote(i) {
			this.todoList = JSON.parse(localStorage.getItem("todoListData")) || []
			this.todoList.splice(i, 1);
			localStorage.setItem('todoListData', JSON.stringify(this.todoList));
		},
		deleteAllNote() {
			this.todoList = [];
			localStorage.removeItem('todoListData');
		}
	}
};
</script>


<style>
[v-cloak] {
	display: none;
}
</style>
