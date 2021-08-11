# vue-provide-inject-example

## Project setup
```
yarn install

or

npm install
```

### Compiles and hot-reloads for development
```
yarn serve

or

npm run serve
```

### Vue3 composition api Provide / Inject
See [Provide / Inject](https://v3.cn.vuejs.org/guide/composition-api-provide-inject.html#%E8%AE%BE%E6%83%B3%E5%9C%BA%E6%99%AF).

---

## 總結

### 起源
練習過程中將api的呼叫方法抽出，透過`組合式API(composition api)`方式引入，目的在減少HelloWorld.vue的代碼，

最初的想法是透過父級將`呼叫api方法`跟`api返回值`引入，然後在子級透過props傳遞`呼叫api方法`跟`api返回值`或是也在子級引入`呼叫api方法`跟`api返回值`，
預想是父級的watch監聽返回值，然後子級更新api時，父級監聽的返回值因為子級的使用而更新，導致父級拿到新的返回值，在透過props傳遞新值給子級，
來達到一個父子的值是連動的一個狀態(父級更動值時子級也會更動，或是顛倒過來子級作動時父級也更動)，

但，在實作後發現`組合式API(composition api)`比較像是引入一段本來可以存在於你的程式碼中的程式碼，當這段程式碼，在別的component被引用時，他就屬於那一個component的程式碼
因此即使是父子級的關係，也無法透過上面的想法達到連動的效果，因此我把目光轉向`provide/inject`

### 結果
使用provide/inject，可以讓父級想傳遞的數據直接傳遞至目標子級(不管中間有幾層)，有效減少層層傳遞造成的維護困難與麻煩，可不透過store做到數據傳遞至多層

在父級與子級的關係底下：

1. provide可以傳遞`值`或`方法`
2. 在inject設置預設值，預設值在父級未provide相對應的`值`或`方法`使觸發
3. 如果值需要在父級與子級都同時作動，可使用ref或reactive變成響應式
4. 如果不希望子級更改到父級的值，可在父級對值加上readonly
