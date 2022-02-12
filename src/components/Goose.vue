<template>
    <div style="height: 100px; display: flex; justify-content: center; align-items: center;">
        <img alt="Goose image" src="../assets/goose.png" style="transform: scale(0.5);" /> 
<<<<<<< Updated upstream
        <h3> {{ name }} </h3> <!-- the {{}} mean it is code, so it's plugging in the value of name -->
        <div>
            <h5> Honk </h5>
=======
        <h3> {{ name }} </h3>
        <table>
        <tbody>
        <tr>
        <td>&nbsp;Honk
>>>>>>> Stashed changes
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