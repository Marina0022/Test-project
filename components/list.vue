<template>
    <table>
        <tr>
            <th>Имя</th>
            <th>Фамилия</th>
            <th>Возраст</th>
            <th>Адрес</th>
            <th>Стаж</th>
        </tr>
        <tr v-for="(item, index) in list" :key="index">
            <td>{{ item.name }}</td>
            <td>{{ item.surname }}</td>
            <td>{{ item.age }}</td>
            <td>{{ item.address }}</td>
            <td>
                <div class="justify-between align-center">
                    <span>{{ item.experience }}</span>
                    <img class="edit" src="@/assets/images/edit.svg" alt="icon" @click="edit(index)">
                </div> 
            </td>
        </tr>
    </table>
</template>

<script>
    export default{
        props: {
            list: {
                type: Array
            }
        },
        methods: {
            edit(i){
                this.list.forEach((item, index) => {
                    if(index === i){
                        this.$emit('edit', item)
                    }
                })
            }
        }
    }
</script>

<style>
    table{
        width: 100%;
        border: 1px solid #bebebe;
        border-collapse: collapse;
    }
    table tr th,td {
        border: 1px solid #bebebe;
        border-collapse: collapse;
        padding: 10px;
    }
    table tr th{
        color: #56575c;
    }
    .edit{
        width: 20px;
        cursor: pointer;
    }
    .justify-between{
        display: flex;
        justify-content: space-between;
    }
    .align-center{
        align-items: center;
    }
</style>