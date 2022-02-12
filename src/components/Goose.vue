<template>
    <div style="height: 100px; display: flex; justify-content: center; align-items: center;">
        <span
        @mouseover="hover = true"
        @mouseleave="hover = false">
        <img alt="Goose image" :src="sprite" style="transform: scale(0.5);" /> 
        </span>
        <span v-if="hover">
        <h3> {{ name }} </h3>
        <table>
        <tbody>
        <tr>
        <td>&nbsp;Honk
            <b-progress :value="honk" :max=100 show-progress animated></b-progress>
        </td>
        </tr>
        <tr>
        <td>&nbsp;Wingspan
            <b-progress :value="wingspan" :max=100 show-progress animated></b-progress>
        </td>
        </tr>
        <tr>
        <td>&nbsp;Neck Size
            <b-progress :value="neck" :max=100 show-progress animated></b-progress>
        </td>
        </tr>
        </tbody>
        </table>
        </span>
    </div>
</template>

<script lang="ts">

export default {
      data() {
    return {
      hover: false,
    };
  },
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