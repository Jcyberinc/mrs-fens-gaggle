<template>
    <div style="height: 100px; display: flex; justify-content: center; align-items: center;">
        <img alt="Goose image" src="../assets/goose.png" style="transform: scale(0.5);" /> 
        <h3> {{ name }} </h3>
        <h5> Honk </h5>
        <b-progress :value=honk :max=100 show-value class="mb-3"></b-progress>
    </div>
</template>

<script lang="ts">
export default {
props: {
    name: String,
    honk: Number,
    wingspan: Number,
    neck: Number
  }
}
</script>