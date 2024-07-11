<script setup>
import { ref, reactive, onMounted, computed } from "vue";
import { Splide, SplideSlide } from "@splidejs/vue-splide";
import "@splidejs/splide/dist/css/themes/splide-default.min.css";
import PrimaryButton from "@/Components/Web/WebRevamp/WebCommoncomponents/PrimaryButton.vue";
import SecondaryButton from "@/Components/Web/WebRevamp/WebCommoncomponents/SecondaryButton.vue";

const categories = [
    {
        name: "Information Technology",
        slides: [
            { id: 1, title: 'IT Course 1', subtitle: 'Learn programming' },
            { id: 2, title: 'IT Course 2', subtitle: 'Web development' },
            { id: 3, title: 'IT Course 3', subtitle: 'Data science' },
            { id: 4, title: 'IT Course 4', subtitle: 'Cloud computing' },
            { id: 5, title: 'IT Course 5', subtitle: 'Cybersecurity' },
            { id: 6, title: 'IT Course 6', subtitle: 'Artificial Intelligence' },
            { id: 7, title: 'IT Course 4', subtitle: 'Cloud computing' },
            { id: 8, title: 'IT Course 5', subtitle: 'Cybersecurity' },
            { id: 9, title: 'IT Course 6', subtitle: 'Artificial Intelligence' },
        ]
    },
    {
        name: "Business",
        slides: [
            { id: 1, title: 'Business Course 1', subtitle: 'Marketing basics' },
            { id: 2, title: 'Business Course 2', subtitle: 'Financial management' },
            { id: 3, title: 'Business Course 3', subtitle: 'Entrepreneurship' },
            { id: 4, title: 'Business Course 4', subtitle: 'Business strategy' },
        ]
    },
    {
        name: "Management",
        slides: [
            { id: 1, title: 'Management Course 1', subtitle: 'Leadership skills' },
            { id: 2, title: 'Management Course 2', subtitle: 'Project management' },
            { id: 3, title: 'Management Course 3', subtitle: 'Operations management' },
        ]
    },
    {
        name: "Administration",
        slides: [
            { id: 1, title: 'Admin Course 1', subtitle: 'Office administration' },
            { id: 2, title: 'Admin Course 2', subtitle: 'Business communication' },
            { id: 3, title: 'Admin Course 3', subtitle: 'Administrative procedures' },
        ]
    },
    {
        name: "Project Management",
        slides: [
            { id: 1, title: 'PM Course 1', subtitle: 'Project planning' },
            { id: 2, title: 'PM Course 2', subtitle: 'Risk management' },
            { id: 3, title: 'PM Course 3', subtitle: 'Agile methodologies' },
        ]
    },
    {
        name: "Hr & Leadership",
        slides: [
            { id: 1, title: 'HR Course 1', subtitle: 'Recruitment strategies' },
            { id: 2, title: 'HR Course 2', subtitle: 'Employee development' },
            { id: 3, title: 'Leadership Course 1', subtitle: 'Team management' },
        ]
    },
    {
        name: "Sales & Marketing",
        slides: [
            { id: 1, title: 'Sales Course 1', subtitle: 'Sales techniques' },
            { id: 2, title: 'Marketing Course 1', subtitle: 'Digital marketing' },
            { id: 3, title: 'Marketing Course 2', subtitle: 'Brand management' },
        ]
    },
    // ... Add more categories as needed
];

const categorySplideRef = ref(null);
const contentSplideRef = ref(null);

const state = reactive({
  hasStarted: false,
  isAtEnd: false,
  activeCategory: categories[0].name,
  progress: 0,
});

const handleCategoryClick = (categoryName) => {
  state.activeCategory = categoryName;
  if (contentSplideRef.value) {
    contentSplideRef.value.go(0);
  }
};

const prevSlide = () => {
  if (categorySplideRef.value) {
    categorySplideRef.value.go("-1");
  }
};

const nextSlide = () => {
  if (categorySplideRef.value) {
    categorySplideRef.value.go("+1");
    state.hasStarted = true;
  }
};

const categorySplideOptions = {
  type: "slide",
  autoWidth: true,
  autoplay: false,
  focus: "left",
  trimSpace: true,
  arrows: false,
  pagination: false,
  gap: "1rem",
  perMove: 1,
  interval: 3000,
  autoScroll: {
    speed: 1,
    pauseOnHover: true,
    pauseOnFocus: false,
  },
};

onMounted(() => {
  const splide = categorySplideRef.value?.splide;
  if (splide) {
    const updateButtons = () => {
      const currentIndex = splide.index;
      const totalSlides = splide.length - splide.options.perPage;
      state.isAtEnd = currentIndex >= totalSlides;
      state.hasStarted = currentIndex > 0;
    };
    splide.on("moved", updateButtons);
    updateButtons();
  }
});

const initialCardCount = ref(6);
const expanded = ref(false);
const sectionRef = ref(null);

const updateInitialCardCount = () => {
    initialCardCount.value = window.innerWidth <= 991 ? 2 : 6;
};

onMounted(() => {
    updateInitialCardCount();
    window.addEventListener('resize', updateInitialCardCount);
});

const activeSlides = computed(() => {
  return categories.find((category) => category.name === state.activeCategory)?.slides || [];
});

const visibleSlides = computed(() => {
  return expanded.value ? activeSlides.value : activeSlides.value.slice(0, initialCardCount.value);
});

const showMoreButton = computed(() => {
  return activeSlides.value.length > initialCardCount.value;
});

function toggleExpand() {
    expanded.value = !expanded.value;
    if (!expanded.value) {
        scrollToSection();
    }
}

function scrollToSection() {
    if (sectionRef.value) {
        const offset = 100;
        const elementPosition = sectionRef.value.getBoundingClientRect().top;
        const offsetPosition = elementPosition + window.pageYOffset - offset;
        
        window.scrollTo({
            top: offsetPosition,
            behavior: "smooth"
        });
    }
}
</script>

<template>
    <section class="bg-ash-1000 py-20 md:py-32 coursecard-section" ref="sectionRef">
        <div class="container">
            <div class="">
                <h1 class="text-xl sm:text-4xl font-bold text-black-500 text-center xl:max-w-[34ch] mx-auto">Master Your Career Growth with Our Top-Rated, Expert-Led Courses</h1>
                <div class="mt-16 md:mt-25">
                    <div class="">
                        <div class="">
                            <div class="">
                                <div class="relative xl:w-3/4 mx-auto">
                                    <button v-if="state.hasStarted" class="prev absolute top-1/2 transform -translate-y-1/2 left-0 z-10" @click.stop="prevSlide">
                                        <i class="fas fa-chevron-left text-white bg-black-900 hover:text-black-900 hover:bg-white border border-black-900 rounded-10 w-[35px] h-[35px] flex justify-center items-center"></i>
                                    </button>
                                    <div class="mx-10 relative">
                                        <Splide :options="categorySplideOptions" ref="categorySplideRef">
                                            <SplideSlide v-for="(category, index) in categories" :key="index">
                                                <div class="my-3 lg:my-5 flex justify-center w-full">
                                                    <div :class="['text-base font-medium rounded-full w-full text-center py-2.5 px-5 border cursor-pointer text-nowrap overflow-hidden',
                                                        state.activeCategory === category.name
                                                            ? 'text-black-900 bg-green-200 border-indigo-200'
                                                            : 'text-black-900 bg-white border-indigo-200',
                                                        ]"
                                                        @click="handleCategoryClick(category.name)"
                                                    >
                                                        {{ category.name }}
                                                    </div>
                                                </div>
                                            </SplideSlide>
                                        </Splide>
                                    </div>
                                    <button v-if="!state.isAtEnd" class="next absolute top-1/2 transform -translate-y-1/2 right-0 z-10" @click.stop="nextSlide">
                                        <i class="fas fa-chevron-right text-white bg-black-900 hover:text-black-900 hover:bg-white border border-black-900 rounded-10 w-[35px] h-[35px] flex justify-center items-center"></i>
                                    </button>
                                </div>
                            </div>
                            <div class="col-span-1 lg:col-span-1 border-bottom"></div>
                        </div>
                        <!-- Content slider -->
                        <div class="">
                            <div class="">
                                <div class="py-10 px-4">
                                    <!-- pass the card data inside this and need to pass each category wise -->
                                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-3 gap-6 py-10">
                                        <transition-group name="card-list">
                                            <div v-for="slide in visibleSlides" :key="slide.id" class="flex justify-center">
                                                <div class="bg-white rounded-4 shadow-gel-shadow w-full p-4">
                                                    <div class="">
                                                        {{ slide.title }}
                                                    </div>
                                                    <div class="">
                                                        {{ slide.subtitle }}
                                                    </div>
                                                </div>
                                            </div>
                                        </transition-group>
                                    </div>
                                    <div class="mt-12 flex justify-center items-center gap-4">
                                        <PrimaryButton v-if="showMoreButton" @click="toggleExpand" class="whitespace-nowrap gap-3 flex items-center text-white font-bold py-2.5 px-4 border border-black-800 bg-black-800 rounded-2 text-lg">
                                            {{ expanded ? 'Show less' : 'Show more' }}
                                        </PrimaryButton>
                                        <SecondaryButton>
                                            View all
                                        </SecondaryButton>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
    .coursecard-section{
        -webkit-clip-path: polygon(0 0,100% 5.2vw,100% calc(100% - 3.2vw),0 100%);
        clip-path: polygon(0 0,100% 5.2vw,100% calc(100% - 3.2vw),0 100%);
    }

    .card-list-enter-active,
.card-list-leave-active {
    transition: opacity 0.5s ease, transform 0.5s ease;
}
.card-list-enter-from,
.card-list-leave-to {
    opacity: 0;
    transform: translateY(30px);
}
</style>
