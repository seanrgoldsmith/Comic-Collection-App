<template>
  <div class="trending-comics">
    <h3>Check out the currently trending comics:</h3>
    <div class="carousel-container">
      <vue-carousel :autoplay="true" :loop="true" :items-per-page="1" :autoplay-timeout="5000">
        <vue-carousel-slide v-for="(slide, index) in comicSlides" :key="index">
          <div class="comic-row">
            <div v-for="(comic, comicIndex) in slide" :key="comicIndex" class="comic-item">
              <router-link :to="{name: 'comic', params: {id: comic.id}}">
               <img :src="comic.image" :alt="'Comic ' + (comicIndex + 1)" />
              </router-link>
              <p>{{ comic.description }}</p>
            </div>
          </div>
        </vue-carousel-slide>
      </vue-carousel>
    </div>
  </div>
</template>

<script>
import metronService from '../services/MetronService'
import { Carousel, Slide } from 'vue-carousel';

export default {
  name: 'TrendingComics',
  components: {
    VueCarousel: Carousel,
    VueCarouselSlide: Slide,
  },
  data() {
    return {
      // comics: [],
      comics: [
        {
          image: 'comic0.jpg',
          description: 'The Avengers (1963)',
          id: 17900,
        },
        {
          image: 'comic1.jpg',
          description: 'Power Girl Special (2023)',
          id: 64474
        },
        {
          image: 'comic2.jpg',
          description: 'Star Wars (1977)',
          id: 0,
        },
        {
          image: 'comic3.jpg',
          description: 'Strange Tales (1951)',
          id: 23784,
        },
        {
          image: 'comic4.jpg',
          description: 'The Amazing Spider-Man (1963)',
          id: 7460
        },
        {
          image: 'comic5.jpg',
          description: 'The Amazing Spider-Man (2022)',
        },
        {
          image: 'comic6.jpg',
          description: 'Peter Parker: The Spectacular Spider-Man (1976)',
        },
        {
          image: 'comic7.jpg',
          description: 'The Uncanny X-Men (1978)',
          id: 17757,
        },
        {
          image: 'comic8.jpg',
          description: 'Gargoyles (2022)',
        },
        {
          image: 'comic9.jpg',
          description: 'Action Comics (1938)',
          id: 34837,
        },
        {
          image: 'comic10.jpg',
          description: 'The X-Men (1963)',
          id: 27711,
        },
        {
          image: 'comic11.jpg',
          description: 'Venom (2018) Add Comic Button',
          id: 31954,
        },
        {
          image: 'comic12.jpg',
          description: 'Something Is Killing The Children (2019)',
          id: 5235,
        },
        {
          image: 'comic13.jpg',
          description: 'Doctor Strange (1968)',
          id: 17638,
        },
        {
          image: 'comic14.jpg',
          description: 'Marvels Greatest Comics (1969)',
        },
        {
          image: 'comic15.jpg',
          description: 'Grimm Fairy Tales (2016)',
        },
       ],
     
    };
  },
 created() {
  
   metronService.getRandomComics().then(response => {

     if(response.status == 200) {
     for(let i=0; i < this.response.data.length; i++) {
        let comicObj = {
          image: this.comics[i].image,
          description: this.comics[i].name[0]
        }

        this.comics.push(comicObj);
     }

      console.log(this.comics)

     }
   }
   
   )

 },
 computed: {
    comicSlides() {
      const comicsPerSlide = 4;
      const slides = [];
      for (let i = 0; i < this.comics.length; i += comicsPerSlide) {
        slides.push(this.comics.slice(i, i + comicsPerSlide));
      }
      return slides;
    },
  },
};
</script>

<style scoped>
.trending-comics {
  text-align: center;
}

.carousel-container {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  max-width: 800px;
  margin: 0 auto;
}

.comic-row {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  margin-bottom: 10px;
  flex-wrap: wrap;
}

.comic-item {
  flex: 1 0 25%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 10px;
}

img {
  width: 200px;
  height: 300px;
  object-fit: cover;
  margin: 3px;
}

.comic-item p {
  margin-top: 10px;
  text-align: center;
}
</style>
