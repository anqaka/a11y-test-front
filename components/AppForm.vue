<template>
  <form @submit.prevent>
    <CFormControl py="2">
      <c-form-label for="pages">Pages</c-form-label>
      <c-textarea
        required
        placeholder="Pages"
        id="pages"
        v-model="form.pages"
      />
      <c-form-helper-text>Divide pages with comma</c-form-helper-text>
    </CFormControl>
    <CFormControl py="2">
      <c-form-label for="title">Title</c-form-label>
      <c-input placeholder="Title" id="title" v-model="form.title" />
    </CFormControl>
    <CFormControl py="2">
      <c-form-label for="fileName">Filename</c-form-label>
      <c-input placeholder="Filename" id="fileName" v-model="form.fileName" />
    </CFormControl>
    <CFormControl py="2">
      <c-form-label for="resultsDir">Results dir</c-form-label>
      <c-input placeholder="Title" id="resultsDir" v-model="form.resultsDir" />
    </CFormControl>
    <CHeading as="h2" size="sm" pt="4">
      Axe config
    </CHeading>
    <CDivider />
    <CFormControl py="2">
      <c-form-label for="reporter">Reporter</c-form-label>
      <c-input
        placeholder="Reporter"
        id="reporter"
        v-model="form.axeConfig.reporter"
      />
    </CFormControl>
    <CHeading as="h2" size="sm" pt="4">
      Viewport
    </CHeading>
    <CDivider />
    <CFormControl py="2">
      <c-form-label for="width">Width (px)</c-form-label>
      <c-input
        type="number"
        placeholder="Width"
        id="width"
        v-model="form.viewport.width"
      />
    </CFormControl>
    <CFormControl py="2">
      <c-form-label for="height">Height (px)</c-form-label>
      <c-input
        type="number"
        placeholder="Height"
        id="height"
        v-model="form.viewport.height"
      />
    </CFormControl>
    <CHeading as="h2" size="sm" pt="4">
      Basic auth configuration
    </CHeading>
    <CDivider />
    <CFormControl py="2">
      <c-form-label for="username">Username</c-form-label>
      <c-input
        placeholder="Username"
        id="username"
        v-model="form.basicAuth.username"
      />
    </CFormControl>
    <CFormControl py="2">
      <c-form-label for="password">Password</c-form-label>
      <c-input
        type="password"
        placeholder="Password"
        id="password"
        v-model="form.basicAuth.password"
      />
    </CFormControl>
    <CButton @click="onSubmit">
      Send
    </CButton>
  </form>
</template>

<script>
import {
  CFormControl,
  CFormLabel,
  CInput,
  CTextarea,
  CFormHelperText,
  CDivider,
  CHeading,
  CButton
} from '@chakra-ui/vue'

export default {
  components: {
    CFormControl,
    CFormLabel,
    CFormHelperText,
    CTextarea,
    CInput,
    CDivider,
    CHeading,
    CButton
  },

  data() {
    return {
      form: {
        pages: [],
        title: '',
        fileName: '',
        resultsDir: '',
        basicAuth: {
          username: '',
          password: ''
        },
        axeConfig: {
          reporter: ''
        },
        viewport: {
          width: null,
          height: null
        }
      }
    };
  },

  methods: {
    onSubmit() {
      this.$emit('submit', this.form);
    }
  }
};
</script>
