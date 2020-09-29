<template>
    <ul>
        <li :id="'task' + todo.id" v-for="todo in arr" v-bind:key="todo.id">
            <div :id="'taskNum' + todo.id">
                <span>Task № {{ todo.id }}</span>
            </div>
            <div class="text-wrapper">
                <h3 :id="'title'+ todo.id" @click="todo.status = !todo.status">{{ todo.title }}</h3>
                <p :id="'text'+ todo.id" v-show="!todo.status">{{ todo.text }}</p>
            </div>
            <input :id="'done' + todo.id" type="checkbox">
            <label @click="doneTask(todo.id)" :for="'done' + todo.id" class="done"></label>
            <button @click="deleteTask(todo.id)" class="delete"></button>
        </li>
    </ul>
</template>

<script>

export default {
    name: 'ListItem',
    props: [
        'arr'
    ],
    methods: {
        doneTask(id) {
            document.getElementById('title' + id).classList.toggle('crossed-out');
            document.getElementById('text' + id).classList.toggle('crossed-out');
            document.getElementById('task' + id).classList.toggle('complete');
            document.getElementById('taskNum' + id).classList.toggle('complete-num');
        },
        deleteTask(todo) {
            this.arr.splice(this.arr.indexOf(todo), 1);
            this.render();
        },
        render() {
            this.arr.forEach((el, i) => {
                el.id = i + 1;
            })
        }
    },
}
</script>

<style lang="scss" scoped>
ul {
    margin: 0 auto;
    padding-bottom: 20px;
    list-style-type: none;
    min-height: 365px;
    max-width: 1500px;
}

li {
    display: flex;
    justify-content: space-between;
    font-size: 26px;
    border: 1px dashed #a3bfb8;
    background-color: #6e8a85;
    color: #ffff;
    border-radius: 10px;

    &:not(:last-of-type) {
        margin-bottom: 20px;
    }

    & > div:first-child {
        background-color: darkred;
        color: #FFFFFF;
        flex-shrink: 0;
        border-radius: 10px 0 0 10px;
        padding: 0 20px;
        display: flex;
        justify-content: center;
        align-items: center;

        &.complete-num {
            background-color: green;
        }
    }
}

.complete {
    background-color: yellowgreen;
}

.text-wrapper {
    flex-grow: 1;
}

h3 {
    cursor: pointer;
}

.crossed-out {
    text-decoration: line-through;
    text-decoration-color: darkgreen;
    color: green;
}

.done,
.delete {
    width: 50px;
    height: 50px;
    margin: auto 10px;
    border-radius: 5px;
    position: relative;
    cursor: pointer;
    flex-shrink: 0;
}

.done:hover,
.delete:hover {
    box-shadow: 0 0 10px 5px rgba(0, 0, 0, 0.6);
}

.done {
    background-color: green;
    border: 1px solid greenyellow;
    outline: none;
}

input {
    position: absolute;
    clip: rect(0 0 0 0);
    width: 1px;
    height: 1px;
    margin: -1px;

    &:focus + .done {
        box-shadow: 0 0 10px 1px #FFFFFF;
    }

    &:checked + .done::before,
    &:checked + .done::after {
        content: '';
        position: absolute;
        background-color: #FFFFFF;
        height: 6px;
    }

    &:checked + .done::after {
        top: 22px;
        left: 12px;
        width: 70%;
        transform: rotate(-50deg);
    }

    &:checked + .done::before {
        top: 27px;
        left: 6px;
        width: 40%;
        transform: rotate(50deg);
    }

    &:checked + .done:hover::before,
    &:checked + .done:hover::after {
        box-shadow: 0 0 5px 1px rgba(255, 255, 255, 1);
    }
}

.delete {
    background-color: darkred;
    border: 1px solid red;
    outline: none;

    &:active {
        box-shadow: 0 0 5px 1px red;
    }

    &::after,
    &::before {
        content: '';
        position: absolute;
        top: 46%;
        left: 0;
        width: 100%;
        height: 4px;
        background-color: #FFFFFF;
        transform: rotate(45deg);
    }

    &::before {
        transform: rotate(-45deg);
    }

    &:active::before,
    &:active::after {
        box-shadow: 0 0 5px 1px rgba(255, 255, 255, 1);
    }
}
</style>