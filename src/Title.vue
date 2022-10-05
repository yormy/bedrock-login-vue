<template>
    <div v-if="title" class="text-center mb-3">
        <h3>{{ title }}</h3>
        <p v-if="subtitle">{{ subtitle }}</p>
    </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
        },
        subtitle: {
            type: String,
        }
    }
}

</script>
