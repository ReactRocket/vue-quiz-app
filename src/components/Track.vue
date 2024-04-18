<template>
    <div class="tracker">
        <ul>
            <li v-for="(que, index) in questions">
                <span @click="$emit('changeQuestion',index)" v-if="index == currentQuestion" class="blueBubble"> {{ index + 1 }}</span>
                <span @click="$emit('changeQuestion',index)" v-else-if="questions[index].isAttempted && questions[index].result" class="greenBubble"> {{ index
                    + 1 }}</span>
                <span @click="$emit('changeQuestion',index)" v-else-if="questions[index].isAttempted && !questions[index].result" class="redBubble"> {{ index
                    + 1 }}</span>
                <span @click="$emit('changeQuestion',index)" v-else class=""> {{ index + 1 }}</span>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    name: "Track",
    props: ['questions', 'currentQuestion']
    
}
</script>
<style scoped>
.tracker {
    height: 70px;
    width: 80%;
    margin: auto;
}

ul {
    list-style: none;
    display: flex;
    width: 100%;
    justify-content: space-between;
}

li {
    overflow: hidden;
}

.redBubble {
    background: rgb(236, 90, 90);
    color: white;
}

.blueBubble {
    background: rgba(69, 69, 255, 0.685);
    color: white;

}

.greenBubble {
    background: rgba(43, 201, 43, 0.781);
    color: white;

}

span {
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    border: 1px solid black;
    cursor: pointer;
    font-weight: bold;
}
</style>