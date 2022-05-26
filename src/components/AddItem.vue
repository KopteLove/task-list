<template>
    <section>
        <h2>Task Header</h2>
        <input ref="inputHeader" type="text">
        <h2>Task Description</h2>
        <textarea rows="3" ref="inputDescription"></textarea>
        <button @click="addItem">Add Task</button>
    </section>
</template>

<script>

export default {
    name: 'AddItem',
    props: [
      'taskArr'
    ],
    data() {
        return {
            newTextTask: '',
        }
    },
    methods: {
        addItem() {
            let numTask = 0;
            if (this.taskArr.length > 0) {
                this.taskArr.forEach(function(item) {
                    numTask = numTask > item.id ? numTask : item.id;
                });
            }

            this.newTextTask = this.$refs.inputHeader.value.trim();
            if (this.newTextTask.length > 0 && this.newTextTask !== ' ') {
                let obj = {};
                obj.id = numTask + 1;
                obj.title = this.$refs.inputHeader.value;
                obj.text = this.$refs.inputDescription.value;
                obj.open = false;
                obj.done = false;
                this.$refs.inputHeader.value = '';
                this.$refs.inputDescription.value = '';
                this.taskArr.unshift(obj);
            }
        }
    },
}
</script>

<style lang="scss" scoped>
section {
    padding: 0 16px 16px 16px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

h2 {
    font-size: 2.1rem;
}

input {
    width: 50%;
    height: 50px;
    font-size: 2.1rem;
    border-radius: 10px;
    border: 1px solid #657d75;
    outline: none;
    color: #5f9ea0;
    padding: 5px;

    &:focus {
        border: 1px solid transparent;
        box-shadow: 0 0 10px 1px #FFFFFF,
        inset 0 0 0 2px yellowgreen;
    }
}

textarea {
    width: 50%;
    border: 1px solid #657d75;
    outline: none;
    color: #5f9ea0;
    font-size: 1.8rem;
    padding: 5px 10px;

    &:focus {
        border: 1px solid transparent;
        box-shadow: 0 0 10px 1px #FFFFFF,
        inset 0 0 0 2px yellowgreen;
    }
}

button {
    height: 53px;
    margin-top: 20px;
    border-radius: 5px;
    position: relative;
    cursor: pointer;
    outline: none;
    background-color: yellowgreen;
    border: 1px solid yellow;
    color: #ffffff;
    font-weight: bold;
    padding: 0 100px 0 50px;
    font-size: 1.8rem;

    &:hover {
        box-shadow: 0 0 10px 2px rgba(0, 0, 0, 0.6);
        text-shadow: 0 0 2px #ffffff;
    }

    &:focus {
        box-shadow: 0 0 10px 1px #FFFFFF;
    }

    &::after,
    &::before {
        content: '';
        position: absolute;
        top: 50%;
        right: 11px;
        width: 32px;
        height: 6px;
        background-color: #FFFFFF;
        transform: translateY(-50%);
    }

    &::before {
        transform: translateY(-50%) rotate(90deg);
    }

    &:hover::before,
    &:hover::after {
        box-shadow: 0 0 2px 0 rgba(255, 255, 255, 1);
    }
}

@media screen and (max-width: 767px) {
    textarea,
    input {
        width: 100%;
    }

    button {
        height: 30px;
        padding: 0 50px 0 20px;

        &::after,
        &::before {
            width: 16px;
            height: 4px;
        }
    }
}
</style>