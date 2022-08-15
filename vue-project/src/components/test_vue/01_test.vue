<script>
let id = 0;
export default {
  // 组件选项
  data() {
    return {
      titleClass: "title",
      message: "Make me dynamic!",
      text: "",
      areyouOK: true,
      time: true,
      counter: {
        count: 10
      },
      todos: [
        { id: id++, text: "Learn HTML", done: true },
        { id: id++, text: "Learn JavaScript", done: true },
        { id: id++, text: "Learn Vue", done: false }
      ],
      addtodotext: "",
      hideCompleted: false
    };
  },
  // computed: {
  //   filteredTodos() {
  //     return this.hideCompleted ? this.todos.filter(t => !t.done) : this.todos;
  //   }
  // },
  computed: {
    filteredTodos() {
      return this.hideCompleted ? this.todos.filter(t => !t.done) : this.todos;
    }
  },
  // 此处声明一些响应式状态
  methods: {
    increment() {
      this.counter.count++;
    },
    onInput(e) {
      this.text = e.target.value;
    },
    onchange() {
      this.areyouOK = !this.areyouOK;
    },
    changetime() {
      this.time = !this.time;
    },
    removeTodo(e) {
      this.todos = this.todos.filter(item => item.id !== e.id);
    },
    addtodo() {
      this.todos.push({ id: id++, text: this.addtodotext, done: false });
      this.addtodotext = "";
    }
    // onhideCompleted() {
    //   this.hideCompleted = !this.hideCompleted;
    // }
  }
};
</script>

<template>
  <h1 :class="titleClass">{{ message }}</h1>
  <p>{{ counter.count }}</p>
  <button @click="counter.count++">count: {{ counter.count }}</button>
  <br />
  <!-- <input :value="text" @input="onInput" placeholder="请输入文字" /> -->
  <input v-model="text" placeholder="请输入文字" />
  <p :class="titleClass">{{ text }}</p>
  <h1 v-if="areyouOK">你好啊？</h1>
  <h1 v-else>我不好啊！</h1>
  <h2 v-if="time">这个时代似的</h2>
  <h2 v-else>啥时候的事</h2>
  <button @click="onchange">切换</button>&nbsp;&nbsp;
  <button @click="changetime">切换time</button>
  <br />
  <form @submit.prevent="addtodo">
    <input v-model="addtodotext" placeholder="请输入" />&nbsp;
    <button>add</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <!-- <button @click="onhideCompleted">hideCompleted</button> -->
  <button @click="hideCompleted = !hideCompleted">
    {{ this.hideCompleted ? "hideCompleted" : "show all" }}
  </button>
</template>

<style>
.title {
  color: red;
}
.done {
  text-decoration: line-through;
}
</style>
