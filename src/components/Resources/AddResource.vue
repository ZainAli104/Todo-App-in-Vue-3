<template>
  <base-dialog v-if="showDialog" title="Input Invalide" @close="confirmError">
    <template #default>
        <p>Unfortunately, at least one input value is invalide.</p>
        <p>Please check all inputs and make sure you entered at least one character in each input.</p>
    </template>
    <template #action>
        <button @click="confirmError">ok</button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="addRes">
        <div class="form-control">
            <label for="title">Title</label>
            <input id="title" name="title" type="text" ref="titleInput" />
        </div>
        <div class="form-control">
            <label for="discription">Discription</label>
            <textarea name="discription" id="discription" rows="3" ref="discInput" />
        </div>
        <div class="form-control">
            <label for="link">Link</label>
            <input id="link" name="link" type="url" ref="linkInput" />
        </div>
        <base-button type="submit" @click="submitData">Add Resource</base-button>
    </form>
  </base-card>
</template>

<script>
export default {
    inject: ['addResource'],
    data() {
        return {
            showDialog: false,
        };
    },
    methods: {
        submitData() {
            const enteredTtile = this.$refs.titleInput.value;
            const enteredDiscription = this.$refs.discInput.value;
            const enteredLink = this.$refs.linkInput.value;

            if(enteredTtile.trim() === '' || enteredDiscription.trim() === '' || enteredLink.trim() === '') {
                this.showDialog = true;
                return;
            }
            this.addResource(enteredTtile, enteredDiscription, enteredLink);
        },
        confirmError() {
            this.showDialog = false;
        }
    }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>