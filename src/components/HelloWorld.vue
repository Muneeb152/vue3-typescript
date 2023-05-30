<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>{{ pow(2, 3) }}</div>
    <button @click="increment">{{ count }}</button>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, onErrorCaptured, onMounted, reactive, ref, watch } from 'vue';

interface State {
  title: string,
  year: number,
  todos: Todo[]
}

interface Todo {
  name: string,
  isComplete: boolean
}

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  setup(props) {
    const count = ref(0)
    const todoId = ref(4)
    console.log(props);
    const state = reactive<State>({
      title: "",
      year: 2020,
      todos: [
        {
          name: 'Finish ScreenCast',
          isComplete: false
        },
        {
          name: 'Go to Store',
          isComplete: false
        }
      ]
    })

    function increment(): void {
      count.value++;
      count.value = pow(2, 3);
    }

    function pow(x: number, y: number): number {
      return Math.pow(x, y);
    }
    const itemsLeft = computed(() => state.todos.filter(todo => !todo.isComplete).length);

    onMounted(() => {
      console.log("Todo Mounted");
    })

    watch(() => count.value,
      (newValue, oldValue) => {
        console.log('New Value:' + newValue);
        console.log('Old Value:' + oldValue)
      }
    )

    onErrorCaptured(e => {
      console.log("Error is:" + e)
    })



    return {
      count,
      increment,
      pow,
      state,
      itemsLeft,
      todoId
    }

  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
