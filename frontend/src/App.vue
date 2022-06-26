<template>
  <div id="app">
    <router-view/>
    <FooterPage/>
  </div>
</template>

<script>
import FooterPage from '@/components/Footer.vue'

export default {
  name: "App",
  components: {
    FooterPage
  }
}
</script>

<style lang="scss">
* { 
  -webkit-box-sizing: border-box; 
  box-sizing: border-box;
  overflow-x: hidden;
  margin: 0; 
  padding: 0;
}
#app { 
  font-family: Arial, Helvetica, sans-serif;
  background: linear-gradient(-45deg, #ee7752, #e778a2, #23a6d5, #23d5ab);
	background-size: 400% 400%;
	animation: gradient 8s ease infinite;
	height: 100vh;
}

@keyframes gradient {
	0% {
		background-position: 0% 50%;
	}
	50% {
		background-position: 100% 50%;
	}
	100% {
		background-position: 0% 50%;
	}
}


</style>
