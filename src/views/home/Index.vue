<template>
	<div class="home">
		<!-- header -->
		<Header />
		<!-- end header -->
		
		<!-- slider -->
		<Slider />
		<!-- end slider -->
		
	<!-- main content -->
	<div class="container-fluid mt-3 mb-5">
		<div class="row">
		<div class="col-md-8">
		<div class="row">
			<!-- berita section -->
				<div class="col-md-12 mb-3">
					<h4><i class="fas fa-book-open"></i> NOTICIAS NOVAS</h4>
				</div>
				
				<div v-if="posts.length > 0" class="row">
					<div class="col-md-4 mb-4" v-for="post in posts" :key="post.id">
						<div class="card h-100 shadow-sm border-0 rounded-lg">
							<div class="card-img"><img :src="post.image" class="w-100" style="height: 200px; object-fit: cover;border-top-left-radius:.3rem; border-top-right-radius:.3rem;">
							</div>
							
							<div class="card-body">
								<router-link :to="{name:'detail_post', params: {slug: post.slug}}" class="text-dark text-decoration-none">
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
			<!-- end berita section -->
		
		<!-- foto section -->
		<div class="col-md-12 mb-3 mt-4">
			<h4><i class="fas fa-images"></i> FOTO NOVA</h4>
		</div>
			<div v-if="photos.length > 0" class="row">
				<div class="col-md-6 mb-4" v-for="photo in photos" :key="photo.id"><div class="card h-100 shadow-sm border-0 rounded-lg">
					<div class="card-img">
						<img :src="photo.image" class="w-100" style="height: 200px; object-fit: cover; border-top-left-radius: .3rem; border-top-right-radius:.3rem;">
					</div>
					<div class="card-body text-center">
						<h6>{{ photo.caption }}</h6>
					</div>
					</div>
				</div>
			</div>
			
			<div v-else>
				<div class="row">
					<div class="col-md-6 mb-3" v-for="loader in photos_loader" :key="loader">
						<div class="card border-0 shadow-sm rounded-lg">
							<div class="card-body p-2">
								<ContentLoader />
							</div>
						</div>
					</div>
				</div>
			</div>
		<!-- end foto section -->
		
		<!-- video section -->
			<div class="col-md-12 mb-3 mt-4">
				<h4><i class="fas fa-video"></i> VIDEO NEWS</h4>
			</div>
			
			<div v-if="videos.length > 0" class="row">
				<div class="col-md-6 mb-4" v-for="video in videos" :key="video.id">
					<div class="card h-100 shadow-sm border-0 rounded-lg">
							<div class="card-img">
								<iframe
								style="width:100%; height:200px; border-top-left-radius:.3rem; border-top-right-radius:.3rem"
								:src="video.embed"
								frameborder="0"
								allow="accelerometer;
								autoplay; encrypted-media; gyroscope; picture-in-picture"
								allowfullscreen></iframe>
							</div>
							<div class="card-body text-center">
								<h6>{{ video.title }}</h6>
							</div>
					</div>
				</div>
			</div>
			
			<div v-else>
				<div class="row">
					<div class="col-md-6 mb-3" v-for="loader in videos_loader" :key="loader">
						<div class="card border-0 shadow-sm rounded-lg">
							<div class="card-body p-2">
								<ContentLoader />
							</div>
						</div>
					</div>
				</div>
			</div>
		<!-- end video section -->
		</div>
		</div>
		
	<div class="col-md-4">
	<!-- agenda section -->
		<div class="title mb-4">
			<h4><i class="fa fa-calendar" ariahidden="true"></i> AGENDA NOVA</h4>
		</div>
	<div v-if="events.length > 0">
	<router-link :to="{name: 'detail_event',
	params:{slug: event.slug}}" v-for="event in events"
	:key="event.id" class="text-decoration-none
	text-dark">
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
				<div v-for="loader in events_loader" :key="loader">
					<div class="card border-0 shadow-sm rounded-lg mb-3">
						<div class="card-body pt-4">
							<FacebookLoader />
						</div>
					</div>
				</div>
			</div>
		</div>
	<!-- end agenda section -->
	
	<!-- kategori section -->
		<div class="title mb-4 mt-5">
			<h4><i class="fa fa-folder" ariahidden="true"></i> CATEGORIA NOTICIA</h4>
		</div>
		
		<div v-if="categories.length > 0">
			<div class="list-group">
			<router-link :to="{name: 'detail_category',
			params:{slug: category.slug}}"
			class="list-group-item list-group-item-action border-0 shadow-sm mb-2 rounded"
			v-for="category in categories"
			:key="category.id"><i class="fa fa-folder-open" aria-hidden="true"></i> {{
			category.name.toUpperCase() }}</router-link>
			</div>
		</div>
		
		<div v-else>
			<div class="row">
				<div v-for="loader in categories_loader" :key="loader">
					<div class="card border-0 shadow-sm rounded-lg mb-3">
						<div class="card-body pt-4">
							<BulletListLoader />
						</div>
					</div>
				</div>
			</div>
		</div>
	<!-- end kategori section -->
	
	</div>
	</div>
	</div>
	<!-- end main content -->
	
		<!-- footer -->
		<Footer />
		<!-- end footer -->
	</div>
</template>


<script>
	//import content loader
	import {
		ContentLoader,
		FacebookLoader,
		BulletListLoader,
	} from 'vue-content-loader'
	
	//import axios
	import axios from 'axios'
	
	//import component
	import Header from "@/components/Header"
	import Slider from "@/components/Slider"
	import Footer from "@/components/Footer"
	
	export default {
		name: 'home',
		components: {
			
			//loader component
			ContentLoader,
			FacebookLoader,
			BulletListLoader,
			
			//component app
			Header,
			Slider,
			Footer
		},
	data() {
		return {
			//define properties
			posts: [],
			events: [],
			categories: [],
			photos: [],
			videos: [],
			
			//define content loader data
			posts_loader: 3,
			events_loader: 2,
			categories_loader: 1,
			photos_loader: 2,
			videos_loader: 2
		}
	},
	
	created() {
			
			//get post homepage
			axios.get('/api/homepage/post').then(response => {
			this.posts = response.data.data
			})
			
			//get event homepage
			axios.get('/api/homepage/event').then(response => {
			this.events = response.data.data
			})
			
			//get categories
			axios.get('/api/category').then(response => {
			this.categories = response.data.data.data
			})
			
			//get photos
			axios.get('/api/homepage/photo').then(response => {this.photos = response.data.data
			})
			
			//get videos
			axios.get('/api/homepage/video').then(response => {
			this.videos = response.data.data
			})
		}
	}
</script>