<template>
    <div class="post-index">
        <!-- header -->
        <Header />
        <!-- end header -->

        <!-- main content -->
        <header class="pt-5 border-bottom bg-light">
            <div class="container pt-md-1 pb-md-1">
                <h1 class="bd-title mt-4 font-weight-bold"><i class="fa fa-bell" aria-hidden="true"></i> AGENDA</h1>
                <p class="bd-lead">{{ event.title }}</p>
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
                    <router-link :to="{ name: 'event' }" class="text-decoration-none"><i class="fa fa-bell"></i>
                        Agenda</router-link>
                </li>
                <li class="breadcrumb-item active" aria-current="page">{{ event.title }}</li>
            </ol>
        </nav>
        <!-- end breadcrumb -->

        <div class="container-fluid mt-5 mb-5">

            <div class="row">

                <div class="col-md-8">
                    <div v-if="event.title">
                        <div class="card border-0 shadow-sm rounded">
                            <div class="card-body">
                                <h3>{{ event.title }}</h3>
                                <hr>
                                <div class="table-responsive">
                                    <table class="table table-bordered table-striped">
                                        <tbody>
                                            <tr>
                                                <td style="width:20%">LOKASI</td>
                                                <td>
                                                    {{ event.location }}
                                                </td>
                                            </tr>
                                            <tr>
                                                <td>TANGGAL</td>
                                                <td>
                                                    {{ event.date }}
                                                </td>
                                            </tr>
                                        </tbody>
                                    </table>
                                    <div class="mt-3" v-html="event.content"> </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div v-else>
                        <div class="card border-0 shadow-sm rounded">
                            <div class="card-body">
                                <FacebookLoader/>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="col-md-4">

<!-- agenda section -->
                    <div class="title mb-4">
                        <h4><i class="fa fa-calendar" aria-hidden="true"></i> AGENDA TERBARU</h4>
                    </div>

                    <div v-if="events.length > 0">
                        <router-link :to="{name: 'detail_event', params:{slug: event.slug}}" v-for="event in events" :key="event.id" class="text-decoration-none text-dark">
                            <div class="card mb-3 shadow-sm border-0">
                                <div class="card-body">
                                    <h6>{{ event.title }}</h6>
                                    <hr>
                                    <div>
                                        <i class="fa fa-map-marker" aria-hidden="true"></i> {{ event.location }}
                                    </div>
                                    <div class="mt-2">
                                        <i class="fa fa-calendar" aria-hidden="true"></i> {{ event.date }}
                                    </div>
                                </div>
                            </div>
                        </router-link>
                    </div>

                    <div v-else>
                        <div class="row">
                            <div class="card border-0 shadow-sm rounded-lg mb-3" v-for="loader in events_loader"
                                :key="loader">
                                <div class="card-body pt-4">
                                    <FacebookLoader />
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- end agenda section -->

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
        name: 'EventShow',
        components: {
            //loader component
            FacebookLoader,
            //component app
            Header,
            Footer
        },
        data() {
            return {
                //define properties
                path: axios.defaults.baseURL,
                event: [],
                events: [],
                //define content loader data
                events_loader: 2,
            }
        },
        created() {

            //get detail event
            axios.get(`/api/event/${this.$route.params.slug}`).then(response => {
                this.event = response.data.data
            })

            //get event sidebar
            axios.get('/api/homepage/event').then(response => {
                this.events = response.data.data
            })

        }
    }
</script>