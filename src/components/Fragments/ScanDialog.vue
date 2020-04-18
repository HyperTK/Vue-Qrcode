<template>
  <div>
    <p class="error">{{ error }}</p>
    <v-text-field
      prepend-icon="mdi-qrcode"
      class="decode-result"
      label="QRコード"
      :value="result"
    ></v-text-field>
    <v-row>
      <v-col cols="1">
        <v-dialog v-model="isCamera" width="500">
          <template v-slot:activator="{ on }">
            <v-btn color="blue lighten-2" fab small dark v-on="on">
              <div>
                <v-icon>mdi-camera</v-icon>
              </div>
            </v-btn>
          </template>

          <v-card>
            <v-card-title class="headline grey lighten-2" primary-title>
              QR-SCAN
            </v-card-title>
            <qrcode-stream @decode="onDecode" @init="onInit" />
            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="isCamera = false">
                CLOSE
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      result: "",
      error: "",
      isCamera: false,
    };
  },
  methods: {
    onDecode(result) {
      this.result = result;
    },
    async onInit(promise) {
      try {
        await promise;
      } catch (error) {
        if (error.name === "NotAllowedError") {
          this.error = "ERROR: you need to grant camera access permisson";
        } else if (error.name === "NotFoundError") {
          this.error = "ERROR: no camera on this device";
        } else if (error.name === "NotSupportedError") {
          this.error = "ERROR: secure context required (HTTPS, localhost)";
        } else if (error.name === "NotReadableError") {
          this.error = "ERROR: is the camera already in use?";
        } else if (error.name === "OverconstrainedError") {
          this.error = "ERROR: installed cameras are not suitable";
        } else if (error.name === "StreamApiNotSupportedError") {
          this.error = "ERROR: Stream API is not supported in this browser";
        }
      }
    },
  },
};
</script>
