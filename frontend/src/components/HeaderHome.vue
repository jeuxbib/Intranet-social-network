<template>
    <header class="header-home">
        <img src="../assets/Logo-groupomania.png" alt="Logo Groupomania">
    </header>
  
</template>

<script>
export default {
    name: 'HeaderHome'
}
</script>

<style scoped lang="scss">
header {
    display: flex;
    align-items: center;
    height: 60px;
    background: linear-gradient(rgb(61, 62, 63) 25%, rgb(159, 162, 164));
    padding: 10px;
    
    img {
       width: 50px;
       height: 40px;
       object-fit:center;
    }
}
</style>