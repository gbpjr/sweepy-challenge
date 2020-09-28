<template>
    <div class="column" @click="$emit('getTask')">
        <span class="column-title">{{ title }}</span>

        <div class="tasks-wrapper">
            <slot></slot>
        </div>
        <span v-if="index===0" :key="index" @click="willAdd" class="column-footer">Add task...</span>
        
        <span v-if="index===0" v-show="isAdding" class="add-new">
            <div class="field-container">
                <input 
                    class="field-input" 
                    type="text" placeholder="" 
                    v-model="newTask"
                    v-on:input="newTask = $event.target.value"
                >
                <label class="field-placeholder" for="inputTask">New task</label>
            </div>
            <a href="#" @click="addTask()" class="action-button shadow animate yellow">Add</a>
        </span> 
    </div>
</template>

<script>
    export default {
        name: "TodoColumn",
        props: {
            title: {
                type: String,
            },
            index: {
                type: Number
            }
        },
        data: function () {
            return {
                isAdding: false,
                newTask: null
            }
        },
        methods: {
            willAdd: function () {
                this.isAdding = true
            },
            addTask: function() {
                this.$parent.addTask(this.newTask);
                console.log(this.newTask)
            },    
        }
    }
</script>

<style lang="scss" scoped>
    .column {
        box-shadow: 2px 2px 5px #e1e2e3;
        padding: 15px;
        width: 20%;
        margin: 15px;
        background: #fafafa;
        border-radius: 25px;

        &-title {
            font-weight: bold;
        }

        &-footer {
            font-size: 13px;
            color: #a0a0a0;
        }
        .add-new {
            display: flex;
            justify-content: flex-start;
            align-items: center;
            margin: 15px;
        }

        .custom-input {
            border: 0;
            border-bottom: 2px solid #e1e2e3;
        }
        .custom-input:focus {
            border: none;
            outline: none;
            border-bottom: 2px solid #e1e2e3;

        }

        // ...

        .animate
        {
            transition: all 0.1s;
            -webkit-transition: all 0.1s;
        }

        .action-button
        {
            display: flex;
            justify-content: center;
            margin: 0px 10px 10px 0px;
            width: 100%;
            height: 100%;
            border-radius: 10px;
            font-family: 'Pacifico', cursive;
            font-size: 25px;
            color: #FFF;
            text-decoration: none;	
        }

        .yellow
        {
            background-color: #F2CF66;
            border-bottom: 5px solid #D1B358;
            text-shadow: 0px -2px #D1B358;
        }

        .action-button:active
        {
            transform: translate(0px,5px);
            -webkit-transform: translate(0px,5px);
            border-bottom: 1px solid;
            margin-bottom: 15px;
        }

        //.....

        $field-container-padding: 5px;
        $label-padding: $field-container-padding !default;


        .field-container{
            position: relative;
            border-bottom: 1px solid #bcbaba;
            height:50%;
            width:100%;
            padding-left:12px;
        }

        .field-placeholder{
            position: absolute;
            top: 50%;
            transform: translate(#{$label-padding}, -50%);
            pointer-events: none;
            transition: all .14s ease-in-out;
            font-size:18px;
            color:#adadad;
        }

        input[type="text"].field-input{
            color: #333;
            border:none;
            padding: $label-padding;
            margin-top: 15px;
            font-size: 13px;
            display: block;
            box-sizing: border-box;
            width: 100%;
            bottom:0px;
            &:focus {
                outline: none;
            }
            &.c-fix,
            &:focus,
            &:not(:placeholder-shown)
            {
                border-color: transparent;
                ~ label {
                color:#646669;
                font-size: 11px;
                top: calc(30% - .5rem);
                transform: translate(#{$label-padding}, 0%);
                }
            }
            
            &::-webkit-input-placeholder {
                color: transparent;
            }
            &::-moz-placeholder {
                color: transparent;
            }
            &:-ms-input-placeholder {
                color: transparent;
            }
        }
    }
    

</style>
