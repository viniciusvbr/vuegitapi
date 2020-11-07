<template>
<div v-if="success">
  <div
    class="card shadow-sm mb-3 rounded "
    style="margin-top: 2%; text-align:left"
    >
    <div
      class="card-header"
      v-bind:class="{
        'alert-warning': release.prerelease,
        'alert-success': index == 0,
      }"
    >
      <h5 class="card-title" style="margin-bottom:0px">
        <a
          v-bind:href="release.html_url"
          class="alert-link"
          style="color:inherit"
        >
          {{ release.tag_name }}</a
        >
        &nbsp;> &nbsp;
        <span class="text-muted h6">
          {{ release.total.toLocaleString() }} downloads
        </span>
      </h5>
    </div>

    <div class="card-body">
      <table class="table table-borderless table-sm">
        <thead>
          <tr>
            <th scope="col">Name</th>
            <th scope="col">Downloads</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(asset, index) in release.assets" :key="index">
            <th scope="row" class="asset">{{ asset.name }}</th>
            <td>{{ asset.download_count.toLocaleString() }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "Card",
  props: ["release", "index", "success"],
};
</script>

<style scoped>
.alert-warning {
  color: inherit;
}
.alert-success {
  color: inherit;
}
</style>
