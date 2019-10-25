<template>
    <div id="app">
        <h1>Tarefas</h1>
        <TaskProgress :progress="progress" />
        <NewTask @newTask="addTask" />
        <TaskGrid @taskDeleted="deleteTask" 
                  @taskStateChanged="changeStatusTask" 
                  :tasks="tasks"/>
    </div>
</template>

<script>
import NewTask from './components/NewTask'
import TaskGrid from './components/TaskGrid'
import TaskProgress from './components/TaskProgress'

export default {
    components: { NewTask, TaskGrid, TaskProgress, },

    data() {
        return {
            tasks: [],
        }
    },

    methods: {
        addTask(task) {
            let sameName = t => t.name === task.name;
            let reallyNew = this.tasks.filter(sameName).length == 0;

            if(reallyNew) {
                this.tasks.push({
                    name: task.name,
                    done: false,
                })
            }
        },

        deleteTask(i) {
            this.tasks.splice(i, 1);
        },

        changeStatusTask(i) {
            this.tasks[i].done = !this.tasks[i].done;
        },
    },

    computed: {
        progress() {
            let total = this.tasks.length;
            let done = this.tasks.filter(t => t.done).length;

            return Math.round(done / total * 100) || 0;
        }
    },

    watch: {
        tasks: {
            deep: true,
            handler() {
                localStorage.setItem('tasks', JSON.stringify(this.tasks));
            },
        }
    },

    created() {
        let tasks = localStorage.getItem('tasks');
        let json = JSON.parse(tasks);

        this.tasks = Array.isArray(json) ? json : [];
    }
}
</script>

<style>
    body {
        font-family: 'Lato', 'sans-serif';
        background: linear-gradient(to right, rgb(22, 34, 42), rgb(48, 96, 115));
        color: #fff;
    }
    
    #app {
        display: flex;
        flex: 1;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100%;
    }

    #app h1 {
        margin-bottom: 5px;
        font-weight: 300;
        font-size: 3rem;
    }
</style>