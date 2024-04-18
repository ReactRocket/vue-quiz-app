<template>
    <ul>
        <b>*Instructions:</b>
        <li class="blue"> For Current Question.</li>
        <li class="green"> For Correct Answer.</li>
        <li class="red"> For Wrong Answer.</li>
    </ul>
</template>
<script>
export default {
    name: "Instruction",

}
</script>
<style scoped>
ul {
    padding: 20px;
    height: 10%;
    width: 80%;
    margin: auto;
    display: flex;
    column-gap: 20px;
    list-style: none;
}


.blue::before {
    padding: 2px 10px;
    margin-right: 7px;
    border: 1px solid black;
    border-radius: 50%;
    content: "";
    background: rgba(69, 69, 255, 0.685);
    color: white;
}

.green::before {
    padding: 2px 10px;
    margin-right: 7px;
    border: 1px solid black;
    border-radius: 50%;
    content: "";
    background: rgba(43, 201, 43, 0.781);
    color: white;

}


.red::before{
    padding: 2px 10px;
    margin-right: 7px;
    border: 1px solid black;
    border-radius: 50%;
    content: "";
    background: rgb(236, 90, 90);
    color: white;

}
</style>