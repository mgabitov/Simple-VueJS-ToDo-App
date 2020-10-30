<template>
    <div>
        <h1>Список задач</h1>
        <div class="row">
            <div class="input-field col s6">
                <select ref="select" v-model="filter">
                    <option value="" disabled selected>Выберите тип задач</option>
                    <option value="Активна">Активные</option>
                    <option value="Просрочена">Просроченные</option>
                    <option value="Завершена">Завершённые</option>
                </select>
                <label>Фильтр задач</label>
            </div>
        </div>
        <button v-if="filter" class="btn btn-small materialize-red" @click="filter = null">Очистить фильтр</button>

        <hr>

        <table v-if="tasks.length">
            <thead>
            <tr>
                <th>#</th>
                <th>Название</th>
                <th>Дата</th>
                <th>Описание</th>
                <th>Статус</th>
                <th>Открыть</th>
                <th class="td-delete">Удалить</th>
            </tr>
            </thead>
            <tbody>
                <tr v-for="(task, idx) of displayTasks"
                    :key="task.id"
                >
                    <td>{{idx + 1}}</td>
                    <td>{{task.title}}</td>
                    <td>{{new Date(task.date).toLocaleDateString()}}</td>
                    <td class="td-description"><div class="text">{{task.description}}</div></td>
                    <td>{{task.status}}</td>
                    <td>
                        <router-link tag="button" class="btn btn-small" :to="'/task/' + task.id">
                            Открыть
                        </router-link>
                    </td>
                    <td class="td-delete"><button class="button" @click="deleteHandler(task.id)">&times;</button> </td>
                </tr>
            </tbody>
        </table>
        <p v-else>Задач нет</p>
    </div>
</template>

<script>
    export default {
        data: () => ({
            filter: null
        }),
       computed: {
           tasks() {
               return this.$store.getters.tasks
           },
           displayTasks(){
               return this.tasks.filter(t => {
                   if (!this.filter) {
                       return true
                   }
                   return t.status === this.filter
               })
           }
       },
       methods: {
            deleteHandler(id) {
                console.log(id)
                this.$store.dispatch('deleteTask', id)
            }
       },
       mounted() {
           M.FormSelect.init(this.$refs.select);
        }
    }
</script>

<style lang="scss" scoped>
    .td-delete {
        text-align: center;
    }
    .td-description {
        max-width: 450px;
    }
    .text {
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
    }
    .button {
        background-color: red;
        border-radius: 50%;
        border-color: red;
        color: white;
        font-weight: bold;
        display: inline-block;
    }
</style>