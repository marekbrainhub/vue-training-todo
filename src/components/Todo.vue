<template>
	<li :class="{ done }" @click="toggleTodo(id)">
		<span>
			<slot />
		</span>
		<span class="close" @click.stop="removeTodo(id)">X</span>
	</li>
</template>

<script>
import store from '../store'

export default {
	props: ['done', 'id'],
	methods: {
    toggleTodo(i) {
      store.todos[i].done = !store.todos[i].done
    },
		removeTodo(i) {
			store.todos.splice(i, 1)
		}
	},
	data() {
		return {
		};
	},
};
</script>

<style lang='stylus' scoped>
li
  display inline-block
  list-style none
  padding 1em
  border 1px black solid
  margin .5em
  border-radius 4px
  user-select none
  cursor pointer
  transition background .1s ease-in-out

.close
  color red
  padding-left 1em

.done
  background-color rgba(green, .3)
</style>
