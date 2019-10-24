<template>
    <div id="app">
        <h1>Tarefas</h1>
        <TaskGrid :tasks="tasks"/>
    </div>
</template>

<script>
import TaskGrid from './components/TaskGrid.vue'

export default {
    components: { TaskGrid, },
    data() {
        return {
            tasks: [
                {   
                    id: 3,
                    name: 'Estudar VueJS', 
                    done: false
                },
                {   
                    id: 2,
                    name: 'Estudar MongoDB',
                    done: false
                },
                {   
                    id: 1,
                    name: 'Estudar Java',
                    done: true
                }
            ],
        }
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