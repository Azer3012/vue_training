<template>
  <div class="container mb-3">
    <form action="">
      <div class="row">
        <div class="col-md-8">
          <div class="mb-3">
            <label for="" class="form-label"> Page Title </label>
            <input v-model="pageTitle" type="text" class="form-control" />
          </div>
          <div class="mb-3">
            <label for="" class="form-label"> Content </label>
            <textarea
              v-model="content"
              type="text"
              rows="5"
              class="form-control"
            ></textarea>
          </div>
        </div>
        <div class="col">
          <div class="mb-3">
            <label for="" class="form-label"> Link Text </label>
            <input v-model="linkText" type="text" class="form-control" />
          </div>
          <div class="mb-3">
            <label for="" class="form-label"> Link Url </label>
            <input v-model="linkUrl" type="text" class="form-control" />
          </div>
          <div class="row mb-3">
            <div class="form-check">
              <input type="checkbox" class="form-check-input" v-model="published" />
              <label for="gridCheck1" class="form-label"> Published </label>
            </div>
          </div>
        </div>
      </div>

      <div class="mb-3">
        <button :disabled="isFormInvalid" @click.prevent="submitForm" class="btn btn-primary">
          Create Page
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {

  emits:{
    pageCreated(pageTitle,content,link){
      if(!pageTitle){
        return false
      }
      if(!content){
        return false
      }
      if(!link.text || !link.url){
        return false
      }

      return true
    }
  },

  computed:{
    isFormInvalid(){
        return !this.pageTitle || !this.content || !this.linkText || !this.linkUrl
    }
  },
  data() {
    return {
      pageTitle: "",
      content: "",
      linkText: "",
      linkUrl: "",
      published:false
    };
  },
  methods: {
    submitForm() {
      if (!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) {
        alert("Please fill the form");
        return;
      }


      this.$emit('pageCreated',{
        pageTitle: this.pageTitle,
        content: this.content,
        link: {
          text: this.linkText,
          url: this.linkUrl,

        },
        published:this.published
      })
       
    },
  },
  watch:{
    pageTitle(newTitle,oldTitle){
      if(this.linkText===oldTitle){
        this.linkText=newTitle
      }
    }
  }
};
</script>


