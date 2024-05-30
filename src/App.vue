<script setup>
import NumberAnimation from "vue-number-animation";

// Расчет количества поглаживаний пропорциональный 1:3 количеству проведенной единиц работы
import {computed, ref} from "vue";

const workUnits = ref(0)

const strokingUnits = computed(() => {
    return workUnits.value * 3
})

const animateCat = ref(true)
const result = ref(false)

function theFormat(number){
    return parseInt(number)
}

</script>

<template>
    <header>
        <div class="title">
            The Stroking Calc :3
        </div>
    </header>
    <main>
        <section class="calc">

            <transition-group name="bounce">
                <div v-if="!result" class="calc__item">
                    <div class="calc__item-img">
                        <img src="/src/assets/work.png" alt="working">
                    </div>
                    <div class="calc__item-input">
                        <button @click="workUnits--">
                            <i class="ri-arrow-down-s-line"></i>
                        </button>
                        <span>{{ workUnits }}</span>
                        <button @click="workUnits++">
                            <i class="ri-arrow-up-s-line"></i>
                        </button>
                    </div>
                    <div class="calc__item-title">
                        unit of work
                    </div>

                    <footer class="calc__footer">
                        <button class="calc__btn"
                            @click="result = true">
                            calc stroking
                            <i class="ri-hand"></i>
                        </button>
                    </footer>
                </div>

                <div v-else class="calc__item">

                    <div class="calc__item-img">
                        <img :src="`/src/assets/cat.${animateCat ? 'gif' : 'png'}`" alt="stroking">
                    </div>
                    <div class="calc__item-input">
                        <span class="w-100">
                            <NumberAnimation
                                ref="number1"
                                :from="0"
                                :to="strokingUnits"
                                :format="theFormat"
                                :duration="3"
                                autoplay
                                easing="linear"
                            />
                        </span>
                    </div>
                    <div class="calc__item-title">
                        stroking
                    </div>

                    <footer class="calc__footer">
                        <button class="calc__btn back"
                            @click="result = false">
                            <i class="ri-rewind-fill"></i>
                            back
                        </button>
                    </footer>
                </div>
            </transition-group>

        </section>
    </main>
</template>

