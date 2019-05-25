<template>
    <li>
        <slot name="content"></slot>
    </li>
</template>

<script>
export default {

}
</script>

<style>
    li {
        border: 1px solid #86aaf8;
        border-radius: 5px;
        min-width: calc(15vw - 1.77em);
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
        background-color: red;
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
        background-color: green;
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


</style>
