<template>
  <div class="hello">
    <button
      @click="openCamera = !openCamera"
      :style="openCamera ? 'margin-bottom: 12px' : ''"
    >
      On/Off Camera
    </button>
    <StreamBarcodeReader
      style="margin-bottom: 12px"
      v-if="openCamera"
      @decode="(a, b, c) => onDecode(a, b, c)"
      @loaded="() => onLoaded()"
    ></StreamBarcodeReader>
    <h2>Input Value: {{ text || "Nothing" }}</h2>
  </div>
</template>

<script>
import { StreamBarcodeReader } from "vue-barcode-reader";
lllllll
export default {
  name: "HelloWorld",
  components: {
    StreamBarcodeReader,
  },
  data() {
    return {
      openCamera: false,
      text: "",
      id: null,
    };
  },
  methods: {
    onDecode(a, b, c) {
      console.log(a, b, c);
      this.text = a;
      if (this.id) clearTimeout(this.id);
      this.id = setTimeout(() => {
        if (this.text === a) {
          this.text = "";
        }
      }, 5000);
    },
    onLoaded() {
      console.log("load");
    },
  },
};
</script>
<style scoped>
.hello {
  max-width: 768px;
  margin: auto;
}
</style>
