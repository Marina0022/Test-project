<template>
    <div class="form-container">
        <div class="input-container">
            <label for="name">Имя</label>
            <input id="name" v-model="user.name" type="text">
        </div>
        <div class="input-container">
            <label for="surname">Фамилия</label>
            <input id="surname" v-model="user.surname" type="text">
        </div>
        <div class="input-container">
            <label for="age">Возраст</label>
            <input id="age" v-model="user.age" type="number">
        </div>
        <div class="input-container">
            <label for="address">Адрес</label>
            <input id="address" v-model="user.address" type="text">
        </div>
        <div class="input-container">
            <label for="experience">Стаж</label>
            <input id="experience" v-model="user.experience" type="text">
        </div>
        <p v-if="error && !editUserForm.name" class="error">{{ error }}</p>
        <button v-if="!editUserForm.name" class="add-btn" @click="submit">Добавить</button>
        <button v-else class="add-btn" @click="$modal.hide('user-form')">Сохранить</button>
    </div>
</template>

<script>
export default{
    props: {
        editUserForm: {
            type: Object
        }
    },
    data(){
        return{
            user: {
                name: '',
                surname: '',
                age: null,
                address: '',
                experience: null,
                id: 0
            },
            error: ''
        }
    },
    mounted(){
        if(this.editUserForm.name){
            this.user = this.editUserForm
        }
    },
    methods: {
        submit(){
            this.error = ''
            if(this.isRequired(this.user.name) && 
                this.isRequired(this.user.surname) && 
                this.isRequired(this.user.age) && 
                this.isRequired(this.user.address) && 
                this.isRequired(this.user.experience)){
                if(!this.editUserForm.name){
                    this.user.id++
                    this.$emit('submited', this.user)
                }else{
                    this.$emit('edited', this.user)
                }        
            }else{
                this.error = 'All the fields are required'
            }
        },
        isRequired(value) {
            return /([^\s])/.test(value)
        }
    }
}
</script>

<style>
    .form-container{
        padding: 20px;
    }
    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 10px;
    }
    .input-container input{
        height: 30px;
        padding-left: 5px;
        border: 1px solid rgb(190, 190, 190);
        border-radius: 4px;
        outline: none;
    }
    .input-container label{
        margin-bottom: 5px;
        color: gray;
        font-weight: 600;
    }
    .add-btn{
        border: 0;
        outline: none;
        margin: 0 auto;
        padding: 5px 20px;
        color: white;
        background-color: rgb(67, 138, 67);
        height: 40px;
        border-radius: 4px;
        width: 40%;
        display: block;
        cursor: pointer;
    }
    .error{
        color: rgb(173, 5, 5);
        padding: 0 0 5px 0;
    }
</style>