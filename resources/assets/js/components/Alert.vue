<template>
    <div class="Alert Alert--{{ type | capitalize }}"
            v-show="show"
            transition="fade"
            @click="show = false"
            >
        <slot></slot>

        <span class="Alert__close" v-if="important">x</span>
    </div>


</template>

<script>
    export default {

        props: {
            type: { default: 'info' },
            timeout: { default: 3000 },
            important: {
                type: Boolean,
                default: false
            }
        },

        data() {
            return { show: true }
        },

        ready() {
            if (! this.important) {
                setTimeout(
                    () =>  this.show = false,
                    this.timeout
                )
            }
        }
    }
</script>

<style>
    .Alert {
        position: relative;
        padding: 10px;
    }

    .Alert--Info {
        background: #e3e3e3;
    }

    .Alert--Success {
        background: green;
    }

    .Alert--Error {
        background: pink;
    }

    .Alert__close {
        position: absolute;
        top: 10px;
        right: 10px;
        cursor: pointer;
    }

    .fade-transition {
        transition: opacity 1s ease;
    }

    .fade-leave {
        opacity: 0;
    }

</style>
