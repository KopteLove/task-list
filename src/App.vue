<template>
    <div id="app">
        <Header/>
        <AddItem :taskArr="taskArr"/>
        <ListItem :taskArr="taskArr"/>
        <Footer/>
    </div>
</template>

<script>
import Header from './components/Header.vue'
import ListItem from './components/ListItem.vue'
import AddItem from './components/AddItem.vue'
import Footer from "@/components/Footer";

export default {
    name: 'App',
    components: {
        Footer,
        Header,
        ListItem,
        AddItem
    },
    data() {
        return {
            taskArr: JSON.parse(localStorage.getItem('taskStorage') || "[]"),
        }
    },
    watch: {
        taskArr: {
            handler: function(taskArr) {
                localStorage.setItem('taskStorage', JSON.stringify(taskArr))
            },
            deep: true
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
}

html {
    font-size: 14px;
}

body {
    margin: 0;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    background-color: #b2ccc7;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

@media screen and (max-width: 767px) {
    html {
        font-size: 8px;
    }
}
</style>
