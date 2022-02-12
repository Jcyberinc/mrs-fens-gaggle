<template>
    <div style=" height: 100px; display: flex; justify-content: center; align-items: center;`">
        <img alt="Goose image" src="../assets/goose.png" style="height: 100%; display: inline-block;" /> 
        <h3> {{ name }} </h3> <!-- the {{}} mean it is code, so it's plugging in the value of name --> 
    </div>
</template>

<script lang="ts">
export default {
    name: 'Goose',
    props: ['name']  // the brackets mean it's a list
    // a prop is a parameter that a component takes in
}
</script>