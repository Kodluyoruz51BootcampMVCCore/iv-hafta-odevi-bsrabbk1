# iv-hafta-odevi
*  Geri dönen bilgiye göre yeşil renkte onay mesajı gösterilmesi. (örneğin:view bag)

*  AddMVC - AddMVCCore - AddDateAnnotations nedir? Nerelerde eklenmelidir?
#### AddMvc vs AddMvcCore?

Projenin Startup sınıfının ConfigureServices() öğesinde bu iki yönteme rastlarız.

AddMVC () yönteminin kaynak kodu= 

[https://github.com/aspnet/Mvc/blob/48546dbb28ee762014f49caf052dc9c8a01eec3a/src/Microsoft.AspNetCore.Mvc/MvcServiceCollectionExtensions.cs]: 

- AddMvc ()  AddMvcCoredan daha çok işlevsellik sağlar.
- AddMvc () CORS desteği, Razor View Engine, data annotations, Cache tag helper gibi özellikler eklemeyi sağlar.

AddMvcCore () yönteminin kaynak kodu= 

[https://github.com/aspnet/Mvc/blob/48546dbb28ee762014f49caf052dc9c8a01eec3a/src/Microsoft.AspNetCore.Mvc.Core/DependencyInjection/MvcCoreServiceCollectionExtensions.cs]: 

AddMvcCore () işlevi denetleyici yönetimi ve yönlendirme gibi bazı temel işlemleri gerçekleştirir.

 * Shanpshot nedir? nasıl değişir? neden alınır?

*  Jquery Calender--> [Datapicker](https://jqueryui.com/datepicker/) --> DueAt'i takvim tipinde eklemek nasıl yapılır? Araştırınız. (DateTimeUffset tipinden atamalar oluşucak)

*  First- FirstOrDefault ve Single- SingleOrDefault nedir? Aralarındaki farkı araştırınız.

*  En kısa null check nasıl yapılır?

* partial view nedir?

* Farklı authentication bulup,aynı işleri farklı yollar ile yapanları araştırınız.

* Ödev- Razor Pages/MVC Projects karşılaştırmasını yapınız.
