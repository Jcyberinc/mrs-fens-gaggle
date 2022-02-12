<template>
    <div style=" height: 100px; display: flex; justify-content: center; align-items: center;`">
        <img alt="Goose image" src="../assets/goose.png" style="height: 100%; display: inline-block;" /> 
        <h3> {{ name }} </h3>
    </div>
</template>

<script lang="ts">
export default {
    name: 'Goose',
    props: ['name']
}
</script>