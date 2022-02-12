<template>
    <div style="height: 100px; display: flex; justify-content: center; align-items: center;">
        <img alt="Goose image" src="../assets/goose.png" style="transform: scale(0.5);" /> 
        <h3> {{ name }} </h3>
        <table>
        <tbody>
        <tr>
        <td>&nbsp;Honk
        </td>
        </tr>
        <tr>
        <td>&nbsp;Wingspan
        </td>
        </tr>
        <tr>
        <td>&nbsp;Neck Size
        </td>
        </tr>
        </tbody>
        </table>
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