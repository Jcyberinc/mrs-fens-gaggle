<template>
    <div style="height: 100px; display: flex; justify-content: center; align-items: center;">
        <img alt="Goose image" src="../assets/goose.png" style="transform: scale(0.5);" /> 
        <h3> {{ name }} </h3> <!-- the {{}} mean it is code, so it's plugging in the value of name -->
        <div>
            <h5> Honk </h5>
            <b-progress :value="honk" :max=100 show-progress animated></b-progress>
        </div>
        <br />
        <div>
            <h5> Wingspan </h5>
            <b-progress :value="wingspan" :max=100 show-progress animated></b-progress>
        </div>
        <br />
        <div>
            <h5> Neck Size </h5>
            <b-progress :value="neck" :max=100 show-progress animated></b-progress>
        </div>
    </div>    
</template>

<script lang="ts">
export default {
props: {
    name: String,
    honk: Number,
    wingspan: Number,
    neck: Number,
    cool: Number,
    cute: Number,
    sprite: String
  }
}
</script>