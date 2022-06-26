<template>
    <div class="profil">
        <HeaderForum/>
        <main>
            <section id="hello">
                <h1>Profil de {{ username }}</h1>
            </section>

            <section id="container">

                <div id="container__profil">
                    <img v-if="avatar != ''" :src="avatar" class="avatar" alt="photo de profil">
                    <img v-else src="../assets/avatar.png" class="avatar" alt="avatar">
                    <label for="file" id="label">Modifier ma photo</label>
                    <input v-on:change="selectFile" id="file" name="file" type="file" accept="avatar/*">

                    <div id="container__form">
                        <h2>Vos informations</h2>
                        <div id="form">
                            <label for="pseudo">Pseudo :</label>
                            <input type="text" name="pseudo" id="pseudo" v-model="username">
                            <label for="email">Email :</label>
                            <input type="email" name="email" id="email" v-model="email">
                            <div id="error">{{ error }}</div>
                        </div>
                        <div id="button">
                            <button @click="updateUser()">Modifier mes informations</button>
                            <button @click="deleteUser()">Supprimer mon compte</button>
                        </div>
                    </div>

                </div>

            </section>
        </main>
    </div>
</template>

<script>
import HeaderForum from "@/components/HeaderForum.vue";
export default {
    name: "ProfilView",
    components: { 
        HeaderForum
    },
    data() {
        return {
            username: '',
            email: '',
            avatar: '',
            error: '',
            regexUsername: /[a-zâäàéèùêëîïôöçñA-Z-0-9\s]{4,25}/,
            regexEmail: /[a-zâäàéèùêëîïôöçñA-Z0-9.-_]+[@]{1}[a-zA_Z0-9.-_]+[.]{1}[a-z]{2,4}/
        }
    },
    mounted() {
        const id = localStorage.getItem('userId')
        this.axios.get(`http://localhost:3000/api/auth/${id}`, {
            headers: {
                Authorization: 'Bearer ' + localStorage.getItem('token')
            }
        })
        .then((res) => {
            console.log(res)
            this.username = res.data.username
            this.email = res.data.email
            this.avatar = res.data.avatar
        })
        .catch((err) => {
            console.log(err)
        });
    },

    methods: {
        selectFile(e) {
            const id = localStorage.getItem('userId')
            this.avatar = e.target.files[0];
            const data = new FormData()
            data.append('image', this.avatar)
            this.axios.put(`http://localhost:3000/api/auth/${id}`, data, {
                headers: {
                    Authorization: 'Bearer ' + localStorage.getItem('token')
                }
            })
            .then((res) => {
                this.avatar = res.data.avatar
            })
            .catch((err) => {
                console.log(err)
            });
        },

        updateUser() {
            if (this.username == '' || this.email == '') {
                return this.error ='⚠ Veuillez renseigner tous les champs du formulaire !'
            } 
            else if (!this.regexUsername.test(this.username)){
                return this.error ='⚠ pseudo non conforme !'
            } 
            else if (!this.regexEmail.test(this.email)){
                return this.error ='⚠ email non conforme !'
            }
            else {
                const id = localStorage.getItem('userId')
                const data = new FormData();
                data.append('email', this.email);
                data.append('username', this.username);
                this.axios.put(`http://localhost:3000/api/auth/${id}`, data, {
                    headers: {
                        Authorization: 'Bearer ' + localStorage.getItem('token')
                    }
                })
            .then((res) => {
                this.uersname = res.data.username,
                this.email = res.data.email,
                window.location.reload();
            })
            .catch((err) => {
                console.log(err)
            });
            }
        },

        deleteUser() {
            const id = localStorage.getItem('userId')
            if (confirm('Êtes-vous sur de vouloir supprimer votre compte ?')) {
                this.axios.delete(`http://localhost:3000/api/auth/${id}`, {
                    headers: {
                        Authorization: 'Bearer ' + localStorage.getItem('token')
                    }
                })
                .then(() => {
                    alert('Votre compte est supprimé !');
                    localStorage.clear()
                    this.$router.push('/');
                })
                .catch((err) => {
                    console.log(err)
                })
            }
        }
    },
}
</script>

<style lang="scss" scoped>
main {
  padding: 1.8em;
  @media screen and (max-width: 450px) {
      padding: 20px 0;   
  }
  #hello {
    display: flex;
    text-align: center;
    justify-content: center;
    background: white;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    font-size: 18px;
    @media screen and (max-width: 450px) {
        font-size: 15px;     
    }
  }
  #container {
    display: flex;
    justify-content: center;

    &__profil {
        display: flex;
        flex-direction: column;
        align-items: center;
        box-shadow: 1px 1px 6px grey;
        border-radius: 8px;
        width: 50%;   
        padding: 15px;
        margin: 20px 10px;
        background: linear-gradient(rgb(78, 79, 80) 25%, rgb(194, 200, 205));
        @media screen and (max-width: 770px) {
            width: 80%;
        }
        @media screen and (max-width: 450px) {
            width: 100%;
        }
        .avatar {
            border-radius: 50%;
            width: 260px;
            height: 260px;
            object-fit: cover;
            padding: 10px;
            border: 1px dotted rgb(130, 166, 238);
            color: white;
            @media screen and (max-width: 550px) {
                width: 200px;
                height: 200px;
            }
        }
        #file {
            display: none;
        }
        #label {
            cursor: pointer;
            border-style: groove;
            border-radius: 8px;
            padding: 8px;
            background: rgb(114, 114, 178);
            margin: 10px;
            font-weight: bold;
            font-size: 14px;
            color: #f2f5f9;
            &:hover {
                box-shadow: 2px 3px 4px rgb(22, 23, 23);
                transition: all 0.3s;
            }
        }
    }

    &__form {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 15px;
        margin: 10px;
        width: 80%;
        gap: 10px;
        background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
        border-radius: 5px;
        @media screen and (max-width: 500px) {
            width: 100%;
        }
        h2 {
            display: flex;
            justify-content: center;
            width: 90%;
            font-size: 18px;
            font-weight: bold;
            color: white;
            text-shadow: 2px 2px 4px black;
        }
        #form {
            display: flex;
            flex-direction: column;
            padding: 0px 10px;
            width: 90%;
            gap: 5px;
            @media screen and (max-width: 500px) {
                width: 100%;
            }
            label {
               font-size: 14px;
               color: rgb(255, 255, 255);
               text-shadow: 1px 2px 2px black;
            }
            input {
                outline: none;
                border: none;
                padding: 7px;
                border-radius: 8px;
                margin-bottom: 8px;
                color: #064198;
                background-color: rgb(231, 239, 250);
            }
            #error {
                display: flex;
                justify-content: center;
                font-size: 12px;
            }
        }
        #button {
            display: flex;
            justify-content: space-between;
            width: 90%;
            @media screen and (max-width: 500px) {
                width: 100%;
            }   
            button {
            border-style: groove;
            border-radius: 8px;
            padding: 8px;
            background: rgb(114, 114, 178);
            margin: 10px;
            font-weight: bold;
            font-size: 14px;
            color: #f2f5f9;
                &:hover {
                    box-shadow: 2px 3px 4px rgb(37, 37, 37);
                    transition: all 0.2s;
                }
            }
        }
    }
  }
}

</style>