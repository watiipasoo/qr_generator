<template>
    <header class="header">
        <h2>My QR Generator</h2>
        <h2>My QR Generator</h2>
    </header>
</template>

<script>
export default {
    name: 'BodyHeader',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.header h2 {
    font-size: 2em;
    position: absolute;
    text-align: center;
}

.header h2:nth-child(1) {
    color: #099FFF;
    -webkit-text-stroke: 2px #18181B;
}

.header h2:nth-child(2) {
    color: #2c3e50;
    animation: animate 4s ease-in-out infinite;
}

/* Use the same keyframe animation */
@keyframes animate {

    0%,
    100% {
        clip-path: polygon(0% 45%, 16% 44%, 33% 50%, 54% 60%, 70% 61%, 84% 59%, 100% 52%, 100% 100%, 0% 100%);
    }

    50% {
        clip-path: polygon(0% 60%, 15% 65%, 34% 66%, 51% 62%, 67% 50%, 84% 45%, 100% 46%, 100% 100%, 0% 100%);
    }
}
</style>
