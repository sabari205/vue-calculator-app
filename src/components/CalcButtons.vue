<template>
    <div @click="onClick" :class="classes">
        {{ buttonValue }}
    </div>
</template>

<script>
    export default {
        name: 'CalcButton',
        props: {
            buttonValue: {
                type: String
            }
        },
        emits: ['onClick'],
        methods: {
            onClick() {
                this.$emit('onClick');
            }
        },
        data() {
            return {
                classList: [
                    "px-3", 
                    "text-center", 
                    "cursor-pointer", 
                    "rounded-xl",
                    "bg-gray-200",
                    "hover:shadow-lg",
                    "transition",
                    "duration-100",
                    "ease-in",
                    "transform",
                    "focus:scale-90"
                ]
            }
        },
        computed: {
            classes() {
                if (this.buttonValue === "0") {
                    return this.classList.join(" ") + " col-span-2 border-2 border-gray-400";
                } else if (this.buttonValue === "=") {
                    return this.classList.join(" ") + " bg-yellow-400";
                } else if (this.buttonValue === "AC" || this.buttonValue === "DEL") {
                    return this.classList.join(" ") + " bg-red-500";
                } else {
                    return this.classList.join(" ") + " border-2 border-gray-400";
                }
            }
        }
    }
</script>