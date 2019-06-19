<template>
    <div class="todo__list-item">
        <input type="checkbox" v-model="item.active">
        <p>{{item.title}}</p>
        <div class="todo__options-block">
            <i class="material-icons todo__options" @click="openMenu">more_vert</i>
            <div v-if="menu" class="todo__options-wrap">
                <div class="todo__color_wrap">
                    <div v-for="color in colorOption"
                         class="todo__color-circle"
                         :class="color.color"></div>
                </div>
                <div class="todo__option-btn-wrap">
                    <div v-for="option in actionOption"
                         class="todo__option-btn"
                         :class="option.action">
                        {{option.action}}
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>
<script>
  export default {
    props: {
      todoItem: Object
    },
    data () {
      return{
        menu: false,
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
    methods:{
      openMenu() {
        this.menu = !this.menu
      }
    }

  }
</script>