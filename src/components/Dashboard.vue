<template>
    <div>
        <h2 class="text-xl-center">NBA Players Info</h2>
        <table class="table-sm table-striped table-bordered" border="1">
            <thead class="thead-primary">
                <tr>
                    <th>ID</th>
                    <th>Primer Nombre</th>
                    <th>Apellido</th>
                    <th>Altura Pulgadas</th>
                    <th>Altura Pies</th>
                    <th>Peso</th>
                    <th>Posicion</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="player in playerList" :key="player.id">
                    <td> {{ player.id }} </td>
                    <td> {{ player.first_name }} </td>
                    <td> {{ player.last_name}} </td>
                    <td> {{ player.height_inches }} </td>
                    <td> {{ player.height_feet }} </td>
                    <td> {{ player.weight_pounds }} </td>
                    <td> {{ player.position }} </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
// import axios from 'axios'

export default {
    name: 'Dashboard',
    data() {
        return {
            playerList: null,
            page: 1,
        }
    },
    mounted() {
    // console.log("Esto se carga automaticamente")

        fetch("https://free-nba.p.rapidapi.com/players?page=" + this.page, {
            headers: {
                "x-rapidapi-key": "665ed21c81msh061a123159a7203p1bb178jsn2ddffd2c7093"
            },
        })
        .then(res => res.json())
        .then(data => {
            this.playerList = data.data;
        })
    }
}

</script>

<style scoped>
    body, html, #app, #root, .auth-wrapper {
        width: 100%;
    }
</style>