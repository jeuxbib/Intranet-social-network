<template>
    <div class="home">
        <HeaderHome/>
        <main>
            <section id="hello">
                <h1>Bienvenue dans notre réseau social interne</h1>
            </section>

            <section id="container">
                <div id="container__auth">
                  <div id="img">
                    <img src="../assets/icon-above-font.png" alt="Logo Groupomania" />
                  </div>
                  <div v-if="auth" class="login">
                      <LoginHome />
                      <p> Vous n'avez pas de compte ? 
                          <span @click="auth = !auth">Inscrivez-vous</span>
                      </p>
                  </div>
                  <div id="loginSignup" v-else class="signup">                        
                      <SignupHome />
                      <p> Vous avez un compte ?
                          <span @click="auth = !auth">Connectez-vous</span>
                      </p>
                  </div>
                </div>
            </section>
        </main>
    </div>
</template>

<script>
import HeaderHome from '@/components/HeaderHome.vue'
import LoginHome from "@/components/Login.vue"
import SignupHome from "@/components/Signup.vue"

export default {
  name: "HomeView",
  components: {
    HeaderHome,
    LoginHome,
    SignupHome
  },
  data() {
    return {
      auth: true,
    }
  }
}
</script>

<style scoped lang="scss">
main {
  padding: 5em;
  @media screen and (max-width: 450px){
      padding: 5px;
    }
  #hello {
    display: flex;
    text-align: center;
    justify-content: center;
    background: rgb(243, 244, 245);
    background-clip: text;
    -webkit-text-fill-color: transparent;
    font-size: 25px;
    @media screen and (max-width: 450px){
      font-size: 15px;
      padding: 10px;
    }
  }
  #container {
    display: flex;
    justify-content: center;

    &__auth {
      box-shadow: 1px 1px 15px rgb(83, 85, 86);
      border-radius: 20px;
      width: 400px;   
      padding: 10px;
      margin: 20px 10px;
      background: white;
      @media screen and (max-width: 450px){
        margin: 5px 5px 20px ;
      }
      #img {
        display: flex;
        align-items: center;
        padding: 8px 0 0 4px;
        img {
          width: 100%;
          height: 100%;
          object-fit: cover;
        }
      }
      p {
          text-align: center;
          font-size: 12px;
          span {
              color: blue;
              cursor: pointer;
          }
      }
    }
  }
}
</style>