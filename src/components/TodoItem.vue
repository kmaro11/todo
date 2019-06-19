<template>
    <div class="todo__list-item">
        <input type="checkbox" v-model="todoItem.active">
        <p class="todo__item-title" :class="selectedColor">{{todoItem.title}}</p>
        <i class="material-icons" v-if="todoItem.star">
            star_rate
        </i>
        <div class="todo__options-block">
            <i class="material-icons todo__options" v-click-outside="closeMenu" @click="openMenu">more_vert</i>
            <div v-if="menu" class="todo__options-wrap">
                <div class="todo__color_wrap">
                    <div v-for="color in colorOption"
                         class="todo__color-circle"
                         :class="color.color" @click="changeColor(color.color)"></div>
                </div>
                <div class="todo__option-btn-wrap">
                    <div v-for="option in actionOption"
                         class="todo__option-btn"
                         :class="option.action"
                         @click="changeAction(option.action, todoItem)">
                        {{option.action}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
  import ClickOutside from 'vue-click-outside'

  export default {
    directives: {
      ClickOutside
    },
    props: {
      todoItem: Object
    },
    data () {
      return {
        menu: false,
        selectedColor: 'black',
        colorOption: [
          {
            color: 'green'
          },
          {
            color: 'red'
          },
          {
            color: 'blue'
          },
          {
            color: 'black'
          }

        ],
        actionOption: [
          {
            name: 'Star',
            action: 'star'
          },
          {
            name: 'Remove',
            action: 'remove'
          }
        ],
      }
    },
    methods: {
      closeMenu () {
        this.menu = false
      },
      openMenu () {
        this.menu = !this.menu
      },
      changeColor (color) {
        this.selectedColor = color
      },
      changeAction (option, item) {
        this.$emit('addStatus', {option, item})
        this.closeMenu()
      }
    }

  }
</script>
<style lang="scss">
    .todo {
        &__item-title {
            &.green {
                color: #8adad6;
            }

            &.blue {
                color: #6e81be;
            }

            &.red {
                color: #f25f66;
            }

            &.black {
                color: black;
            }
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