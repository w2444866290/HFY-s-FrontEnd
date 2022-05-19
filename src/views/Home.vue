<template>
  <div class="vw-100 vh-100">
    <div style="height: 100px"></div>
    <div class="container">
      <div class="input-group mb-1">
        <input
          type="text"
          class="form-control p-2"
          aria-label="input"
          placeholder="填写专利信息..."
          aria-describedby="button-search"
        />
        <button
          class="btn btn-dark"
          type="button"
          id="button-search"
          style="width: 100px"
        >
          查询
        </button>
      </div>

      <div class="d-flex flex-row m-3 mb-5" v-if="keywords.length != 0">
        <span class="fw-light">关键词：</span>
        <div
          v-for="keyword in keywords"
          :key="keyword"
          class="badge bg-primary m-1"
        >
          {{ keyword }}
        </div>
      </div>

      <div v-if="files.length != 0">
        <div class="d-flex flex-row justify-content-center">
          <div class="btn-group m-3" role="IsActive" aria-label="IsActive">
            <input
              type="radio"
              class="btn-check"
              name="IsActive"
              id="activeDefault"
              autocomplete="off"
              checked
            />
            <label class="btn btn-outline-dark" for="activeDefault">默认</label>

            <input
              type="radio"
              class="btn-check"
              name="IsActive"
              id="active"
              autocomplete="off"
            />
            <label class="btn btn-outline-dark" for="active">现行</label>

            <input
              type="radio"
              class="btn-check"
              name="IsActive"
              id="abandon"
              autocomplete="off"
            />
            <label class="btn btn-outline-dark" for="abandon">废弃</label>
          </div>

          <div class="btn-group m-3" role="IsAbroad" aria-label="IsAbroad">
            <input
              type="radio"
              class="btn-check"
              name="IsAbroad"
              id="abroadDefault"
              autocomplete="off"
              checked
            />
            <label class="btn btn-outline-dark" for="abroadDefault">默认</label>

            <input
              type="radio"
              class="btn-check"
              name="IsAbroad"
              id="domestic"
              autocomplete="off"
            />
            <label class="btn btn-outline-dark" for="domestic">国内</label>

            <input
              type="radio"
              class="btn-check"
              name="IsAbroad"
              id="abroad"
              autocomplete="off"
            />
            <label class="btn btn-outline-dark" for="abroad">国外</label>
          </div>
        </div>

        <table class="table table-hover mt-3">
          <thead>
            <tr class="table-dark">
              <th scope="col">#</th>
              <th scope="col">摘要</th>
              <th scope="col">标准号</th>
              <th scope="col">地区</th>
              <th scope="col">发表年份</th>
              <th scope="col">状态</th>
            </tr>
          </thead>
          <tbody>
            <tr
              class="align-middle"
              v-for="(file, index) in files"
              :key="index"
              style="table-layout: fixed"
            >
              <th style="width: 80px" scope="row">{{ index + 1 }}</th>
              <td>{{ file.abstract }}</td>
              <td style="width: 200px">{{ file.standardNum }}</td>
              <td style="width: 100px">{{ file.area }}</td>
              <td style="width: 80px">{{ file.years }}</td>
              <td style="width: 80px">
                <span
                  class="badge bg-success text-wrap"
                  v-if="file.status == '现行'"
                  >{{ file.status }}</span
                >
                <span
                  class="badge bg-danger"
                  v-else-if="file.status == '作废'"
                  >{{ file.status }}</span
                >
                <span class="badge bg-secondary" v-else>{{ file.status }}</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";

@Options({})
export default class Home extends Vue {
  keywords: string[] = [];
  files: Record<string, string>[] = [];
  originFiles: Record<string, string>[] = [];

  // search(inputInfo: string): void {}
  // filterTrigger(): void {}
  // filterByStatus(): void {}
  // filterByAbroad(): void {}
}
</script>

<style>
html,
body {
  width: 100%;
  height: 100%;
}
</style>
