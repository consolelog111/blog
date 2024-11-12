
<template>
	<div class="overflow-x-hidden w-full cursor-crosshair mt-10">
		<div class="content w-full px-5 text-center pt-10">
			<h1 class="text-5xl font-bold uppercase mt-10 mb-4 flex items-center justify-center flex-col font-serif text-[#f2d680]">TAKE A LOOK :)
				<span class="flex gap-4 items-center mt-2 text-2xl ">
					<a href="https://github.com/kromate/vue3-gsap-animations" target="_blank" rel="noopener noreferrer" class=" transition-all duration-500 hover:text-[#171515]"><i class="lab la-github"></i></a>
					<a href="https://youtu.be/KJrymk0uKC4" target="_blank" rel="noopener noreferrer" class="transition-all duration-500 hover:text-[#e36868]"><i class="lab la-youtube "></i></a>
					<a href="https://twitter.com/kromate_24" target="_blank" rel="noopener noreferrer" class="transition-all duration-500 hover:text-[#1DA1F2]"><i class="lab la-twitter "></i></a>
				</span>
			</h1>

			<p class="mb-16 w-[40rem] max-w-[100%] mx-auto text-white">Some blog posts are written in Chinese, and I have translated them into English using ChatGPT  ---  Thank you, ChatGPT👍!</p>
			<div class="flex flex-wrap px-10 justify-center w-full mx-auto gap-y-12 pb-12">
				<router-link replace :to="n.link" class="card cardx" v-for="n in animationPageList" :key="n">
					<span class="absolute text-3xl font-bold num -top-5 -right-5 uppercase transition-all duration-500">Article - 0{{n.index}}</span>
					<span class="sub text-3xl font-bold card_text block text-white">{{n.title}}</span>
					<div class="explore text-white center font-bold text-4xl pt-10" >
						<span>View </span>
					</div>
				</router-link>
			</div>
		</div>
	</div>
</template>

<script setup lang="ts">
// import { fadeOut } from '@/assets/scripts/animation-scripts/landingPage'

const animationPageList=[
    {
        index:1,
        link:'/articles',
        desc:"This article primarily introduces the role of `defineComponent` in Vue 3. It provides a detailed explanation through example code, which can be a valuable reference for learning or work. Interested readers can refer to it for further insights.",
        title:'An in-depth explanation of the purpose of defineComponent in Vue 3.'
    },
    {
        index:2,
        link:'/animation2',
        title:'Compilation of Front-End Animation Libraries'
    },
    {
        index:3,
        link:'/animation3',
        desc:'3D Card Flip'
    }]

</script>

<style scoped lang="scss">


.cardx {
    @apply flex justify-center items-center hover:scale-105 mb-5  hover:border-2 border border-[#f9a825] relative rounded w-8/12 h-36 p-3 shadow text-xl card text-center transition-all duration-500;
}

.card:hover .num {
    top: -35px;
    color: #ff3d00; /* this is the fallback */
    -webkit-text-stroke: 1.5px #ff3d00;
    -webkit-text-fill-color: transparent;
}

.card .explore {
    position: absolute;
    background: #000;
    width: 1%;
    height: 1%;
    pointer-events: none;
    opacity: 0;
    transition: all;
    transition-duration: 500ms;
}
.card:hover .explore {
    position: absolute;
    opacity: 1;
    height: 100%;
    width: 100%;
    background: #f9a825;
}
.card:hover .card_text {
    opacity: 0;
}

.num {
    color: #fff; /* this is the fallback */
    -webkit-text-stroke: 1px #fff;
    -webkit-text-fill-color: transparent;
    transition: all;
    transition-duration: 500ms;
}


button {
    letter-spacing: 6px;
    color: #fff;
    text-transform: uppercase;
    outline: none;
    overflow: hidden;
    background: none;
    z-index: 1;
    cursor: crosshair;
    transition: 0.8s ease-out;
}

.myBtn:hover {
    color: #fff;
    cursor: pointer;
    border: 2px solid #fff;
}

.myBtn:before {
    content: '';
    position: absolute;
    background: #fff;
    bottom: 0;
    left: 0;
    right: 0;
    top: 100%;
    z-index: -1;
    transition: top 0.65s ease-out;
}

.myBtn:hover:before {
    top: 0;
}

</style>