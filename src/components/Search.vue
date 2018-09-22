<template>
	<div class="search">
		<!-- <i class="fas fa-search"></i> -->

		<input type="text" class="form-search"
			v-model="query"
			@keyup.prevent="buscar"
			placeholder="Escribi la pelicula que buscas">
	</div>
</template>

<script>
	export default{
		data(){
			return {
				query: ''
			}
		},
		watch:{ //escucha cuando hay una consulta
			query(){
				this.buscar();
			}
		},
		methods: {
			buscar(){ //crea el evento busqueda y le pasa el parámetro query
				this.$emit('busqueda', this.query)
			},

		}
	}
</script>

<style lang="scss">
	@import '~bootstrap/dist/css/bootstrap.css';
	@import '~bootstrap-vue/dist/bootstrap-vue.css';

	.search {
		padding:10px;
		transition: .5s;
	}

	input:focus {
    	outline: none;
		border-bottom: 3px solid #01d277;
		transition: .5s;
	}

	.form-search {
		transition: .5s;
		border:0px;
		padding: 10px 35px;
		width: 100%;
	}

</style>