<template>
  <div class="row">
    <div class="card offset-2 col-md-3">
      <div class="card-body tex-center d-flex align-items-center flex-column">
        <img height="128" class="img-responsive text-center mb-3"
             :src="product.selectedImage == null ? '/src/assets/default.png' : product.selectedImage">
        <input ref="file" type="file" style="display: none;" @change="onChange($event)" class="form-control">
        <button class="btn btn-outline-secondary " type="button" @click="$refs.file.click()">Resim Seç</button>
      </div>
    </div>
    <div class="col-md-5">
      <div class="col-md-11 card">
        <div class="card-body">
          <div class="form-group">
            <label>Ürün Adı</label>
            <input type="text" v-model="product.title" class="form-control" placeholder="Adını giriniz">
          </div>
          <div class="row">
            <div class="form-group col-md-6">
              <label>Ürün Adeti</label>
              <input type="number"  min="1" v-model="product.count" class="form-control" placeholder="Adetini giriniz">
            </div>
            <div class="form-group col-md-6">
              <label>Ürün Fiyatı</label>
              <input type="number" min="1" class="form-control" v-model="product.price" placeholder="Fiyatını giriniz">
            </div>
          </div>
          <button @click="addProduct" class="btn btn-outline-info btn-block">Ekle!</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import {eventBus} from "../main";

export default {
  data() {
    return {

      product: {
        price: null,
        count: null,
        title: null,
        selectedImage: null,
        totalPrice: null
      }
    }
  },
  methods: {
    onChange(e) {
      const file = e.target.files[0];
      this.product.selectedImage = URL.createObjectURL(file);
    },
    addProduct() {
      this.product.totalPrice = this.product.price * this.product.count;
      eventBus.$emit("productAdded", this.product);
      this.product = {
        price: null,
        count: null,
        title: null,
        selectedImage: null,
        totalPrice: null
      }
    }
  }
}
</script>
