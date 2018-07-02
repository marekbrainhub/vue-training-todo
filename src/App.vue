<template>
	<div id="app">
		<img src="./assets/loading.gif" alt='Loading...' v-if='loading' id='loading' />
		<ul v-else>
      <transition-group name='bounce'>
        <Todo 
          v-for="(todo, i) in todos" 
          :done="todo.done"
          :key="i"
          :id="i"
          >{{ todo.content }}</Todo>
      </transition-group>
		</ul>

		<form @submit.prevent="addTodo(input)">
			<input type='text' v-model="input" />
		</form>
	</div>
</template>

<script>
import Todo from '@/components/Todo'
import store from '@/store'

export default {
	components: {
		Todo
	},
	mounted() {
		setTimeout(this.load, 2000)
	},
	methods: {
		addTodo(content) {
			store.todos.push({
				content,
				done: false
			})
			this.input = ''
		},
		load() {
			this.loading = false
		}
	},
	data() {
		return {
			todos: store.todos,
			input: '',
			loading: true,
		}
	}
}
</script>

<style lang='stylus' scoped>
*
  margin 0
  padding 0
  box-sizing border-box

#app
  font-family 'Avenir'
  font-size 3rem
  text-align center

input
  padding 1em
  font-size 3rem
  font-family 'Avenir'
  margin .5em

.bounce-enter-active, .bounce-leave-active
  transition all .3s

.bounce-enter, .bounce-leave-to
  opacity 0
  transform translateY(30px)

.bounce-move
  transition all .3s
</style>
