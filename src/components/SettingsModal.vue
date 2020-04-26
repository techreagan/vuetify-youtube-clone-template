<template>
  <v-dialog
    v-model="dialog"
    persistent
    transition="fab-transition"
    max-width="800"
    id="settings"
  >
    <v-card tile>
      <div class="d-flex justify-space-between mb-5" id="modal-header">
        <v-card-title class="py-3">Settings</v-card-title>

        <v-btn icon text @click="closeModal">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </div>

      <v-card-text>
        <v-row>
          <v-col
            order="last"
            order-sm="last"
            order-md="first"
            order-lg="first"
            order-xl="first"
            cols="12"
            sm="12"
            md="8"
            lg="8"
            class="pt-0"
          >
            <!-- <v-card> -->
            <h3 class="mb-6 mt-0 pt-0">Personal Information</h3>
            <ValidationObserver ref="form" v-slot="{ handleSubmit, reset }">
              <form
                @submit.prevent="handleSubmit(submit)"
                @reset.prevent="reset"
              >
                <ValidationProvider
                  v-slot="{ errors }"
                  name="Channel Name"
                  rules="required|min:3"
                >
                  <v-text-field
                    v-model="formData.channelName"
                    :error-messages="errors"
                    label="Channel Name"
                    filled
                    dense
                  ></v-text-field>
                </ValidationProvider>
                <ValidationProvider
                  v-slot="{ errors }"
                  name="email"
                  rules="required|email"
                >
                  <v-text-field
                    v-model="formData.email"
                    :error-messages="errors"
                    label="Email"
                    filled
                    dense
                  ></v-text-field>
                </ValidationProvider>
                <!-- <div class="mt-3 d-flex justify-space-between"> -->
                <v-btn type="submit" class="primary " depressed>Submit</v-btn>
                <!-- </div> -->
              </form>
            </ValidationObserver>
            <!-- </v-card> -->
            <!-- <v-card> -->
            <h3 class="mb-6 mt-6">Change Password</h3>
            <ValidationObserver ref="form" v-slot="{ handleSubmit, reset }">
              <form
                @submit.prevent="handleSubmit(submit)"
                @reset.prevent="reset"
              >
                <ValidationProvider
                  v-slot="{ errors }"
                  name="Current Password"
                  rules="required|min:5"
                >
                  <v-text-field
                    v-model="formData.currentPassword"
                    :append-icon="
                      showCurrentPassword ? 'mdi-eye' : 'mdi-eye-off'
                    "
                    :error-messages="errors"
                    :type="showCurrentPassword ? 'text' : 'password'"
                    name="Current Password"
                    label="Current Password"
                    filled
                    dense
                    hint="At least 5 characters"
                    class="input-group--focused"
                    @click:append="showCurrentPassword = !showCurrentPassword"
                  ></v-text-field>
                </ValidationProvider>
                <ValidationProvider
                  v-slot="{ errors }"
                  name="New Password"
                  rules="required|min:5"
                >
                  <v-text-field
                    v-model="formData.newPassword"
                    :append-icon="showNewPassword ? 'mdi-eye' : 'mdi-eye-off'"
                    :error-messages="errors"
                    :type="showNewPassword ? 'text' : 'password'"
                    name="New Password"
                    label="New Password"
                    filled
                    dense
                    hint="At least 5 characters"
                    class="input-group--focused"
                    @click:append="showNewPassword = !showNewPassword"
                  ></v-text-field>
                </ValidationProvider>

                <!-- <div class="mt-6 d-flex justify-space-between"> -->
                <v-btn type="submit" class="primary" depressed>Submit</v-btn>
                <!-- </div> -->
              </form>
            </ValidationObserver>
            <!-- </v-card> -->
          </v-col>
          <v-col
            order-sm="1"
            cols="12"
            sm="12"
            md="4"
            lg="4"
            class="text-center"
          >
            <v-btn text @click="toggleShow">Upload Avatar</v-btn>
            <my-upload
              field="img"
              @crop-success="cropSuccess"
              v-model="show"
              :width="200"
              :height="200"
              :params="params"
              :headers="headers"
              img-format="jpg"
              langType="en"
            ></my-upload>
            <v-responsive
              width="230"
              class="mx-auto"
              style="border-radius: 50%;"
            >
              <div
                v-if="!imgDataUrl"
                class="px-12"
                id="settings-image-placeholder"
              >
                <v-icon>mdi-image-plus</v-icon>
              </div>
              <v-img v-else height="220" :src="imgDataUrl"></v-img>
            </v-responsive>
          </v-col>
        </v-row>
      </v-card-text>
      <!-- <v-card-actions v-if="!uploaded">
        <p class="text-center grey--text caption px-12 px-xs-0">
          By submitting your videos to YouTube, you acknowledge that you agree
          to YouTube's Terms of Service and Community Guidelines. Please be sure
          not to violate others' copyright or privacy rights. Learn more
        </p>
      </v-card-actions> -->
    </v-card>
  </v-dialog>
</template>

<script>
import myUpload from 'vue-image-crop-upload'
export default {
  name: 'SettingsModal',
  props: ['openDialog'],
  data: function() {
    return {
      // dialog: this.openDialog ? this.openDialog : false,
      showCurrentPassword: false,
      showNewPassword: false,
      valid: false,

      interval: {},
      value: 0,
      show: false,
      rules: [
        (value) =>
          !value ||
          value.size < 5000000 ||
          'Video size should be less than 5 MB!'
      ],
      categories: ['People', 'Technology', 'Fashion'],
      visibilty: ['Public', 'Private'],
      formData: {
        title: '',
        description: '',
        category: '',
        visibilty: ''
      },
      imgDataUrl: '',
      params: {
        token: '123456798',
        name: 'avatar'
      },
      headers: {
        smail: '*_~'
      }
    }
  },
  computed: {
    dialog() {
      return this.openDialog
    }
  },
  methods: {
    submit() {
      // if (this.$route.name === 'Dashboard')
      //   return this.$router.push('/studio/videos')
      console.log('submittied')
      this.closeModal()
    },
    closeModal() {
      this.$emit('closeDialog')
    },

    toggleShow() {
      this.show = !this.show
    },
    cropSuccess(imgDataUrl, field) {
      console.log('-------- crop success --------')
      console.log(field)
      this.imgDataUrl = imgDataUrl
    }
  },
  components: {
    myUpload
  }
}
</script>

<style lang="scss">
#modal-header {
  border-bottom: 1px solid rgb(238, 232, 232);
}

#settings-image-placeholder {
  padding-top: 7em;
  padding-bottom: 7em;
  border: 2px dashed rgb(209, 209, 209);
  border-radius: 50%;
}

@media (max-width: 700px) {
  .vue-image-crop-upload {
    .vicp-wrap {
      width: 95%;
      height: 550px;
      .vicp-step2 .vicp-crop {
        .vicp-crop-left {
          float: none;

          .vicp-range {
            margin: auto;
            margin-top: 30px;
          }

          & * {
            margin-left: auto;
            margin-right: auto;
          }
        }
        .vicp-crop-right {
          float: none;
          margin-top: 30px;
          .vicp-preview .vicp-preview-item {
            display: inline-block;
            float: none;
          }
          & * {
            // margin-left: auto;
            // margin-right: auto;
          }
        }
      }
    }
  }
}
</style>
