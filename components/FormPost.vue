<template>
  <div class="box column is-10 is-offset-1">
    <form>
      <input id="post-id" v-model="value.id" type="hidden" />
      <b-field label="Post">
        <b-input
          v-model="value.text"
          placeholder="Enter the question text"
          type="text"
          icon="tag"
          required
        />
      </b-field>
      <div class="columns">
        <b-field class="column" label="Start date">
          <b-datetimepicker
            v-model="value.created_at"
            icon="calendar-arrow-right"
            required
          />
        </b-field>
      </div>
      <b-field>
        <b-upload v-model="dropFiles" multiple drag-drop>
          <section class="section">
            <div class="content has-text-centered">
              <p>
                <b-icon icon="upload" size="is-large"> </b-icon>
              </p>
              <p>Drop your files here or click to upload</p>
            </div>
          </section>
        </b-upload>
      </b-field>

      <div class="tags">
        <span
          v-for="(file, index) in dropFiles"
          :key="index"
          class="tag is-primary"
        >
          {{ file.name }}
          <button
            class="delete is-small"
            type="button"
            @click="deleteDropFile(index)"
          ></button>
        </span>
      </div>

      <div>
        <b-button type="is-info" icon-left="check" @click="save">
          Save
        </b-button>
        <b-button type="is-dark" icon-left="redo" @click="reset">
          Cancel
        </b-button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
  methods: {
    save() {
      this.$emit('save', this.value)
    },
    reset() {
      this.$emit('reset')
    },
  },
}
</script>
