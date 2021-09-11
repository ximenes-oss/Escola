<template>
    <div class="post-index">
        <!-- header -->
        <Header />
        <!-- end header -->

        <!-- main content -->
        <header class="pt-5 border-bottom bg-light">
            <div class="container pt-md-1 pb-md-1">
                <h1 class="bd-title mt-4 font-weight-bold"><i class="fa fa-phone" aria-hidden="true"></i> KONTAK</h1>
                <p class="bd-lead">Kontak EBG Timor-Leste.</p>
            </div>
        </header>

        <!-- breadcrumb -->
        <nav aria-label="breadcrumb">
        <ol class="breadcrumb">
            <li class="breadcrumb-item"><router-link :to="{ name: 'home' }" class="text-decoration-none"><i class="fa fa-home"></i> Home</router-link></li>
            <li class="breadcrumb-item"><router-link :to="{ name: 'contact' }" class="text-decoration-none"><i class="fa fa-phone"></i> Kontak</router-link></li>
        </ol>
        </nav>
        <!-- end breadcrumb -->

        <div class="container-fluid mt-5 mb-5">

            <div class="row">
                <div class="col-md-7">
                    <div class="card border-0 shadow-sm rounded">
                        <div class="card-body">
                            <iframe src="https://www.google.com/maps/d/embed?mid=1gmkyYaoOZm672fIV1m1p8k_ZFSZ9vTjb" width="100%" height="400" frameborder="0" style="border:0;" allowfullscreen="" aria-hidden="false" tabindex="0"></iframe>
                        </div>
                    </div>
                </div>
                <div class="col-md-5">
                    <div class="card border-0 shadow-sm rounded">
                        <div class="card-body">
                            <h3>Contacto Nos</h3>
                            <hr>
                            <p>
                                <i class="fa fa-map-marker" aria-hidden="true"></i> DILI. Fatuhada-Marconi,Timor-Leste
                                <br>
                                <br>
                                <i class="fas fa-phone"></i> +670 77154409
                                <br>
                                <br>
                                <i class="fas fa-envelope"></i> ximenesmarco26@gmail.com
                            </p>
                        </div>
                    </div>
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
    //import component
    import Header from "@/components/Header"
    import Footer from "@/components/Footer"

    export default {
        name: 'ContactIndex',
        components: {
            Header,
            Footer
        }
    }
</script>