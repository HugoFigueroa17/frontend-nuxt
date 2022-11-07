<template>
    <div class="vld-parent">
        <loading :active="isLoading" ></loading>
    </div>
</template>

<script>
    // Import component
    import Loading from 'vue-loading-overlay';
    // Import stylesheet
    import 'vue-loading-overlay/dist/vue-loading.css';
    
    export default {
        props:{
            isLoading:{
                type: Boolean,
                default: true
            }
        },
        data() {
            return {}
        },
        components: {
            Loading
        },
    }
</script>