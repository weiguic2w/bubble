<template>
  <div>
    <div v-if="seeTag" class="editor" spellcheck="false">
      <editor-content :editor="editor" />
    </div>
    <svg
      @click="seeTag = !seeTag"
      class="icon"
      viewBox="0 0 1024 1024"
      width="25"
      height="25"
    >
      <path
        d="M810.666667 128H213.333333a85.333333 85.333333 0 0 0-85.333333 85.333333v597.333334a85.333333 85.333333 0 0 0 85.333333 85.333333h341.333334l341.333333-341.333333V213.333333a85.333333 85.333333 0 0 0-85.333333-85.333333z m-298.666667 682.666667v-298.666667h298.666667l-298.666667 298.666667z"
      ></path>
    </svg>
  </div>
</template>

<script>
import { Color } from "@tiptap/extension-color";
import ListItem from "@tiptap/extension-list-item";
import TextStyle from "@tiptap/extension-text-style";
import StarterKit from "@tiptap/starter-kit";
import { Editor, EditorContent } from "@tiptap/vue-2";
import { openDatabase, saveContent, getContent } from "../util/dbHelper";

export default {
  components: {
    EditorContent,
  },

  data() {
    return {
      seeTag: false,
      editor: null,
      content: "",
      dbName: "MyDatabase",
      storeName: "MyStore",
    };
  },

  async mounted() {
    const db = await openDatabase(this.dbName, this.storeName);
    const key = this.$route.fullPath;
    const storedContent = await getContent(db, this.storeName, key);

    this.editor = new Editor({
      extensions: [
        Color.configure({ types: [TextStyle.name, ListItem.name] }),
        TextStyle.configure({ types: [ListItem.name] }),
        StarterKit,
      ],
      content: storedContent || "",
    });

    this.editor.on("update", async ({ editor }) => {
      this.content = editor.getHTML();
      await saveContent(db, this.storeName, this.content, key);
    });
  },

  beforeUnmount() {
    this.editor.destroy();
  },
};
</script>

<style>
.editor {
  position: fixed;
  right: 1rem;
  top: 50%;
}
.tiptap:first-child {
  width: 70rem;
  max-width: 70rem;
  height: 35rem;
  max-height: 35rem;
  padding: 1.5rem;
  font-size: 1.6rem;
  overflow-y: auto;
  overflow-wrap: break-word;

  outline: none;
  border-color: none;
  box-shadow: 0 0 0 1px var(--bg-300);
  border-radius: 1rem;
  background: var(--bg-200);
}

ul li {
  list-style: circle;
}
.tiptap ul,
.tiptap ol {
  padding: 0 1rem;
  margin-left: 1rem;
}

/* Heading styles */
.tiptap h1,
.tiptap h2,
.tiptap h3,
.tiptap h4,
.tiptap h5,
.tiptap h6 {
  line-height: 1.1;
  margin-top: 0;
}

.tiptap h1,
.tiptap h2 {
  margin: 1rem 0;
}

.tiptap h1 {
  font-size: 2rem;
}

.tiptap h2 {
  font-size: 1.8rem;
}

/* Code and preformatted text styles */
.tiptap code {
  background-color: var(--primary-330);
  border-radius: 0.4rem;
  color: var(--bg-300);
  font-size: 0.85rem;
  padding: 0.25em 0.3em;
}

.tiptap pre {
  background: var(--bg-300);
  border-radius: 0.5rem;
  color: var(--text-200);
  font-family: "JetBrainsMono", monospace;
  margin: 1.5rem 0;
  padding: 0.75rem 1rem;
}

.tiptap pre code {
  background: none;
  color: inherit;
  font-size: 0.8rem;
  padding: 0;
}

.tiptap blockquote {
  border-left: 3px solid var(--bg-300);
  margin: 1.5rem 0;
  padding-left: 1rem;
}

.tiptap hr {
  border: none;
  border-top: 1px solid var(--bg-300);
  margin: 2rem 0;
}

.icon {
  position: fixed;
  right: 1rem;
  top: 50%;
  cursor: pointer;
  border-radius: 1rem;
  background: var(--text-100);
  fill: var(--bg-200);
  padding: 0.2rem;
  transition: 200ms;
}
.icon:hover {
  fill: var(--text-100);
  background: var(--bg-200);
}
</style>
