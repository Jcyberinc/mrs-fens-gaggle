<template>
  <div
    style="
      height: 100px;
      display: flex;
      justify-content: center;
      align-items: center;
    "
  >
    <span @mouseenter="hover = true" @mouseleave="hover = false">
      <h3>{{ status() }} {{ name }}</h3>
      <img alt="Goose image" :src="sprite" style="transform: scale(0.5)" />
    </span>
    <div class="statsandother">
      <span v-if="hover">
        <table>
          <tbody>
            <tr>
              <td>
                &nbsp;Honk
                <b-progress
                  :value="honk"
                  :max="100"
                  variant="info"
                  striped
                  animated
                ></b-progress>
              </td>
            </tr>
            <tr>
              <td>
                &nbsp;Wingspan
                <b-progress
                  :value="wingspan"
                  :max="100"
                  variant="info"
                  striped
                  animated
                ></b-progress>
              </td>
            </tr>
            <tr>
              <td>
                &nbsp;Neck Size
                <b-progress
                  :value="neck"
                  :max="100"
                  variant="info"
                  striped
                  animated
                ></b-progress>
              </td>
            </tr>
          </tbody>
        </table>
      </span>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      hover: false,
    };
  },
  methods: {
    status() {
      if (this.cute > 200 && this.cool > 200) {
        if (this.cute > this.cool) {
          return "Cute";
        } else {
          return "Cool";
        }
      } else if (this.cute > 200 && this.cool < 200) {
        return "Cute";
      } else if (this.cute < 200 && this.cool > 200) {
        return "Cool";
      } else {
        return "";
      }
    },
  },
  props: {
    name: String,
    honk: Number,
    wingspan: Number,
    neck: Number,
    cute: Number,
    cool: Number,
    sprite: String,
    fertile: {
      type: Boolean,
      default: true,
    },
  },
};
</script>