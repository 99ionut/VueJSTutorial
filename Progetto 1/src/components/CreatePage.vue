<template>
  <div class="container mb-3">
    <form action="">
      <div class="col">
        <div class="mb-3">
          <label for="" class="form-label"> Page Title </label>
          <input type="text" class="form-control" v-model="pageTitle" />
        </div>
        <div class="mb-3">
          <label for="" class="form-label"> content </label>
          <textarea
            type="text"
            class="form-control"
            rows="5"
            v-model="content"
          ></textarea>
        </div>
      </div>
      <div class="col">
        <div class="mb-3">
          <label for="" class="form-label"> Link Text </label>
          <input type="text" class="form-control" v-model="linkText" />
        </div>
        <div class="mb-3">
          <label for="" class="form-label"> Link URL </label>
          <input type="text" class="form-control" v-model="linkUrl" />
        </div>
        <div class="mb-3">
          <div class="form-check">
            <input for="" class="form-check-input" type="checkbox" v-model="published" />
            <label for="gridCheck1" class="form-check-label">Published</label>
          </div>
        </div>
      </div>

      <div class="mb-3">
        <button
          class="btn btn-primary"
          @click.prevent="submitForm"
          :disabled="isFormInvalid"
        >
          Create Page
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
    emits: {
        pageCreated(pageObject){
            if(!pageObject.pageTitle){
                console.log("log eventtt");
                return false;
            }
        }
    },
  props: ["pageCreated"],
  data() {
    return {
      pageTitle: "",
      content: "",
      linkText: "",
      linkUrl: "",
      published: true,
    };
  },
  computed: {
    isFormInvalid() {
      return !this.pageTitle || !this.content || !this.linkText || !this.linkUrl;
    },
  },
  methods: {
    submitForm() {
      if (!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) {
        alert("fill the form");
        return;
      }

      this.$emit("pageCreated", {
        pageTitle: this.pageTitle,
        content: this.content,
        link: { text: this.linkText, url: this.linkUrl },
        published: this.published,
      });


      this.pageTitle = "";
      this.content = "";
      this.linkText = "";
      this.linkUrl = "";
      this.published = "";
    },
  },
  watch: {
    pageTitle(newTitle, oldTitle) {
      if (this.linkText === oldTitle) {
        this.linkText = newTitle;
      }
    },
  },
};
</script>
