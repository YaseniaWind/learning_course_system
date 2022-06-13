<template>


     <Card :courses="newCourses"></Card>

     <div class="row mt-5">

    <div class="dropdown">
    <button class="btn btn-outline-danger btn-lg dropdown-toggle col-12" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
    Выберите категорию курсов
    </button>
    <ul class="dropdown-menu col-12 " aria-labelledby="dropdownMenuButton1">
    <li ><a class="dropdown-item" href="#" @click="fetchAllCourses()">Все категории</a></li>
    <li  v-for="category in categories" :key="category.id" @click="fetchCoursesOnCategory(category.id)"><a class="dropdown-item" href="#">{{category.title}}</a></li>
  </ul>
    </div>

    <Card :courses="courses" class="mt-5"></Card>

</div>





</template>

<script>
import Card from './welcome/components/Card.vue'
import axios from 'axios'
export default {
    components:{
        Card
    },
    data(){
        return{
            courses: [],
            newCourses : [],
            categories : []
        }
    },
      mounted() {
        this.fetchCourses();
        this.fetchAllCourses();
  },
  methods:{
    fetchCourses(){
            axios.get('/api/courses')
                .then((response) => {
                    console.log(response.data);
                     this.newCourses = response.data.all_courses;
                     this.categories = response.data.all_categories;

                })
                .catch((error) => {
                    console.log(error);
                });

        },
      fetchCoursesOnCategory(id){
        console.log('work')
            axios.get('api/category/' + id)
                .then((response) => {
                    console.log(response.data);
                     this.courses = response.data.courses;
                    //  this.categories = response.data.categories;

                })
                .catch((error) => {
                    console.log(error);
                });

        },
        fetchAllCourses(){
            axios.get('api/all_courses/')
                .then((response) => {
                    console.log(response.data);
                     this.courses = response.data;
                    //  this.categories = response.data.categories;

                })
                .catch((error) => {
                    console.log(error);
                });

        }
  },

}


</script>

<style>

</style>
