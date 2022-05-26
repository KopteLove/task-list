<template>
    <ul class="task-list">
        <li
                class="task-item"
                v-bind:class="{ complete: task.done }"
                :id="'task-' + task.id"
                v-for="(task, index) in listTask"
                v-bind:key="index"
                draggable="true"
                @dragover.prevent
                @dragenter.prevent
                @drop="onDrop($event, index)"
                @dragstart="startDrag($event, index)">
            <div class="task-num">
                <span>Task № {{ task.id }}</span>
            </div>
            <div class="text-wrapper" @click="task.open = !task.open">
                <h3 class="task-header">{{ task.title }}</h3>
                <p class="task-desk" v-show="task.open">{{ task.text }}</p>
            </div>
            <div class="task-buttons">
                <input :id="'done' + task.id" type="checkbox" :checked="task.done">
                <label @click="done($event, task)" :for="'done' + task.id" class="done"></label>
                <button @click="deleteTask(index)" class="delete"></button>
            </div>
        </li>
    </ul>
</template>

<script>

export default {
    name: 'ListItem',
    props: [
        'taskArr'
    ],
    data: () => {
        return {
            dragging: null
        };
    },
    methods: {
        deleteTask(task) {
            this.taskArr.splice(task, 1);
        },
        done(evn, task) {
            evn.preventDefault();
            task.done = !task.done;
        },
        startDrag(evt, index) {
            this.dragging = index;
        },
        onDrop(evt, to) {
            if (to === -1) {
                this.taskArr.splice(this.dragging, 1);
            } else {
                this.taskArr.splice(to, 0, this.taskArr.splice(this.dragging, 1)[0]);
            }
        },
    },
    computed: {
        listTask() {
            return this.taskArr;
        },
    }
}
</script>

<style lang="scss" scoped>
.task-list {
    margin: 0 auto;
    padding: 0 40px 20px;
    list-style-type: none;
    max-width: 1500px;
    width: 100%;
}

.task-item {
    display: flex;
    justify-content: space-between;
    font-size: 1.8rem;
    background-color: #6e8a85;
    color: #ffff;
    border-radius: 10px;
    cursor: move;

    &:not(:last-of-type) {
        margin-bottom: 20px;
    }
}

.task-num {
    background-color: darkred;
    color: #FFFFFF;
    flex-shrink: 0;
    border-radius: 10px 0 0 10px;
    padding: 0 20px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.complete {
    background-color: yellowgreen;

    .crossed-out {
        text-decoration: line-through;
        text-decoration-color: darkgreen;
        color: green;
    }

    .task-num {
        background-color: green;
    }
}

.text-wrapper {
    flex-grow: 1;
    padding: 0 10px;
}

.task-header {
    cursor: pointer;
    font-size: 1.8rem;
}

.task-desk {
    font-size: 1.5rem;
}

.task-buttons {
    display: flex;
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
    box-shadow: 0 0 10px 2px rgba(0, 0, 0, 0.6);
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
        width: 30%;
        transform: rotate(40deg);
    }

    &:checked + .done:hover::before,
    &:checked + .done:hover::after {
        box-shadow: 0 0 5px 0 rgba(255, 255, 255, 1);
    }
}

.delete {
    background-color: darkred;
    border: 1px solid red;
    outline: none;
    margin-right: 20px;

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

    &:hover::before,
    &:hover::after {
        box-shadow: 0 0 5px 0 rgba(255, 255, 255, 1);
    }
}

@media screen and (max-width: 767px) {
    .task-list {
        padding: 0 16px 20px;
    }

    .text-wrapper {
        padding: 0 5px;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .task-buttons {
        flex-direction: column;
    }

    .done,
    .delete {
        width: 30px;
        height: 30px;
        margin: 10px;
    }

    .task-num {
        padding: 10px;
    }

    .delete {
        margin: 0 10px 10px;

        &::after,
        &::before {
            height: 2px;
            width: 80%;
            left: 3px;
        }
    }

    input {
        &:checked + .done::before,
        &:checked + .done::after {
            height: 3px;
        }

        &:checked + .done::after {
            top: 13px;
            left: 8px;
            width: 60%;
        }

        &:checked + .done::before {
            top: 15px;
            left: 6px;
            width: 20%;
        }
    }
}
</style>