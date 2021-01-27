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
      'arr'
    ],
    data() {
        return {
            newTextTask: '',
        }
    },
    methods: {
        addItem() {
            this.newTextTask = this.$refs.inputHeader.value.trim();
            if (this.newTextTask.length > 0 && this.newTextTask !== ' ') {
                let obj = {};
                obj.id = this.arr.length + 1;
                obj.title = this.$refs.inputHeader.value;
                obj.text = this.$refs.inputDescription.value;
                obj.status = true;
                this.$refs.inputHeader.value = '';
                this.$refs.inputDescription.value = '';
                this.arr.push(obj);
            }
        }
    },
}
</script>

<style lang="scss" scoped>
section {
    padding: 0 20px 20px 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

h2 {
    font-size: 30px;
}

input {
    width: 50%;
    height: 50px;
    font-size: 30px;
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
    font-size: 25px;
    padding: 5px 10px;

    &:focus {
        border: 1px solid transparent;
        box-shadow: 0 0 10px 1px #FFFFFF,
        inset 0 0 0 2px yellowgreen;
    }
}

button {
    height: 50px;
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
    font-size: 25px;
    line-height: 52px;

    &:hover {
        box-shadow: 0 0 10px 5px rgba(0, 0, 0, 0.6);
        text-shadow: 0 0 5px #ffffff;
    }

    &:focus {
        box-shadow: 0 0 10px 1px #FFFFFF;
    }

    &::after,
    &::before {
        content: '';
        position: absolute;
        top: 22px;
        right: 6px;
        width: 32px;
        height: 6px;
        background-color: #FFFFFF;
    }

    &::before {
        transform: rotate(90deg);
    }

    &:hover::before,
    &:hover::after {
        box-shadow: 0 0 2px 1px rgba(255, 255, 255, 1);
    }
}
</style>