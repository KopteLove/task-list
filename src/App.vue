<template>
    <div id="app">
        <Header/>
        <AddItem :arr="todos"/>
        <ListItem :arr="todos"/>
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
            todos: [],
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
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
}
</style>
