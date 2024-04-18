<template>
    <div class="main">
        <h1>You Scored</h1>
        <h1>{{ marks + "/" + total }}</h1>
        <ul>
            <li>Attemped-{{ attempted }}</li>
            <li>Not-Attemped-{{ total - attempted }}</li>
            <li>Correct-{{ marks }}</li>
            <li>Incorrect-{{ attempted - marks }}</li>
        </ul>
        <button @click="$emit('resetAll')">New Quiz</button>
    </div>
</template>
<script>
export default {
    name: "Result",
    props: ['marks', 'total', "attempted"]
} 
</script>
<style scoped>
.main {
    height: 500px;
    width: 500px;
    background-color: white;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    box-shadow: 0 0 10px 0.5;
}

button {
    padding: 10px;
    margin-top: 25px;
    width: 25%;
    background-color: antiquewhite;
    border: 1px solid;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
    font-size: large;
}

button:hover {
    background-color: rgb(223, 200, 171);
}

ul {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    column-gap: 10px;
    list-style: none;
    height: 20%;
    font-size: larger;
    font-weight: bold;
}
</style>