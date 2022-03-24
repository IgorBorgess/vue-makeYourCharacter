<template>
    <Banner v-bind:style="cssProps"/>
    <h1>Races</h1>
    <div id="races">
    <div>
    <Carousel 
        @next="next"
        @prev="prev">
            <CarouselSlide v-for="(slide, index) in slides" 
            v-bind:key="slide"
            v-bind:index="index"
            v-bind:visibleSlide="visibleSlide"
            v-bind:direction="direction">
            <img v-bind:src="slide" />
            </CarouselSlide >
        </Carousel >
    </div>
    <h3>
        Voices talk quickly in countless tongues. The scent of dozens of kitchens mix themselfs with the tumultuous streets and it's poor sanitation.
        Skyscrapers in a myriad of architectural styles exhibit the diverse origins of its inhabitants.
        And the residents themselfs - people of different sizes, shapes and colors, all dressed with a spectre of gorgeous styles and shades - 
        represents many distinct races, from the small halflings and the strong dwarfs, to the majestically beautiful
        elfs, all blending together with the great variety of human etnicy.
    </h3>
    <h3>
        Spread between the members of those common races lives the most exotic ones, such as the powerful dragonborn, making his way into the crowd,
        and the cunning tiefling, which lurks in the shadows with guile in his eyes. A group of gnomes laughs while one of them activates a wood toy
        that moves on its own. Half-elfs and half-orcs live and work side-by-side with humans, without themselfs belonging completely to any race of
        their parents. And, from there, in such distance from the sun, a solitary drow, a runaway from the deep extension of the underground. He tries to
        make a living in a world that fear his species.
    </h3>
    </div>

    <div id="classifications">
    <h1>Class</h1>
    <img src="/img/classifications2.jpg" alt="">
    <h3>
        Adventurous people are extraordinary, moved by the their yearning and excitement of a life that other dare not live themselfs.
        They are heros, compelled to explore the dark places of the world and to accept challenges that weaker men and women could not.
        Their class is what defines those heroes, and it's more than a profession, a calling, even. Those classifications modifies the way they
        view and interact with the world around them, such as their relationship with other people and so on.
    </h3>
    <h3>    
        A fighter, for instance, can see the world through pure strategic pragmatism or combat maneuvers, even seeing himself as a pawn in the whole scenario.
        A cleric, on the other hand, sees himself as a devout servant in the plans of an mighty god or in the conflict that involves such deities.
        Even the rogue has his place in this scenario, robbing people in order to survive while the bard can make a living by playing in the local tavern.
        The possibilities are truly endless.
    </h3>
    </div>
</template>

<script>
import Banner from "../components/Banner.vue";
import Carousel from "../components/Carousel/Carousel.vue"
import CarouselSlide from "../components/Carousel/CarouselSlide.vue"


export default {
    name: "Glossary",
    components: {
    Banner,
    Carousel,
    CarouselSlide
    },
    data() {
        return {
        cssProps: {
            backgroundImage: `url(${require("/public/img/cover.png")})`,
            },
            slides: [
                "../img/carousel1/races.jpg",
                "../img/carousel1/races2.png",
                "../img/carousel1/races3.jpg",
                "../img/carousel1/races4.jpg",
                "../img/carousel1/races5.jpg"
            ],
            visibleSlide: 0,
            direction: "left",
        }
    },
    computed: {
        slidesLen() {
            return this.slides.length
        }
    },
    methods: {
        next() {
            if(this.visibleSlide >= this.slidesLen - 1) {
                this.visibleSlide = 0
            } else {
                this.visibleSlide++
            }
            this.direction = "left"
        },
        prev() {
            if(this.visibleSlide <= 0) {
                this.visibleSlide = this.slidesLen - 1
            } else {
                this.visibleSlide--
            }
            this.direction = "right"
        }
    }
}
</script>

<style scoped>

    h3 {
        width: 600px;
        text-align: center;
        margin-bottom: 20px;
    }

    #summary,
    #races,
    #classifications {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    img {
        margin-bottom: 20px;
        width: 600px;
    } 

</style>