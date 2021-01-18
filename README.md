<p align="center">
  <a href="https://github.com/kettanaito/naming-cheatsheet">
    <img src="./naming-cheatsheet.png" alt="Naming cheatsheet" />
  </a>
</p>

# İsimlendirme Kuralları

- [İngilizce](#İngilizce)
- [İsimlendirme kuralı](#İsimlendirme-kuralı)
- [K-S-A](#k-s-a)
- [Kısaltma kullanmayın](#kısaltma-kullanmayın)
- [Bağlam tekrarı yapmayın](#bağlam-tekrarı-yapmayın)
- [Beklenen sonucu yansıtın](#beklenen-sonucu-yansıtın)
- [Fonksiyonları isimlendirmek](#Fonksiyonları-isimlendirmek)
  - [A/YB/DB deseni](#aybdb-deseni)
    - [Aksiyonlar](#aksiyonlar)
    - [Bağlam](#bağlam)
    - [Önekler](#önekler)
- [Tekil ve Çoğullar](#singular-and-plurals)

---

Bir şeyleri isimlendirmek zordur. Bu sayfa ise bir şeyleri isimlendirmeyi daha kolay bir hale getirmeye çalışıyor.

Buradaki öneriler herhangi bir program diline uyarlanabilir olsa da, pratikte açıklamak için JavaScript kullanacağım.

## İngilizce

Değişkenlerinizi ve fonksiyonlarınızı adlandırırken İngilizce kullanın.

```js
/* Kötü */
const adi = "Cenk";
const arkadaslari = ["Ecenur", "Serkan"];

/* İyi */
const firstName = "Cenk";
const friends = ["Ecenur", "Serkan"];
```

> Beğenin veya beğenmeyin, İngilizce programlama alanında baskın dil: tüm programlama dillerinin sözdizimleri İngilizce, aynı şekilde sayısız dökümantasyon ve eğitim materyali de. İngilizce yazarak kodunuzun tutarlılığını önemli ölçüde artırırsınız.

## İsimlendirme kuralı

**Bir** adet isimlendirme kuralı belirleyin ve onunla devam edin. Seçtiğiniz kural `camelCase` veya `snake_case` veya herhangi başka bir şey olabilir önemli değil. Önemli olan tutarlı kalmak.

```js
/* Kötü */
const pages_count = 5;
const shouldUpdate = true;

/* İyi */
const pageCount = 5;
const shouldUpdate = true;

/* Bu da İyi */
const page_count = 5;
const should_update = true;
```

## K-S-A

Bir isim _kısa_, _sezgisel_ ve _açıklayıcı_ olmalı:

- **Kısa**. Bir ismin yazılması uzun sürmemeli, böylece hatırlanabilir de olacaktır;
- **Sezgisel**. Bir isim doğal bir şekilde okunabilir, olabildiğince yaygın konuşmaya yakın olmalı;
- **Açıklayıcı**. Bir isim yaptığı/sahip olduğu şeyi en verimli şekilde yansıtmalı.

```js
/* Kötü */
const a = 5; // "a" her anlama gelebilir
const isPaginatable = a > 10; // "Paginatable" kulağa hiç doğal gelmiyor
const shouldPaginatize = a > 10; // Uydurma fiiller çok eğlencelidir!

/* İyi */
const postCount = 5;
const hasPagination = postCount > 10;
const shouldDisplayPagination = postCount > 10; // alternatif
```

## Kısaltma Kullanmayın

Kısaltmaları **kullanmayın**. Kodun okunabilirliğinin azalmasından başka hiçbir işe yaramazlar. Kısa ve açıklayıcı bir isim bulmak zor olabilir, ancak kısaltma bunun için bir çözüm değildir.

```js
/* Kötü */
const onItmClk = () => {};

/* İyi */
const onItemClick = () => {};
```

## Bağlam tekrarı yapmayın

Bir isim, tanımlandığı bağlamı tekrar etmemelidir. Okunabilirliğini azaltmıyorsa her zaman isimden bağlamı kaldırın.

```js
class MenuItem {
  /* Fonksiyon isminde bağlam tekrar kullanılıyor ("MenuItem" olan) */
  handleMenuItemClick = (event) => { ... }

  /* `MenuItem.handleClick()` olarak güzelce okunuyor */
  handleClick = (event) => { ... }
}
```

## Beklenen sonucu yansıtın

Bir isim, beklenen sonucu yansıtmalıdır.

```jsx
/* Kötü */
const isEnabled = itemCount > 3;
return <Button disabled={!isEnabled} />;

/* İyi */
const isDisabled = itemCount <= 3;
return <Button disabled={isDisabled} />;
```

---

# Fonksiyonları isimlendirmek

## A/YB/DB deseni

Fonksiyonları adlandırırken izlenecek faydalı bir model vardır:

```
önek? + aksiyon (A) + yüksek bağlam (YB) + düşük bağlam? (DB)
```

Aşağıdaki tabloda bu modelin nasıl uygulanabileceğine bir göz atın.

| İsim                   | Önek     | Aksiyon (A) | Yüksek bağlam (YB) | Düşük bağlam (DB) |
| ---------------------- | -------- | ----------- | ------------------ | ----------------- |
| `getPost`              |          | `get`       | `Post`             |                   |
| `getPostData`          |          | `get`       | `Post`             | `Data`            |
| `handleClickOutside`   |          | `handle`    | `Click`            | `Outside`         |
| `shouldDisplayMessage` | `should` | `Display`   | `Message`          |                   |

> **Not:** Bağlamın sırası bir değişkenin anlamını etkiler. Örneğin, "shouldUpdateComponent" bir bileşeni güncellemek üzere olduğunuz anlamına gelirken, "shouldComponentUpdate" size _component_ öğesinin kendi kendine güncelleneceğini ve ne zaman güncellenmesi gerektiğini sizin kontrol ettiğiniz anlamına gelir.
> Başka bir deyişle, **yüksek bağlam bir değişkenin anlamını vurgular**.

---

## Aksiyonlar

Fonksiyon adınının fiil kısmı. Fonksiyonun _ne yaptığını_ açıklamaktan sorumlu en önemli kısım.

### `get`

Verilere anında erişir (örneğin dahili verilerin kısa toplayıcısı).

```js
function getFruitCount() {
  return this.fruits.length;
}
```

> Ayrıca bakınız [compose](#compose).

### `set`

`A` değerinden `B` değerine bir değişkeni dekleratif bir biçimde değiştirir.

```js
let fruits = 0;

function setFruits(nextFruits) {
  fruits = nextFruits;
}

setFruits(5);
console.log(fruits); // 5
```

### `reset`

Bir değişkeni başlangıç değerine veya durumuna geri döndürür.

```js
const initialFruits = 5;
let fruits = initialFruits;
setFruits(10);
console.log(fruits); // 10

function resetFruits() {
  fruits = initialFruits;
}

resetFruits();
console.log(fruits); // 5
```

### `fetch`

Belirsiz bir süre alan bazı veriler için istek yapar (örneğin, async request).

```js
function fetchPosts(postCount) {
  return fetch('https://api.dev/posts', {...})
}
```

### `remove`

Bir yerden _bir şeyi_ kaldırır.

Örneğin, bir arama sayfasında seçilen filtrelerden oluşan bir koleksiyonunuz varsa, koleksiyondan birini kaldırmak için `removeFilter` kullanırsınız, `deleteFilter` **değil** (Doğal olarak İngilizce söyleyeceğiniz de budur):

```js
function removeFilter(filterName, filters) {
  return filters.filter((name) => name !== filterName);
}

const selectedFilters = ["price", "availability", "size"];
removeFilter("price", selectedFilters);
```

> Ayrıca bakınız [delete](#delete).

### `delete`

Varoluş aleminden bir şeyi tamamen siler.

Bir içerik editörü olduğunuzu ve kurtulmak istediğiniz kötü şöhretli bir gönderi olduğunu hayal edin. Parlak bir "Gönderiyi sil" düğmesini tıkladığınızda, CMS bir `deletePost` aksiyonu gerçekleştirdi, `removePost` **değil**.

```js
function deletePost(id) {
  return database.find({ id }).delete();
}
```

> Ayrıca bakınız [remove](#remove).

### `compose`

Mevcut olandan yeni veriler oluşturur. Çoğunlukla stringler, nesneler veya fonksiyonlar için geçerlidir.

```js
function composePageUrl(pageName, pageId) {
  return `${pageName.toLowerCase()}-${pageId}`;
}
```

> Ayrıca bakınız [get](#get).

### `handle`

Bir aksiyonu yönetir. Genellikle bir callback fonksiyonunu adlandırırken kullanılır.

```js
function handleLinkClick() {
  console.log("Linke tıklandı!");
}

link.addEventListener("click", handleLinkClick);
```

---

## Bağlam

Bir fonksiyonun üzerinde çalıştığı alan.

Bir fonksiyon genellikle _bir şey_ üzerine yapılan bir aksiyondur. Çalıştırılabilir alanının veya en azından beklenen bir veri türünün ne olduğunu belirtmek önemlidir.

```js
/* Primitivelerle çalışan saf bir fonksiyon */
function filter(predicate, list) {
  return list.filter(predicate);
}

/* Tam olarak postslarla çalışan bir fonksiyon */
function getRecentPosts(posts) {
  return filter(posts, (post) => post.date === Date.now());
}
```

> Bazı dile özgü varsayımlar, bağlamın çıkarılmasına izin verebilir. Örneğin, JavaScript'te, `filter` ın Array üzerinde çalışması yaygındır. Açıkça `filterArray` eklemek gereksiz olacaktır.

--

## Önekler

Önek, bir değişkenin anlamını geliştirir. Fonksiyon adlarında nadiren kullanılır.

### `is`

Mevcut bağlamın bir karakteristiğini veya durumunu açıklar (genellikle `boolean`).

```js
const color = "blue";
const isBlue = color === "blue"; // karakteristik
const isPresent = true; // durum

if (isBlue && isPresent) {
  console.log("Mavi mevcut!");
}
```

### `has`

Mevcut bağlamın belirli bir değere veya duruma sahip olup olmadığını açıklar (genellikle `boolean`).

```js
/* Kötü */
const isProductsExist = productsCount > 0;
const areProductsPresent = productsCount > 0;

/* İyi */
const hasProducts = productsCount > 0;
```

### `should`

Belirli bir eylemle birlikte pozitif bir koşullu ifadeyi (genellikle `boolean`) yansıtır.

```js
function shouldUpdateUrl(url, expectedUrl) {
  return url !== expectedUrl;
}
```

### `min`/`max`

Minimum veya maksimum değeri temsil eder. Sınırları veya sınırları açıklarken kullanılır.

```js
/**
 * Verilen minimum/maksimum sınırlar dahilinde
 * rastgele sayıda gönderi oluşturur.
 */
function renderPosts(posts, minPosts, maxPosts) {
  return posts.slice(0, randomBetween(minPosts, maxPosts));
}
```

### `prev`/`next`

Geçerli bağlamda bir değişkenin önceki veya sonraki durumunu belirtir. Durum geçişlerini açıklarken kullanılır.

```jsx
function fetchPosts() {
  const prevPosts = this.state.posts;

  const fetchedPosts = fetch("...");
  const nextPosts = concat(prevPosts, fetchedPosts);

  this.setState({ posts: nextPosts });
}
```

## Tekil ve Çoğullar

Önek gibi, değişken isimleri de tek bir değer veya birden fazla değer bulundurmalarına bağlı olarak tekil veya çoğul yapılabilir.

```js
/* Bad */
const friends = "Eser";
const friend = ["Leyla", "Uğur", "Ahsen"];

/* Good */
const friend = "Eser";
const friends = ["Leyla", "Uğur", "Ahsen"];
```
