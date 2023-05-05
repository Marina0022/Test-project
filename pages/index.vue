<template>
  <div>
    <list :list="list" @edit="edit" />
    <div class="add" @click="show">+</div>
    <modal name="user-form"><user-form :editUserForm="editUserForm" @submited="submited" @edited="edited" /></modal>
  </div>
</template>

<script>
import list from '@/components/list.vue'
import userForm from '@/components/user-form.vue'
export default {
  name: 'Home',
  components: {
    list,
    userForm
  }, 
  data() {
    return {
      list: [],
      editUserForm: {}
    }
  },
  methods: {
    show () {
      this.$modal.show('user-form');
    },
    submited(value){
      this.list.push(value)
      this.$modal.hide('user-form')
    },
    edit(user){
      this.$modal.show('user-form');
      this.editUserForm = user
    },
    edited(editedItem){
      this.list.forEach(item => {
          if(item.id === editedItem.id){
            item = editedItem
          }
      })
      this.$modal.hide('user-form')
    }
  }
}
</script>

<style>
  .add{
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    background-color: rgb(67, 138, 67);
    font-size: 25px;
    font-weight: 700;
    color: white;
    width: 40px;
    height: 40px;
    cursor: pointer;
    margin-top: 10px;
  }
  .vm--modal{
    height: auto !important;
    top: 50% !important;
    transform: translateY(-50%);
    box-shadow: none !important;
  }
</style>
