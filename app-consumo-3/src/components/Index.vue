<template>
    <div class="pt-5">
        <div v-if="edificios && edificios.length">
            <div class="card mb-3" v-for="edificio of edificios" v-bind:key="edificio.id">
                <div class="row no-gutters">
                    <div class="col-md-4">
                        <div class="card-body">
                            <h5 class="card-title">Nombre: {{ edificio.nombre }}</h5>
                            <h5 class="card-text">Dirección: {{ edificio.direccion }}</h5>
                            <h5 class="card-text">Ciudad: {{ edificio.ciudad }}</h5>
                            <h5 class="card-text">Tipo: {{ edificio.tipo }}</h5>
                            <br>
                            <router-link :to="{name: 'edit', params: { id: edificio.id }}" class="btn btn-sm btn-primary">Editar</router-link>
                            <button class="btn btn-danger btn-sm ml-1" v-on:click="deleteEdificio(edificio)">Eliminar</button>
                        </div>
                    </div>
                    <div class="col-md-8">
                        <div class="card-body">
                            <p class="card-text">Número de Cuartos: {{ edificio.cuartos }}</p>
                            <p class="card-text">Costo: {{ edificio.costo }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <p  v-if="edificios.length == 0"> Sin Edificios</p>
    </div>
</template>
<script>

import axios from 'axios';

export default {
    data() {
        return {
            edificios: []
        }
    },
    created() {
        this.all();
    },
    methods: {
        deleteEdificio: function(e) {
            if (confirm('Eliminar ' + e.nombre)) {
                axios.delete(e.url)
                    .then( response => {
                        this.all();
                    });
            }
        },
        all: function () {
            axios.get('http://127.0.0.1:8000/api/edificios/')
                .then( response => {
                    this.edificios = response.data
                });
        }
    },
}
</script>
