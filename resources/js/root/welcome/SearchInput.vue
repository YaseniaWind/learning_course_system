<template>

 <div class="d-flex " role="search">
    <input class="form-control " style="height:37px; margin-left: 50px;" v-model.trim="inputSearch" type="search" placeholder="Курс" aria-label="Search">


  <div class="dropdown dropabs">
  <button  class=" btn btn-danger dropdown-toggle"  @click.prevent="addSearch" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="mx-3" role="img" viewBox="0 0 24 24">
                            <title>Search</title>
                            <circle cx="10.5" cy="10.5" r="7.5"></circle>
                            <path d="M21 21l-5.2-5.2"></path>
                        </svg>
  </button>
  <div v-if="flags">
  <div v-if="!datasearch">

   Идет загрузка...

    </div>
      <div v-else>

          <div v-if="datasearch.length > 0">
               <a class="dropdown-item" v-for="datas in datasearch" :key="datas.id" :href="'/course/'+ datas.id" >
               {{datas.title}}
               </a>
          </div>
      </div>
  </div>

</div>

</div>





</template>

<script>
import axios from 'axios'

export default {
    data(){
        return{
            inputSearch: " ",
            datasearch: null,
            flags: null
        }
    },
    methods:{
        addSearch(){

            axios({
    method:'post',
    url:`/search`+ `?q=${this.inputSearch}`,
    baseURL: 'http://127.0.0.1:8000/',
    // data:  this.inputSearch
   },
)
            .then((response) => {
                // window.location.href = '/home/' + this.userId;
                this.flags = true;
                this.datasearch = response.data
                console.log(response);
            })
            .catch((error) => {
                console.error(error.response);
                if ( error.message ) {
                    console.log('ошибка')
                }
            });
        }
    }

}
</script>

<style>
.dropabs{
left: 61%;
    position: absolute;
}
@media (max-width: 769px) {
    .dropabs{
    left: 1%;
    position: static;
}
}
@media (max-width: 1230px) {
    .dropabs{
    left: 50%;
    position: absolute;
}
}
</style>
