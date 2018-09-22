<template>
	<div class="nav-bar">
        <div class="row" >

            <!-- el logo de la página vuelve al inicio cuando le haces clic encima-->
            <div id="logo" class="col-md-3 text-left" style="margin-left: 25px;">
                <a class="active" @click="inicio()"> 
                TheMovie<span>DB</span>
                </a>
            </div>

            <div class="col-md-8 text-right" style="margin-right:25px;">
                <ul style="margin-top: 15px;">

                <li class="tab"><a class="active" @click="inicio()"><i class="fas fa-home"></i> Cartelera</a></li>
                <li class="tab"><a class="active" @click="recomendados()"><i class="far fa-plus-square"></i> Valorados</a></li>
                <li class="tab"><a class="active" @click="estrenos()"><i class="fas fa-calendar-alt"></i> Prox.Estrenos</a></li>
                <li class="tab"><a class="active" @click="populares()"><i class="fas fa-star"></i> Populares</a></li>
                </ul>
            </div>
        </div>
	</div>
</template>

<script>
    export default {
        name: 'navbar',
   
        methods:{ //se crean los eventos que van a desencadenar al navegar por la barra ($emit)
            inicio(){
                this.$emit('inicio')
            },

            recomendados(){
                this.$emit('recomendados')
            },

            estrenos(){
                this.$emit('estrenos')
            },

            populares(){
                this.$emit('populares')
            }
        }   
    }
	
</script>

<style lang="scss">
    @import '~bootstrap/dist/css/bootstrap.css';
    @import '~bootstrap-vue/dist/bootstrap-vue.css';
    
    router-link, li {
        color: #FFF;
        background-color: #000;
        padding: 8px 35px;
        margin-top: 4px;
        vertical-align: -webkit-baseline-middle;
        display: inline-block;
        transition: .5s;
    }

    router-link, li:hover{
        filter: invert(100);
    }

     li:hover{
        filter: invert(100);
    }

	.nav-bar {
        padding-top: 30px;
    }

    #logo {
        color: #FFF;
        font-weight: 500;
        font-size:3em;
    }

    #logo span {
        color: #01d277;
        font-weight: 700;
    }


</style>