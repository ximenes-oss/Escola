<template>
    <div class="post-index">
        <!-- header -->
        <Header />
        <!-- end header -->

        <!-- main content -->
        <header class="pt-5 border-bottom bg-light">
            <div class="container pt-md-1 pb-md-1">
                <h1 class="bd-title mt-4 font-weight-bold"><i class="fa fa-book-open" aria-hidden="true"></i> NOTICIA
                </h1>
                <p class="bd-lead">Noticia Nova Sobre EBG Timor-Leste.</p>
            </div>
        </header>

        <!-- breadcrumb -->
        <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
                <li class="breadcrumb-item">
                    <router-link :to="{ name: 'home' }" class="text-decoration-none"><i class="fa fa-home"></i> Home
                    </router-link>
                </li>
                <li class="breadcrumb-item">
                    <router-link :to="{ name: 'post' }" class="text-decoration-none"><i class="fa fa-book-open"></i>
                        Noticia</router-link>
                </li>
            </ol>
        </nav>
        <!-- end breadcrumb -->

        <div class="container-fluid mt-5 mb-5">

            <div class="row">

                <div v-if="posts.length > 0" class="row">
                    <div class="col-md-4 mb-4" v-for="post in posts" :key="post.id">
                        <div class="card h-100 shadow-sm border-0 rounded-lg">
                            <div class="card-img">
                                <img :src="post.image" class="w-100"
                                    style="height: 200px;object-fit: cover;border-top-left-radius: .3rem;border-top-right-radius: .3rem;">
                            </div>
                            <div class="card-body">
                                <router-link :to="{name: 'detail_post', params: {slug: post.slug}}"
                                    class="text-dark text-decoration-none">
                                    <h6>{{ post.title }}</h6>
                                </router-link>
                            </div>
                            <div class="card-footer bg-white">
                                <i class="fa fa-calendar" aria-hidden="true"></i> {{ post.created_at }}
                            </div>
                        </div>
                    </div>
                </div>

                <div v-else>
                    <div class="row">
                        <div class="col-md-4 mb-3" v-for="loader in posts_loader" :key="loader">
                            <div class="card border-0 shadow-sm rounded-lg">
                                <div class="card-body">
                                    <FacebookLoader />
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="text-center" v-show="moreExists">
                    <button type="button" class="btn btn-primary btn-md" v-on:click="loadMore"><span class="fa fa-arrow-down"></span> LIHAT LEBIH BANYAK</button>
                </div>

            </div>
        </div>
        <!-- main content -->

        <!-- footer -->
        <Footer />
        <!-- end footer -->
    </div>
</template>

<script>
    //import content loader
    import {
        FacebookLoader
    } from 'vue-content-loader'

    //import axios
    import axios from 'axios'

    //import component
    import Header from "@/components/Header"
    import Footer from "@/components/Footer"

    export default {
        name: 'PostIndex',
        components: {
            //loader component
            FacebookLoader,
            // component app
            Header,
            Footer
        },
        data() {
            return {
                //define properties
                path: axios.defaults.baseURL,
                posts: [],
                //define content loader data
                posts_loader: 6,
                //pagination
                moreExists: false,
                nextPage: 0
            }
        },
        mounted() {
            this.getPosts()
        },
        methods: {
            getPosts() {
                axios.get('/api/post').then(response => {
                    this.posts = response.data.data.data
                    if (response.data.data.current_page < response.data.data.last_page) {
                        this.moreExists = true
                        this.nextPage = response.data.data.current_page + 1
                    } else {
                        this.moreExists = false
                    }
                }).catch(response => {
                    console.log(response)
                })
            },
            //load more function
            loadMore() {
                axios.get('/api/post?page='+this.nextPage).then(response => {
                  if (response.data.data.current_page < response.data.data.last_page) {
                        this.moreExists = true
                        this.nextPage = response.data.data.current_page + 1
                    } else {
                        this.moreExists = false
                    }
                    response.data.data.data.forEach(data => {
                        this.posts.push(data)
                    })
                }).catch(response => {
                    console.log(response)
                })
            }
        }
    }
</script>