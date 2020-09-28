<template>
    <div id="app">
        <!-- component | navbar -->
        <navbar/>

        <!-- sweepy todo -->
        <div class="sweepy-todo">
            <todo-column :title="status.title" v-for="(status, index) in columnStatus"
                         :key="status.id" v-bind:index=index
                         @getTask="getCurrentTask(status.id)">
                <todo-task v-for="task in filterStatus(status.id)"
                           @setActive="setActive"
                           :active="isActive(task)"
                           :task="task" :key="task.id"/>
            </todo-column>
        </div>
        <delete-button
            v-if="active"
            v-on:click.native="remove()"
        >
        </delete-button>
    </div>
</template>

<script>
    import Navbar from "@/components/global/Navbar";
    import TodoColumn from "@/components/todo/TodoColumn";
    import TodoTask from "@/components/todo/TodoTask"; 
    import DeleteButton from "@/components/todo/DeleteButton";

    export default {
        name: 'App',
        components: {TodoTask, TodoColumn, Navbar, DeleteButton},

        data() {
            return {
                columnStatus: [
                    {
                        id: 'backlog',
                        title: 'Backlog',
                    },
                    {
                        id: 'todo',
                        title: 'To Do',
                    },
                    {
                        id: 'doing',
                        title: 'Doing',
                    },
                    {
                        id: 'done',
                        title: 'Done',
                    },
                ],
                active: null,
                selectedIndex: null,
                tasks: [
                    {
                        'id': 1,
                        'title': 'Jogar lol',
                        'status': 'backlog'
                    },
                    {
                        'id': 2,
                        'title': 'estudar vuejs',
                        'status': 'doing'
                    },
                    {
                        'id': 3,
                        'title': 'trabalhar',
                        'status': 'done'
                    },
                    {
                        'id': 4,
                        'title': 'dormir',
                        'status': 'backlog'
                    },
                    {
                        'id': 5,
                        'title': 'viajar',
                        'status': 'backlog'
                    },
                    {
                        'id': 6,
                        'title': 'tomar breja',
                        'status': 'done'
                    }
                ]
            }
        },

        methods: {
            filterStatus: function (status) {
                return this.tasks.filter(
                    (task) => {
                        return task.status === status
                    })
            },

            setActive: function (task) {
                this.active = task;
                if(this.active)
                    this.selectedIndex = this.tasks.findIndex(t => t.id === task.id )
            },

            isActive: function (task) {
                if (task && this.active) {
                    if (task.id === this.active.id)
                        return true;
                }

                return false;
            },

            getCurrentTask: function (statusId) {
                if (this.active) {
                    this.active.status = statusId;
                }
            },

            remove: function () {
                this.$delete(this.tasks, this.selectedIndex)
                this.active = null
            },

            addTask: function (newTask) {
                if(newTask)
                    this.tasks.push({
                        'id': Math.random() * 20,
                        'title': newTask,
                        'status': 'backlog'
                    })
            }
        }
    }
</script>

<style lang="scss">
    @import "./assets/sass/styles.scss";

    .sweepy-todo {
        display: flex;
        justify-content: flex-start;
        flex-wrap: wrap;
        margin: 15px;
        align-items: flex-start;
    }
    
</style>
