<template>
  <!-- email template -->

  <div
    class="grid grid-rows-3 grid-flow-col grid-cols-4 border w-[80vw] mx-auto my-5 rounded-lg pr-[4px]"
  >
    <!-- Add button -->
    <div
      class="row-span-3 bg-gray-50 border-r overflow-hidden p-5 shadow rounded-l-lg"
    >
      <div class="pb-3 w-[100%]">
        <button
          type="submit"
          class="bg-white hover:bg-gray-50 hover:text-gray-800 border focus-visible:outline focus-visible:outline-2 focus-visible:outline-indigo-600 focus-visible:outline-offset-2 font-semibold inline-flex items-center justify-center px-3 py-3 rounded-md shadow-sm text-gray-600 text-sm w-[100%]"
          @click="showAddModal()"
        >
          Add {{ lableName }}
        </button>
      </div>
      <!-- Add button -->

      <CollectionsList
        :emailTemplates="emailTemplates"
        :appName="appName"
        @editTemplate="edit"
        @deleteRecord="deleteRecord"
      />
    </div>

    <!-- Add component -->
    <CollectionsAdd
      :showModal="showModal"
      @save="addWebsite"
      :selectedForm="selectedForm"
      :appName="appName"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, defineProps } from "vue";

const props = defineProps({
  Heading: String,
  appName: String,
  url: String,
  serverUrl: String,
  lableName: String,
});
const currentIndex = ref(0);

const selectedForm = ref({
  name: "",
  subject: "",
  body: "",
});

// Get email templates or websites
const { pending, data: emailTemplates } = await useAuthLazyFetch(
  `${props.url}`
);

const showModal = ref(false);

// Insert or update records
const addWebsite = async (data: Object, type: String) => {
  if (type == "cancel") {
    selectedForm.value = {
      name: "",
      subject: "",
      body: "",
    };
    return;
  }

  // Set options data
  let options = {
    method: `${data.uid} ? 'PUT' :'POST'`,
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
      Authorization:
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzljMGM3MjkzMWI0NGZjOWE1NTc5ZWMyOTg4NzVlYzMiLCJkIjoiMTY4MDA2MiIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNjczNzl9.3_zIDyeZ0ACxOF0VpywmxGpzdhUadzmvMRggb106s5E",
    },
    body: JSON.stringify(data),
  };

  const { data: addTemplateData } = data.uid
    ? await useAuthLazyFetchPut(`${props.serverUrl}${data.uid}`, options)
    : await useAuthLazyFetchPost(`${props.serverUrl}`, options);

  // Unshift record into an array to display data in templates
  data.uid
    ? (emailTemplates.value[`${currentIndex.value}`] = data)
    : emailTemplates.value.unshift(addTemplateData._rawValue);

  // Set form data to empty
  selectedForm.value = {
    name: "",
    subject: "",
    body: "",
  };
  showModal.value = false;
};

// Edit email templates or website
const edit = (form: Object, index: Number) => {
  showModal.value = props.appName == "website" ? true : false;
  selectedForm.value = { ...form };
  currentIndex.value = index;
};

// Delete record
const deleteRecord = async (data: Object, index: Number) => {
  await useAuthLazyFetchDelete(`${props.serverUrl}${data.uid}`);
  emailTemplates.value.splice(index, 1);
};

// Display website add modal
const showAddModal = () => {
  if (props.appName == "website") {
    showModal.value = true;
    selectedForm.value = {
      name: "",
      subject: "",
      body: "",
    };
  } else
    selectedForm.value = {
      name: "",
      url: "",
    };
};
</script>
