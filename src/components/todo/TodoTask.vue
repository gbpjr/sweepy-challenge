<template>
    <div class="task" :class="{ active: active === true }" @click="toggleCurrentTask()">
        <span>{{ task.title }}</span>
    </div>
</template>

<script>
    export default {
        name: "TodoTask",
        props: {
            task: {
                type: Object,
            },
            active: {
                type: Boolean,
                default: false,
            }
        },
        
        methods: {
            toggleCurrentTask: function () {
                if(!this.active)
                    return this.$emit('setActive', this.task);

                return this.$emit('setActive', null);
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import "../../assets/sass/mixins";

    .task {
        display: flex;
        justify-content: space-between;
        font-size: 14px;
        margin: 15px 0;
        padding: 15px;
        background: #fff;
        border-radius: 5px;
        transition: 0.1s;
        @include animate(.2s,.1s);

        &.active {
            @include animate(.2s,.1s);
            @include scale(1.05);
            background: #d8fca8;
            box-shadow: 2px 2px 7px rgba(0,0,0,.15);
        }

        &:hover {
            @include animate(.2s,.1s);
            box-shadow: 2px 2px 5px rgba(0,0,0,.05);
            transition: 0.1s;
        }
    }
</style>
