<template>
    <li :class="setClass">
        <slot name="content"></slot>
        <span>{{ task.description }}</span>
    </li>
</template>

<script>
    export default {
        props: {
            task: {
                type: Object,
                required: true
            }
        },
        computed: {
            setClass() {
                return {
                    pending: !this.task.done,
                    done: this.task.done
                }
            }
        }
    }
</script>

<style>
    li {
        border: 1px solid #86aaf8;
        border-radius: 6px;
        width: 350px;
        height: 160px;
        box-sizing: border-box;
        padding: 10px;
        margin: 5px; 
        overflow: hidden;   
        font-size: 1.2em;
        font-weight: 300; 
    }
    li span{
        padding: 1em;
        display: inline-block;
    }
    .task-header {
        border-bottom: 1px solid #86aaf8;        
    }
    .task-header div {
        padding: 0 0 0 0; 
        overflow: auto;
    }
    .task-header div button {   
        float: right;    
        width: 2em;
        height: 2em;        
        background-color: inherit;
        color: inherit;
        border: none;
        outline: none;
        font-weight: 900
    }
    .task-header div button:hover {
        border-radius: 50%;
        background-color: rgb(160, 5, 5);
        color: #e5e5f1;
        cursor: pointer;  
    }
    .check-area {
        margin: 0;
        padding: 0;
        float: left;
        width: 1.7em;
        height: 1.7em; 
    }
    .check-area:hover {
        border-radius: 50%;
        background-color: rgb(2, 63, 2);
        cursor: pointer;
    }
    .check {
        width: 3px;
        height: 10px;
        border-right: solid 2.4px #858596;
        border-bottom: solid 2.4px #858596;
        transform: rotate(45deg) translateX(100%);        
        padding: 0;
        margin: 0 6px 2px;
    }
    .check-area:hover .check {
        border-right: solid 2.4px #e5e5f1;
        border-bottom: solid 2.4px #e5e5f1;
    }
    .check::before {
        content: '';
    }
    .pending {
        background-color:  #cf0505;
        border-left: 5px solid #a80b0b;
        border-bottom: 5px solid #a80b0b;
        color: #eccdcd;
    }
    .done{
        background-color:  #0e8122;
        border-left: 5px solid #03460e;
        border-bottom: 5px solid #03460e;
        color: #c7f3c7;

    }    
    .done span {
        text-decoration: line-through
    }

</style>
