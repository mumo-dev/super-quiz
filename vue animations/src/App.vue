<template>
    <div class="container">
        <div class="row">
            <div class="col-sm-8 col-sm-offset-2">
                <h1>Animation</h1>
                <hr>
                <button class="btn btn-primary" @click="show=!show">Show Alert</button>
                <br><br>
                <select v-model="alertAnimation" class="form-control">
                    <option value="fade"> Fade</option>
                    <option value="slide"> Slide</option>
                </select>
                <br><br>
                <!--<transition :name="alertAnimation">
                    <div class="alert alert-info" v-if="show">
                        Some info
                    </div>
                </transition>

                <transition name="slide" type="animation">
                    <div class="alert alert-info" v-if="show">
                        Some info
                    </div>
                </transition>

                <transition
                       enter-active-class="animated bounce"
                       enter-leave-class="animated shake"
                      >
                    <div class="alert alert-info" v-if="show">
                        Some info here
                    </div>
                </transition>-->
                <!--
                                <transition :name="alertAnimation" mode="out-in">
                                    <div class="alert alert-info" v-if="show" key="info">
                                        This is some info
                                    </div>
                                    <div class="alert alert-warning" v-else key="warning">
                                        This is some warning
                                    </div>
                                </transition>
                                <hr>
                                <button class="btn btn-primary"
                                        @click="selectedComponent == 'app-danger-alert'? selectedComponent= 'app-success-alert'
                                :selectedComponent='app-danger-alert'">Toggle Component
                                </button>
                                <br><br>
                                <transition name="fade" mode="out-in">
                                    <component :is="selectedComponent"></component>
                                </transition>
                                -->
                <hr>
                <button class="btn btn-primary" @click="addItem">Add Item</button>
                <br><br>
                <ul class="list-group">
                    <transition-group name="slide">
                        <li class="list-group-item"
                            v-for="(number,index) in numbers"
                            @click="removeItem(index)"
                            style="cursor: pointer" :key="number">{{ number }}
                        </li>
                    </transition-group>
                </ul>
            </div>
        </div>

    </div>
</template>

<script>
    import DangerAlert from './DangerAlert.vue'
    import SuccessAlert from './SuccessAlert.vue'

    export default {
        components: {
            appDangerAlert: DangerAlert,
            appSuccessAlert: SuccessAlert
        },
        data() {
            return {
                show: true,
                alertAnimation: 'fade',
                selectedComponent: 'app-danger-alert',
                numbers: [1, 2, 3, 4, 5]
            }
        },
        methods: {
            addItem() {
                const pos = Math.floor(Math.random() * this.numbers.length);
                this.numbers.splice(pos, 0, this.numbers.length + 1);
            },
            removeItem(index) {
                this.numbers.splice(index, 1);
            }
        }
    }
</script>

<style>
    .fade-enter {
        opacity: 0;
    }

    .fade-enter-active {
        transition: opacity 1s;
    }

    .fade-leave {

    }

    .fade-leave-active {
        transition: opacity 1s;
        opacity: 0;
    }

    .slide-enter {
        opacity: 0;

    }

    .slide-enter-active {
        animation: slide-in 1s ease-out forwards;
        transition: opacity 1s;
    }

    .slide-leave {

    }

    .slide-leave-active {
        animation: slide-out 1s ease-out forwards;
        transition: opacity 3s;
        opacity: 0;
        position: absolute;
    }
    .slide-move{
        transition: transform 1s;
    }

    @keyframes slide-in {
        from {
            transform: translateY(20px);
        }
        to {
            transform: translateY(0);
        }

    }

    @keyframes slide-out {
        from {
            transform: translateY(0);
        }
        to {
            transform: translateY(20px);
        }

    }

</style>
