<template>
  <view class="container">
      <statusbar />
      <header title="todo app" />
      <view class="inputContainer">
          <text-input class="input" v-model="newTodoText" />
          <touchable-opacity class="add-btn" :on-press="newTodo">
              <text class="btn-text">ADD</text>
          </touchable-opacity>
      </view>
      <view class="todo" v-for="todo in todosArray" v-bind:key="todo.id">
          <touchable-opacity :on-press="() => toggleDone(todo.id)">
              <text class="todo-text done" v-if="todo.completedStatus === true">{{ todo.title }}</text>
              <text class="todo-text" v-else>{{ todo.title }}</text>
          </touchable-opacity>
          <touchable-opacity class="remove-btn" :on-press="() => removeTodo(todo.id)">
              <text class="remove-btn-text">Remove</text>
          </touchable-opacity>
      </view>
    
  </view>
</template>

<script>
import StatusBar from './components/StatusBar';
import Header from './components/Header';
export default {
    components: {
        'statusbar': StatusBar,
        'header': Header
    },
    data () {
        return {
            newTodoText: '',
            todosArray: [
                {
                    id: 0,
                    title: 'Do Laundry',
                    completedStatus: false
                },
                {
                    id: 1,
                    title: 'Clean Dishes',
                    completedStatus: false
                }
            ],
        }
    },
    methods: {
        newTodo () {
            this.todosArray.push({
                id: this.todosArray.length + 1,
                title: this.newTodoText,
                done: false
            })

            this.newTodoText = ''
        },
        toggleDone (id) {
            this.todosArray = this.todosArray.map(todo => {
                if (todo.id === id) todo.completedStatus = !todo.completedStatus;
                return todo;
            })
        },
        removeTodo (id) {
            this.todosArray = this.todosArray.filter(todo => todo.id !== id)
        }
    }
}
</script>
<style>
.container {
  flex: 1;
  background-color: white;
}
.statusbar {
    background-color: #bda164;
    height: 20px;
}
.inputContainer {
    width: 100%;
    flex-direction: row;
    justify-content: center;
    align-items: stretch;
}
.input {
    flex: 1;
    height: 35px;
    background-color: #f3f3f3;
    font-size: 18px;
    color: #888888
}
.add-btn {
    width: 100px;
    height: 35px;
    background-color: #bda164;
    justify-content: center;
    align-items: center;
}
.btn-text {
    font-size: 18px;
    font-weight: 700;
}
.todo {
    flex-direction: row;
    justify-content: space-between;
    padding: 15px;
}
.todo-text {
    font-size: 18px;
}
.done {
    color: #aaaaaa;
}
.remove-btn-text {
    font-size: 18px;
    color: red;
}
</style>
