<template>
    <div id="app">
        <section class="todo">
            <div class="todo__wrap">
                <h1 class="todo__title">TO DO List</h1>
                <input type="text" class="todo__input" v-model="newTodo" v-on:keyup.enter="addTodo">
                <div v-if="todoList.length >= 1"
                     class="todo__action-wrap">
                    <p>left to do:{{ listCount }}</p>
                    <button class="todo__button"
                            :key="item.name"
                            @click="filterTodo(item.action)"
                            v-for="item in actionButtons">
                        {{item.name}}
                    </button>
                </div>
                <div class="todo__list-wrap">
                    <TodoItem :todoItem="item" v-for="item in showList" :key="item.title"/>

                </div>
            </div>

        </section>
    </div>
</template>

<script>
  // @ is an alias to /src

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
        return this.todoList.length
      },
      showList () {
        if (this.actionValue === 'all') {
          return this.todoList
        } else if (this.actionValue === 'active') {
          console.log('active')
          return this.todoList.filter(item => item.active)
        } else if (this.actionValue === 'delete') {
          return this.todoList = []
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
      deleteList (index) {
        this.todoList.splice(this.todoList.indexOf(index), 1)
      },
      filterTodo (item) {
        this.actionValue = item
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

        &__list-item {
            display: flex;
            align-items: center;
            padding: 15px;
            border: 1px solid #f5f5f5;
            margin: 5px;
        }

        &__delete {
            margin-left: auto;
        }

        &__options-block {
            position: relative;
            margin-left: auto;
        }

        &__options-wrap {
            position: absolute;
            width: 80px;
            padding: 10px;
            top: -30px;
            right: 30px;
            box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
            z-index: 10;
            background: white;
        }

        &__options {
            cursor: pointer;
        }

        &__option-btn-wrap {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        &__option-btn {
            margin: 5px;
            cursor: pointer;

            &.remove {
                color: #f25f66;
            }

            &.star {
                color: #ffd662;
            }
        }


        &__color_wrap {
            display: flex;
            align-items: center;
            justify-content: space-around;
            margin-bottom: 5px;
        }

        &__color-circle {
            width: 12px;
            height: 12px;
            display: block;
            border-radius: 50px;
            cursor: pointer;

            &.green {
                background-color: #8adad6;
            }

            &.blue {
                background-color: #6e81be;
            }

            &.red {
                background-color: #f25f66;
            }

            &.black {
                background-color: black;
            }


        }

    }


</style>


