<template>
  <transition name="modal"  :class="{ 'is-active': showContactModal }">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          
          <div class="modal-header">
            <slot name="header">
              <button class="delete" aria-label="close" @click="$emit('close')"></button>
            </slot>
          </div>

          <div class="modal-body">
            <slot name="body">
                <form>
                    <div class="field">
                      <label class="label">スクールに連絡する</label>
                      <div class="control">
                        <textarea class="textarea" placeholder="ラインで返信が来ます"></textarea>
                      </div>
                    </div>
                </form>
            </slot>
        </div>

          <div class="modal-footer">
            <slot name="footer">
              <button class="button btn-line is-block is-fullwidth" @click="contact">
                送信
              </button>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  data() {
    return {
    }
  },
  props: {
    showContactModal: Boolean,
    action: {
      type: Function,
      required: true
    }
  },
  methods: {
    contact() {
      this.action()
    }
  }
}
</script>

<style scoped>
.btn-line {
  background-color: #00c300;
  border: 1px solid #00c300;
  color: white;
}
.orField {
    padding-top: 10px;
    padding-bottom: 15px;
}
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}
.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}
.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}
.modal-body {
  margin: 20px 0;
}
.modal-default-button {
  float: right;
}
.modal-enter {
  opacity: 0;
}
.modal-leave-active {
  opacity: 0;
}
.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}


input[type=checkbox] {
  display: none;
}
.checkbox {
  box-sizing: border-box;
  -webkit-transition: background-color 0.2s linear;
  transition: background-color 0.2s linear;
  position: relative;
  display: inline-block;
  margin: 0 20px 8px 0;
  padding: 12px 12px 12px 42px;
  border-radius: 8px;
  background-color: #f6f7f8;
  vertical-align: middle;
  cursor: pointer;
}
.checkbox:hover {
  background-color: #e2edd7;
}
.checkbox:hover:after {
  border-color: #53b300;
}
.checkbox:after {
  -webkit-transition: border-color 0.2s linear;
  transition: border-color 0.2s linear;
  position: absolute;
  top: 50%;
  left: 15px;
  display: block;
  margin-top: -10px;
  width: 16px;
  height: 16px;
  border: 2px solid #bbb;
  border-radius: 6px;
  content: '';
}

.checkbox:before {
  -webkit-transition: opacity 0.2s linear;
  transition: opacity 0.2s linear;
  position: absolute;
  top: 50%;
  left: 21px;
  display: block;
  margin-top: -7px;
  width: 5px;
  height: 9px;
  border-right: 3px solid #53b300;
  border-bottom: 3px solid #53b300;
  content: '';
  opacity: 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
input[type=checkbox]:checked + .checkbox:before {
  opacity: 1;
}
</style>