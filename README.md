

## Google Analytics 4 dataLayer Kurulum Klavuzu


### Datalayer Eventları

🚩 Her event ayrı ayrı tetiklenecektir. 

Eventlar içindeki **items** dizisindeki obje sayısı, ölçümü yapılması istenen ürünlerin sayısı kadar olacak. Örneğin 3 tane ürün satınalınmışsa purchase eventında items dizisinde her ürün bilgilerini içeren 3 tane obje eklenecek.

Eventta yer alan parametre ve aldıkları değerler aşağıdaki gibi olacak:

- **value** - ürün fiyatıdır. items içindeki price * quantity sonucu elde edilen toplam miktar

- **currency** - para birimidir. TRY, USD şekilde olacak

- **item_list_id** - varsa kategori id numarası

- **item_list_name** - kategori ismi

- **item_name** - ürün ismi

- **item_id** - ürün id değeri. DİKKAT ❗❗❗ sku değil, id olacak

- **price** - ürün fiyatı. küsürat nokta ile ayrılacak ve Number olarak

- **quantity** - ürün miktarı

- **item_brand** - ürün markası

- **item_category**, **item_category2**, **item_category3**, **item_category4**, **item_category5**, - ürün kategori kırılımlarıdır. Örneğin sitenizde kategori kırılımı "Anasayfa > Erkek > Giyim > T-Shirt > Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört" şeklinde ise, baştaki Anasayfa ve sondaki ürün ismi alınmaksızın *item_category: "T-Shirt", item_category2: "Giyim", item_category3: "Erkek"* olacak şekilde ayarlanacak. item_category4 ve item_category5 yoksa boş gönderilebilir. Esasında hiçbiri zorunlu değil lakin ilk değer item_category gönderilirse iyi olur

- **item_list_name** - eventın tetiklendiği liste ismini içerir. Örneğin anasayfada çok satanlar bölümünden sepete eklenmişse *item_list_name: "Çok Satanlar"* olacaktır. Zorunlu alan değildir. İsteğe bağlı gönderilebilir

- **transaction_id** - sipariş numarası
- **tax** - vergi tutarı
- **shipping** - kargo tutarı
- **coupon** - kupon kodu

- **enhanced_conversion_data** - bu dizi google ads enahcned conversion için gereklidir. girilen verilere google tarafından sha250 uygulanacağı için kvkk sorunu yaşanmamaktadır. email ve phone number zorunludur, diğerleri de olursa daha iyi olur

- **id** - ga4 ürün id değerini items dizisinde *item_id* olarak isterken, ads *id* olarak istemektedir. bu yüzden aynı items dizi içinde id olarak ek parametre eklenmiştir

- **google_business_vertical** - iş türünüz için ürün özelliklerini bulmak amaçlı kullanılır. e-ticaret siteleri için statik değer *'retail'* olacaktır


#

### 🚩 Liste Görüntüleme - **view_item_list**
 
```view_item_list``` kategori sayfalarında listelenen ürünleri ölçer.

Tamamı gönderilmesine gerek yoktur. İlk 7 ürün yeterlidir.

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ 'ecommerce': null }); // Önceki eventın ecommerce verisini temizler.
window.dataLayer.push({
    'event': "view_item_list",
    'ecommerce': {

        // GA4 event parametreleri ⤵️
        'item_list_id': "123",
        'item_list_name': "T-Shirt",
        'items': [{
            'item_name': "Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört",
            'item_id': "123",
            'price': 130.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "123",
            'google_business_vertical': 'retail'
        },
        {
            'item_name': "V Yaka Kısa Kollu Tişört",
            'item_id': "124",
            'price': 120,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "124",
            'google_business_vertical': 'retail'
        },
        {
            'item_name': "Siyah Beyaz Oval Kesim Tshirt",
            'item_id': "125",
            'price': 1230.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "125",
            'google_business_vertical': 'retail'
        }],
    },
});
```

### 🚩 Ürün Görüntüleme - **view_item**
 
```view_item``` ürün ayrıntılarının kaç kez görüntülendiğini ölçer. Bu event ürün sayfaları yüklendiğinde tetiklenir.

```javascript
window.dataLayer = window.dataLayer || [];
dataLayer.push({ 'ecommerce': null }); // Önceki eventın ecommerce verisini temizler.
window.dataLayer.push({
    'event': "view_item",
    'ecommerce': {

        // GA4 event parametreleri ⤵️
        'value': 130.99,
        'currency': 'TRY',
        'items': [{
            'item_name': "Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört",
            'item_id': "123",
            'price': 130.99,
            'quantity': 1, // view_item için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "123",
            'google_business_vertical': 'retail'
        }],
    }
});
```

### 🚩 Sepete Ekleme - **add_to_cart**
 
```add_to_cart``` sepete eklenen ürünlerin ölçümünü yapar. Bu event sepete ekleme işlemi yapılan tüm sayfalarda tetiklenecek.
 
```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ 'ecommerce': null }); // Önceki eventın ecommerce verisini temizler.
window.dataLayer.push({
    'event': "add_to_cart",
    'ecommerce': {

        // GA4 event parametreleri ⤵️
        'value': 392.97,
        'currency': 'TRY',
        'items': [{
            'item_name': "Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört",
            'item_id': "123",
            'price': 130.99,
            'quantity': 3,
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "123",
            'google_business_vertical': 'retail'
        }],
    }
});
```

### 🚩 Sepet - **view_cart**

```view_cart``` sepetteki ürünlerin ölçümünü yapar. Bu event sepet sayfasında tetiklenecek.

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ 'ecommerce': null }); // Önceki eventın ecommerce verisini temizler.
window.dataLayer.push({
    'event': "view_cart",
    'ecommerce': {

        // GA4 event parametreleri ⤵️
        'currency': "TRY",
        'value': 1480.99,
        'items': [{
            'item_name': "Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört",
            'item_id': "123",
            'price': 130.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "123",
            'google_business_vertical': 'retail'
        },
        {
            'item_name': "V Yaka Kısa Kollu Tişört",
            'item_id': "124",
            'price': 120,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "124",
            'google_business_vertical': 'retail'
        },
        {
            'item_name': "Siyah Beyaz Oval Kesim Tshirt",
            'item_id': "125",
            'price': 1230.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "125",
            'google_business_vertical': 'retail'
        }],
    },
});
```

### 🚩 Sepetten Çıkarma - **remove_from_cart**
 
```remove_from_cart``` sepetten çıkarılan ürünlerin ölçümünü yapar.
 
```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ 'ecommerce': null }); // Önceki eventın ecommerce verisini temizler.
window.dataLayer.push({
    'event': "remove_from_cart",
    'ecommerce': {

        // GA4 event parametreleri ⤵️
        'value': 392.97,
        'currency': 'TRY',
        'items': [{
            'item_name': "Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört",
            'item_id': "123",
            'price': 130.99,
            'quantity': 3,
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.
        }],
    }
});
```

### 🚩 Ödeme Başlatma - **begin_checkout**
 
```begin_checkout``` kullanıcı ödeme işlemini başlattığında gönderilir ve ödeme başlatma işlemlerini ölçmek için kullanılır.

view_cart event bilgileri ile aynı olacak.
value değerine *kargo dahil değildir.*
 
```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ 'ecommerce': null }); // Önceki eventın ecommerce verisini temizler.
window.dataLayer.push({
    'event': "begin_checkout",
    'ecommerce': {

        // GA4 event parametreleri ⤵️
        'currency': "TRY",
        'value': 1480.99,
        'items': [{
            'item_name': "Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört",
            'item_id': "123",
            'price': 130.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.
        },
        {
            'item_name': "V Yaka Kısa Kollu Tişört",
            'item_id': "124",
            'price': 120,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.
        },
        {
            'item_name': "Siyah Beyaz Oval Kesim Tshirt",
            'item_id': "125",
            'price': 1230.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.
        }],
    },
});
```

### 🚩 Ödeme Yöntemi - add_payment_info
 
```add_payment_info``` kullanıcı ödeme yöntemini seçtiği sayfada tetiklenir.

begin_checkout event bilgileri ile aynı olacak.
 
```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ 'ecommerce': null }); // Önceki eventın ecommerce verisini temizler.
window.dataLayer.push({
    'event': "add_payment_info",
    'ecommerce': {

        // GA4 event parametreleri ⤵️
        'currency': "TRY",
        'value': 1480.99,
        'payment_type': "Kredi Kartı", // Ödeme Türü
        'items': [{
            'item_name': "Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört",
            'item_id': "123",
            'price': 130.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.
        },
        {
            'item_name': "V Yaka Kısa Kollu Tişört",
            'item_id': "124",
            'price': 120,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.
        },
        {
            'item_name': "Siyah Beyaz Oval Kesim Tshirt",
            'item_id': "125",
            'price': 1230.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.
        }],
    },
});
```

### 🚩 Alışveriş Tamamlama - purchase

```purchase``` satın alma işlemini tamamladığında tetiklenir.
 
```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ 'ecommerce': null }); // Önceki eventın ecommerce verisini temizler.
dataLayer.push({
    'event': "purchase",
    'ecommerce': {

        // GA4 event parametreleri ⤵️
        'transaction_id': "T12345",
        'value': 809.70,
        'tax': 0.00, 
        'shipping': 0.00,
        'currency': "TRY",
        'coupon': 'indirim 100 tl', // Eğer kupon ile alınmışsa kupon değeri ilave edilecek. Yoksa "" boş gönderilebilir.
        'items': [{
            'item_name': "Pamuk Slim Fit Bisiklet Yaka Kısa Kollu Tişört",
            'item_id': "123",
            'price': 130.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "123",
            'google_business_vertical': 'retail'
        },
        {
            'item_name': "V Yaka Kısa Kollu Tişört",
            'item_id': "124",
            'price': 120,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "124",
            'google_business_vertical': 'retail'
        },
        {
            'item_name': "Siyah Beyaz Oval Kesim Tshirt",
            'item_id': "125",
            'price': 1230.99,
            'quantity': 1, // view_item_list için bu değer 1 olacak.
            'item_brand': "Ürün Markası",
            'item_category': "T-Shirt",
            'item_category2': "Giyim",
            'item_category3': "Erkek",
            'item_category4': "",
            'item_category5': "",
            'item_list_name': "", // Bu değer şimdilik boş dönebilir.

            // Google Ads Remarketing Parametreleri ⤵️
            'id': "125",
            'google_business_vertical': 'retail'
        }],

        // Google Ads Enhanced Ecommerce Parametreleri ⤵️
        'enhanced_conversion_data': {
            "email": 'E-mail adresi', // 
            "phone_number": '+90 555 111 22 33',
            "address": {
                "first_name": 'İsim',
                "last_name": 'Soyisim',
                "street": 'Sokak',
                "city": 'İl',
                "region": 'İlçe',
                "postal_code": 'Posta Kodu',
                "country": 'Ülke'
            }
        },
});
```

> Bunların haricinde tüm sayfalarda giriş yapmış müşterinin bilgilerini içeren dizi yazdırılacaktır.
Eğer kullanıcı giriş yapmamışsa boş ("") gönderilecek. Hangi bilgiler varsa gönderilsin, olmayanlar boş ("") gönderilsin.

```javascript
var user_data = [{
    name: 'İsim',
    surname: 'Soyisim',
    phone_number: '+905551112233', // Başında ülke kodu olacak.
    email: mail@gmail.com,
    country: 'Turkey',
    city: Istanbul,
    post_code: 34111,
    gender: 'm', // ya da 'f'
}]
```
