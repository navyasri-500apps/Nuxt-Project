<template>
  <div>
    <CollectionsMain
      appName="emailTemplate"
      :url="useAppConfig().templateGetURL"
      :serverUrl="useAppConfig().servertemplateURL"
      lableName="Template"
    />
  </div>
</template>

<script setup></script>

<style scoped></style>
