<template>
    <div class="login">
        <div class="d-flex justify-content-center align-items-center login-div-base">
            <div class="d-flex flex-column col-xxl-4 col-lg-6 col-md-8 col-11">
                <h1 class="fs-2 mb-4">Leitor Excel</h1>
                <div class=" p-4 rounded-3 login-form-div">
                    <h2 class="fs-4 mb-5">Login</h2>
                    <form class="col-11 m-auto">
                        <div class="mb-4">
                            <label for="email" class="form-label">E-Mail</label>
                            <input type="email" class="form-control" id="email">
                        </div>
                        <div class="mb-5">
                            <label for="senha" class="form-label">Senha</label>
                            <input type="password" class="form-control" id="senha">
                        </div>
                        <button type="button" class="btn btn-success col-md-6 col-11" @click="login()">Entrar</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: "LoginView",
    methods: {
        login() {
            this.$router.push("/")
        }
    }
}
</script>
<style scoped>
label,
h2 {
    color: var(--primaria);
}

label {
    font-size: 18px;
}

h1 {
    color: rgb(223, 255, 233);
    font-size: 35px;
}

.login-div-base {
    background-color: var(--primaria);
    min-height: 100vh;
}

.login-form-div {
    background-color: rgba(255, 255, 255, 0.783);
    box-shadow: #FFFFFF 0px 0px 25px 0px;
}
</style>