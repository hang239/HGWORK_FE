<template>
    <form v-on:submit.prevent="submitForm">
        <div class="main" :style="mainStyle">
            <h1>QUÊN MẬT KHẨU?</h1>
            <input class="login-input" type="text" name="username" id="username" placeholder="Tài khoản"
                v-model="form.username" :style="input" />
            <br />
            <input class="login-input" type="text" name="email" id="email" v-model="form.email"
                placeholder="Email" :style="input" />
            <br />
            <input type="submit" value="Lấy lại mật khẩu" class="button login-input" id="done" :style="inputStyle" />
            <br />
        </div>
    </form>
</template>
  
<script>
import axios from 'axios';
export default {
    name: "Login",
    //Custom style for main and input for make the page responsive:
    props: {
        mainStyle: String,
        inputStyle: String,
    },
    data() {
        return {
            notifications: {
                topCenter: false,
            },
            form: {
                username: '',
                email: ''
            }
        }
    },
    methods: {
        submitForm() {
            axios.post('http://localhost:8080/user/forgot', this.form)
                .then((res) => {
                    if (res.data.statusCode == 200) {
                        location.href = "http://localhost:8080/#/login";
                        // location.reload();
                    }
                    else {
                        this.notifyVue('top', 'right', 'Tài khoản hoặc email không tồn tại ')
                    }
                })
                .catch((error) => {
                    this.notifyVue('top', 'right', 'Tài khoản hoặc email không tồn tại')
                }).finally(() => {
                    //Perform action in always
                });
        },
        notifyVue(verticalAlign, horizontalAlign, dataMess) {
            this.$notify({
                message:
                    dataMess,
                icon: "add_alert",
                horizontalAlign: horizontalAlign,
                verticalAlign: verticalAlign,
                type: "danger",
            });
        },
    }
};
</script>
  
<style>
/* Import Poppins font: */
@import url("https://fonts.googleapis.com/css2?family=Poppins&display=swap");

.main {
    background: rgba(255, 255, 255, 0.4);
    position: absolute;
    top: 140%;
    left: 10%;
    width: 60%;
    text-align: center;
    padding: 5px;
    border-radius: 3rem;
    box-shadow: 0px 0px 8px -5px #000000;
    padding-top: 3%;
    padding-bottom: 5%;
    font-family: "Poppins", sans-serif;
}

h1 {
    cursor: default;
    user-select: none;
}

.login-input {
    border-radius: 3rem;
    border: none;
    padding: 10px;
    text-align: center;
    outline: none;
    margin: 10px;
    width: 30%;
    box-sizing: border-box;
    font-family: "Poppins", sans-serif;
    font-weight: 400;
}

.login-input:hover {
    box-shadow: 0px 0px 8px -5px #000000;
}

.login-input:active {
    box-shadow: 0px 0px 8px -5px #000000;
}

#done {
    background: lightgreen;
}

/* img {
    height: 2.2rem;
    margin: 10px;
    user-select: none;
}

img:hover {
    box-shadow: 0px 0px 8px -5px #000000;
    cursor: pointer;
    border-radius: 200rem;
} */
</style>