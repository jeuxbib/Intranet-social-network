<template>
    <footer>
        <a class="social" href="https://www.twitter.com" target="_blank" aria-label="logo twitter">
        <span class="fa fa-twitter icon-md"></span></a>
        <a class="social" href="https://dribbble.com" target="_blank" aria-label="logo dribbble">
        <span class="fa fa-dribbble icon-md"></span></a>
        <a class="social" href="https://fr-fr.facebook.com" target="_blank" aria-label="logo facebook">
        <span class="fa fa-facebook icon-md"></span></a>
        <a class="social" href="https://www.instagram.com" target="_blank" aria-label="logo instagram">
        <span class="fa fa-instagram icon-md"></span></a>
    </footer>
</template>

<script>
export default {
    name: 'FooterPage'
}
</script>

<style lang="scss" scoped>
footer { display: flex; 
    justify-content: center; 
    align-items: center; 
    height: 55px;
    background: linear-gradient(rgb(61, 62, 63) 25%, rgb(130, 188, 238));
    
    a { 
        text-decoration: none;
        padding: 0 20px;
        &:hover {
            opacity: 0.7;
        }
        
        span {
            padding: 2px;
            font-size: 25px;
            color: white;
        }
    } 
}
</style>>