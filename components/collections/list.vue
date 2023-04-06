<template>
  <div>
    <!-- Display email templates and websites -->
    <div
      v-for="(template, index) in emailTemplates"
      :key="index"
      class="border p-4 rounded-md mb-3 shadow-sm bg-white"
    >
      <div
        class="border-b border-gray-200 bg-white px-4 py-5 sm:px-6 group/item justify-between flex"
      >
        <h5 class="font-[500] text-md mb-2 flex items-center">
          <!-- icon for email templates -->
          <span v-if="appName == 'emailTemplate'">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              class="mr-2"
              viewBox="0 0 24 24"
            >
              <path
                fill="#888888"
                d="M11 11L3 6v10h10v2H3q-.825 0-1.413-.588T1 16V4q0-.825.588-1.413T3 2h16q.825 0 1.413.588T21 4v5h-2V6l-8 5Zm0-2l8-5H3l8 5Zm8 13q-1.65 0-2.825-1.175T15 18v-4.5q0-1.05.725-1.775T17.5 11q1.05 0 1.775.725T20 13.5V18h-2v-4.5q0-.2-.15-.35T17.5 13q-.2 0-.35.15t-.15.35V18q0 .825.588 1.413T19 20q.825 0 1.413-.588T21 18v-4h2v4q0 1.65-1.175 2.825T19 22ZM3 6V4v12V6Z"
              /></svg
          ></span>
          <!-- icon for email templates -->

          <!-- icon for websites -->
          <span v-else>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M12 21a9.004 9.004 0 008.716-6.747M12 21a9.004 9.004 0 01-8.716-6.747M12 21c2.485 0 4.5-4.03 4.5-9S14.485 3 12 3m0 18c-2.485 0-4.5-4.03-4.5-9S9.515 3 12 3m0 0a8.997 8.997 0 017.843 4.582M12 3a8.997 8.997 0 00-7.843 4.582m15.686 0A11.953 11.953 0 0112 10.5c-2.998 0-5.74-1.1-7.843-2.918m15.686 0A8.959 8.959 0 0121 12c0 .778-.099 1.533-.284 2.253m0 0A17.919 17.919 0 0112 16.5c-3.162 0-6.133-.815-8.716-2.247m0 0A9.015 9.015 0 013 12c0-1.605.42-3.113 1.157-4.418"
              /></svg
          ></span>
          <!-- icon for websites -->

          {{ template.name }}
        </h5>

        <div class="text-sm text-gray-600">
          <p v-if="appName == 'emailTemplate'">{{ template.subject }}</p>
          <p v-else>{{ template.url }}</p>
        </div>

        <div
          class="flex items-center text-gray-500 group-hover/item:visible invisible"
        >
          <PencilIcon
            class="h-[17px] cursor-pointer mr-[4px] pt-1"
            @click="$emit('editTemplate', template, index)"
          />
          <TrashIcon
            class="h-[17px] cursor-pointer mr-[4px] pt-1 tect-danger"
            @click="
              (showDeleteModal = true),
                (selectedTemplate = template),
                (currentIndex = index)
            "
          />
        </div>
      </div>
    </div>
    <!-- Display email templates and websites -->

    <!-- Delete confirmation modal -->
    <TransitionRoot as="template" :show="showDeleteModal">
      <Dialog as="div" class="relative z-10" @close="showDeleteModal = false">
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
                class="relative transform overflow-hidden rounded-lg bg-white px-4 pt-5 pb-4 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
              >
                <div>
                  <div
                    class="mx-auto flex h-12 w-12 items-center justify-center rounded-full bg-red-100"
                  >
                    <TrashIcon
                      class="h-6 w-6 text-red-600"
                      aria-hidden="true"
                    />
                  </div>
                  <div class="mt-3 text-center sm:mt-5">
                    <DialogTitle
                      as="h3"
                      class="text-base font-semibold leading-6 text-gray-900"
                      >Are you sure</DialogTitle
                    >
                    <div class="mt-2">
                      <p class="text-sm text-gray-500">
                        Are you sure you want to delete
                      </p>
                    </div>
                  </div>
                </div>
                <div
                  class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
                >
                  <button
                    type="button"
                    class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                    @click="
                      emit('deleteRecord', selectedTemplate, currentIndex),
                        (showDeleteModal = false)
                    "
                  >
                    Delete
                  </button>
                  <button
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                    @click="showDeleteModal = false"
                    ref="cancelButtonRef"
                  >
                    Cancel
                  </button>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
    <!-- Delete confirmation modal -->
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from "vue";
import { PencilIcon, TrashIcon } from "@heroicons/vue/24/outline";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
const props = defineProps({
  emailTemplates: Array,
  appName: String,
  lableName: String,
});
const emit = defineEmits(["deleteRecord"]);
const showDeleteModal = ref(false);
const selectedTemplate = ref({});
const currentIndex = ref(0);
</script>

<style scoped></style>
