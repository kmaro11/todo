<template>
    <div id="app">
        <section class="todo">
            <div class="todo__wrap">
                <h1 class="todo__title">TO DO List</h1>
                <input type="text" class="todo__input" v-model="newTodo" @keyup.enter="addTodo">
                <div v-if="todoList.length >= 1"
                     class="todo__action-wrap">
                    <p class="todo__display">left to do:{{ listCount }}</p>
                    <button class="todo__button"
                            :key="item.name"
                            @click="filterTodo(item.action)"
                            v-for="item in actionButtons">
                        {{item.name}}
                    </button>
                    <p class="todo__display">Completed: {{completedTodos}}</p>
                </div>
                <div class="todo__list-wrap">
                    <TodoItem :todoItem="item" v-for="item in showList" :key="item.title" @addStatus="changeAction"/>
                </div>
            </div>

        </section>
    </div>
</template>

<script>
  import TodoItem from '@/components/TodoItem'

  export default {
    name: 'home',
    components: {TodoItem},
    data () {
      return {
        todoList: [],
        newTodo: '',
        actionValue: 'all',

        actionButtons: [
          {
            name: 'All',
            action: 'all'
          },
          {
            name: 'Active',
            action: 'active'
          },
          {
            name: 'Delete all',
            action: 'delete'
          },

        ],

      }
    },
    computed: {
      listCount () {
        return this.todoList.filter(item => !item.active).length
      },
      completedTodos () {
        return this.todoList.filter(item => item.active).length
      },
      showList () {
        if (this.actionValue === 'all') {
          return this.todoList
        } else if (this.actionValue === 'active') {
          return this.todoList.filter(item => item.active)
        } else {
          return this.todoList
        }
      }
    },
    methods: {

      addTodo () {

        if (this.newTodo) {
          this.todoList.push({
            title: this.newTodo,
            active: false,
            star: false
          });
          this.newTodo = '';
        }
      },
      changeAction ({option, item}) {
        console.log(option, item)
        if (option === 'remove' && !item.star) {
          this.showList.filter(todo => {
            if (todo.title === item.title) {
              this.showList.splice(todo, 1)
            }
          })
        } else if (option === 'star') {
          item.star = !item.star
        }
      },
      filterTodo (item) {
        if (item === 'delete') {
          this.todoList = []
        } else {
          this.actionValue = item
        }
      },

    },

  }

</script>
<style lang="scss">
    body {
        margin: 0;
    }

    .todo {
        background: #f5f5f5;
        height: calc(100vh);
        padding-top: 90px;

        &__wrap {
            background: white;
            box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
            max-width: 700px;
            width: 100%;
            margin: 0 auto;
            box-sizing: border-box;
            padding: 25px;
        }

        &__title {
            margin: 0 auto 25px;
            text-align: center;
            color: rgba(175, 47, 47, 0.15);
            font-size: 48px;
        }

        &__input {
            box-sizing: border-box;
            padding: 10px;
            width: 100%;
            font-size: 16px;
            margin-bottom: 15px;
        }

        &__display {
            margin: 0 10px;
        }

        &__action-wrap {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 5px;
        }

        &__button {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100px;
            font-size: 14px;
            background: white;
            height: 25px;
            margin: 10px;
        }

        &__list-wrap {
            width: 100%;
        }





    }


</style>


