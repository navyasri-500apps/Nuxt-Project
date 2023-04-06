<template>
  <!-- Add email template  -->
  <div class="col-span-4 bg-white" v-if="appName == 'emailTemplate'">
    <div class="bg-gray-50 mx-auto px-5 py-3">
      <div class="text-center mb-0 rounded-0">
        <div>
          <input
            type="text"
            name="template-name"
            id="template-name"
            autocomplete="given-name"
            class="block w-full rounded-md border-0 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 px-4"
            placeholder="Enter template name"
            v-model="selectedForm.name"
          />
        </div>
      </div>
    </div>
  </div>

  <div class="row-span-2 col-span-4 bg-white" v-if="appName == 'emailTemplate'">
    <div class="mx-4 my-3">
      <input
        type="text"
        name="first-name"
        id="first-name"
        autocomplete="given-name"
        class="block w-full rounded-md border-0 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 px-4"
        placeholder="Enter subject"
        v-model="selectedForm.subject"
      />
    </div>

    <div class="mx-4 h-[78%]">
      <textarea
        v-model="selectedForm.body"
        rows="4"
        name="comment"
        id="comment"
        class="p-4 h-[100%] block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
      />
    </div>

    <div class="flex justify-end mr-3 mt-4">
      <button
        type="button"
        class="border rounded-md bg-white py-2 px-3 text-sm font-semibold text-gray-600 shadow-sm hover:bg-gray-50 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mr-3"
        @click="$emit('save', 'cancel')"
      >
        Cancel
      </button>

      <button
        type="button"
        class="rounded-md bg-indigo-600 py-2 px-4 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        @click="saveEmailData"
      >
        Save
      </button>
    </div>
  </div>
  <!-- Add email template  -->

  <!-- Add website modal  -->
  <div v-if="appName == 'website'">
    <TransitionRoot as="template" :show="showModal">
      <Dialog as="div" class="relative z-10" @close="showModal = false">
        <TransitionChild
          as="template"
          enter="ease-out duration-300"
          enter-from="opacity-0"
          enter-to="opacity-100"
          leave="ease-in duration-200"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <div
            class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
          />
        </TransitionChild>

        <div class="fixed inset-0 z-10 overflow-y-auto">
          <div
            class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
          >
            <TransitionChild
              as="template"
              enter="ease-out duration-300"
              enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
              enter-to="opacity-100 translate-y-0 sm:scale-100"
              leave="ease-in duration-200"
              leave-from="opacity-100 translate-y-0 sm:scale-100"
              leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            >
              <DialogPanel
                class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:w-full sm:max-w-lg"
              >
                <div class="flex items-center p-4 pb-0">
                  <DialogTitle
                    as="h3"
                    class="text-base font-semibold leading-6 text-gray-900"
                    >{{ selectedForm.name ? "Edit" : "Add" }}
                    {{ appName }}</DialogTitle
                  >
                  <div class="absolute right-0 hidden pr-4 sm:block">
                    <button
                      type="button"
                      class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-0 focus:ring-indigo-500 focus:ring-offset-0"
                      @click="showModal = false"
                    >
                      <span class="sr-only">Close</span>
                      <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                    </button>
                  </div>
                </div>

                <div class="items-end p-5">
                  <div class="grow mr-3">
                    <span>Website Name</span>
                    <input
                      type="text"
                      id="website_name"
                      name="website_name"
                      autocomplete="given-name"
                      placeholder="Enter Website Name"
                      class="block w-full rounded-md border-0 px-3 py-2.5 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-1 focus:ring-inset focus:ring-gray-300 sm:text-sm sm:leading-6"
                      v-model="selectedForm.name"
                    />
                  </div>

                  <div class="grow mr-3 my-5">
                    <span>Website URl</span>
                    <input
                      type="text"
                      id="website_url"
                      name="website_url"
                      autocomplete="given-name"
                      placeholder="Enter Website URL"
                      class="block w-full rounded-md border-0 px-3 py-2.5 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-1 focus:ring-inset focus:ring-gray-300 sm:text-sm sm:leading-6"
                      v-model="selectedForm.url"
                    />
                  </div>
                  <div class="flex justify-end">
                    <button
                      type="button"
                      class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-4 py-3 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 sm:w-auto"
                      @click="saveEmailData()"
                    >
                      Save
                    </button>
                  </div>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </div>
  <!-- Add website modal  -->
</template>

<script setup lang="ts">
import { ref, defineEmits, defineProps } from "vue";
import { XMarkIcon } from "@heroicons/vue/24/outline";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
const props = defineProps({
  selectedForm: Object,
  appName: String,
  showModal: Boolean,
});

const emit = defineEmits(["save"]);

const saveEmailData = () => {
  // Prepare form data to insert or update
  let data =
    props.appName == "website"
      ? {
          name: props.selectedForm.name,
          url: props.selectedForm.url,
        }
      : {
          project_id: "1",
          name: props.selectedForm.name,
          subject: props.selectedForm.subject,
          body: props.selectedForm.body,
          is_active: "1",
          type: "PLAIN_TEXT",
          share_type: "PRIVATE",
          category: "category1",
        };
  if (props.selectedForm && props.selectedForm.uid)
    data["uid"] = props.selectedForm.uid;

  // Emits data to insert or update data
  emit("save", data);
};
</script>

<style scoped></style>
