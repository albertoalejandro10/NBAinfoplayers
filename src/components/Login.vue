<template>
    <form @submit.prevent="checkForm">

        <p v-if="errors.length">
            <b>Por favor, corrije los siguientes errores: </b>
            <ul>
                <li v-for="error in errors" :key="error"> {{ error }}</li>
            </ul>
        </p>
        <div class="form-group">
            <label for="">Usuario:</label>
            <input type="text" class="form-control" v-model="username" placeholder="Usuario" />
        </div>

        <div class="form-group">
            <label> Contraseña: </label>
            <input type="password" class="form-control" v-model="password" placeholder="Contraseña">
        </div>

        <label for="checkbox"> No se puede iniciar sesion si el usuario no acepta las politicas de privacidad </label>
        <input type="checkbox" class="form-check-label" v-model="checked">

        <button class="btn btn-primary btn-block" :disabled="!checked"><a class="text-warning" href="/Table">Ingresar</a></button>

    </form>
    
</template>

<script>

export default {
    name: 'Login',
    data() {
        return {
            errors: [],
            username: '',
            password: '',
            checked: false,
        }
    },
    methods: {
        checkForm:function(e) {
            this.errors = [];
            if(!this.username){
                this.errors.push("Usuario requerido");
            } else if(!this.validUser(this.username)){
                this.errors.push("Se requiere un usuario válido");
            }

            if(!this.password) {
                this.errors.push("Contraseña requerida");
            } else if(!this.validPassword(this.password)) {
                this.errors.push("Se requiere una contraseña válida");        
            }

            if(!this.errors.length) return true;
            e.preventDefault();
        },

        validUser:function(username) {
            if(this.username.length >= 3) {
                let re = /[^!@#$%^&*()0-9A-Z][a-z]/g;
                return re.test(username);
            }
        },

        validPassword:function(password) {
            if(this.password.length >= 3) {
                let re = /[^a-z]/g;
                return re.test(password);
            }
        },        
    }

}
</script>