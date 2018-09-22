<template>
	<div class="row">
		 <!--  recorre el array de vectores y los va mostrando  -->
		<div class="col-md-4" v-for="movie in movies" :key="movie.id" style="margin-bottom:15px;">
			<div class="view overlay">
				<a :href="`https://www.themoviedb.org/movie/`+ movie.id" target="_blank">
					<img :src="apiImageBasePath+
						movie.poster_path"
						class="img-fluid"
						:alt="movie.title">
				</a>

				<div class="mask rgba-black-strong">
					<h5 class="white-text text-center" style="padding-top:20px;">{{ movie.title }}</h5>
					<p class="white-text text-center" style="padding:20px; font-size: 15px;">{{ movie.overview }}</p>
				</div>
			</div>
		</div>

	</div>
</template>

<script>
	export default{
		props: ['movies'],
		data(){
			return{
				apiImageBasePath: 'https://image.tmdb.org/t/p/w600_and_h900_bestv2'
			}
		}
	}
</script>

<style>
	.card-block {
		padding: 25px;
	}
</style>
