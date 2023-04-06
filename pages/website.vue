<template>
  <div>
    <CollectionsMain
      appName="website"
      :url="useAppConfig().websiteGetURL"
      :serverUrl="useAppConfig().websiteServerURL"
      lableName="Website"
    />
  </div>
</template>

<script setup></script>

<style scoped></style>
