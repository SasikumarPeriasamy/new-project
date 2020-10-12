<script>
import { h } from "vue";
import FeedEditSetup from "./FeedEditSetup.vue";
export default {
  name: "render-feed",
  props: {
    user: String,
  },
  data: () => ({
    editFeeds: false,
    contents: [
      "Hi friends....",
      "I am in India now.....",
      "I am currently working in Infoview....",
      "I am moving to vaken :-P.....",
      "Have a nice day friends....",
    ],
  }),
  components: {
    FeedEditSetup,
  },
  render() {
    const feeds = [];
    if (!this.editFeeds) {
      feeds.push(h("span", { class: "header" }, "Hi " + this.user + "!"));
      feeds.push(h("br"));
      feeds.push(h("br"));
      feeds.push(h("span", { id: "feeds-header" }, "Your feeds:"));
      feeds.push(h("br"));
      feeds.push(h("br"));
      const feedCount = 5;
      for (let index = 0; index < feedCount; index++) {
        feeds.push(
          h(
            "span",
            { id: "feeds-header" },
            h("strong", "F" + (index + 1) + ": ")
          )
        );
        feeds.push(h("span", { id: "feeds" }, this.contents[index]));
        feeds.push(h("br"));
      }
      feeds.push(h("br"));
      feeds.push(
        h(
          "button",
          {
            attr: { id: "edit" },
            onClick: this.editFeedAll,
            style: [
              { float: "left" },
              { "margin-top": "8px" },
              { "border-radius": "4px" },
              { width: "75px" },
              { height: "30px" },
              { "background-color": "darkgrey" },
            ],
          },
          "Edit"
        )
      );
      return h(
        "div",
        { class: "divhead", style: "text-align: left; margin-right: 27px;" },
        feeds
      );
    } else {
      feeds.push(
        h(FeedEditSetup, {
          contents: this.contents,
          onEditedvalues: this.changeContent,
        })
      );
      feeds.push(h("br"));
      return h(
        "div",
        { class: "divhead", style: "text-align: left; margin-right: 27px;" },
        feeds
      );
    }
  },
  methods: {
    editFeedAll() {
      this.editFeeds = true;
    },
    done() {
      this.editFeeds = false;
    },
    changeContent(update) {
      update.forEach((value) => {
        this.contents[Number(value.id)] = value.value;
      });
      this.done();
    },
  },
};
</script>

<style>
#divhead {
  margin-right: 20px;
}

#feeds {
  font-size: 15px;
  font-family: Arial, Helvetica, sans-serif;
}
#feeds-header {
  font-size: 15px;
  font-family: Arial, Helvetica, sans-serif;
}

.header {
  font-style: bold;
  text-align: left;
  margin-top: 10%;
  font-size: 20px;
  font-family: Arial, Helvetica, sans-serif;
}
#edit {
  margin-top: 16px;
  float: left;
}
</style>
