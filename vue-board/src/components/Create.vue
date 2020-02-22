<template>
  <div>
    <input v-model="writer" type="text" placeholder="글쓴이" />
    <input type="text" v-model="title" placeholder="제목" />
    <textarea type="text" v-model="content" placeholder="내용" />
    <button @click="index !== undefined ? update() : write()">{{index !== undefined? "수정" : "작성"}}</button>
  </div>
</template>

<script>
import data from "@/data";
export default {
  name: "Create",
  data() {
    var index = this.$route.params.contentId;
    return {
      data: data,
      index: index,
      writer: index !== undefined ? data[index].writer : "",
      title: index !== undefined ? data[index].title : "",
      content: index !== undefined ? data[index].content : ""
    };
  },
  methods: {
    wrtie() {
      this.data.push({
        writer: this.writer,
        title: this.title,
        content: this.content
      });
      this.$router.push({
        path: "/"
      });
    },
    update() {
      data[this.index].writer = this.writer;
      data[this.index].title = this.title;
      data[this.index].content = this.content;
      this.$router.push({
        name: "Detail",
        params: {
          contentId: this.index
        }
      });
    }
  }
};
</script>

<style>
</style>