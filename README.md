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

### Snapshot Nedir ? Nasıl Çalışır? 

Kısa süreli çalışmaların öncesinde backup almak yerine snapshot kullanırız. Anlık ekran görüntüsü almayı sağlar. Geri almak istediğimiz bir işlem için snapshot'a revert diyerek eski haline dönüş yapabiliriz.

Snapshot'ın kısa süreli işlemler için kullanılması öneriliyor. 24-72 saat arasında snapshot'ın silinmesi gerektiği önerilmekte bu saatten uzun süreli kullanılırsa performans anlamında problemler yaşanabilmektedir.

### Jquery Calender--> [Datapicker](https://jqueryui.com/datepicker/) --> DueAt'i takvim tipinde eklemek nasıl yapılır?

- Solution Explorer> dependencies kısmından sağ tıklayıp Manage Nuget Package e tıklayarak arama kısmından FullCalendar eklentisini bulup seçiyoruz ve install ediyoruz.

- Takvim üzerine verileri çekebilmek için models klasörüne class ekliyoruz.

- ```
  namespace FullCalendar.Models {
      public class CalendarEvent {
          public int id { get; set; }
          public string title { get; set; }
          public string start { get; set; }
          public string end { get; set; }
          public string color { get; set; }
          public bool allDay { get; set; }
      }
  }
  ```

- Conrollers klasörüne yeni bir class ekliyoruz.

- ```
  namespace FullCalendar.Controllers
  {
      public class CalendarController : Controller
      {
          //
          // GET: /Calendar/
  
          public ActionResult Index()
          {
  
              return View();
          }
  
          public JsonResult GetCalendarEvents() {
              List<CalendarEvent> eventItems = new List<CalendarEvent>();
              int i = 0, n = 9;
              for (i = 0; i < n; i++) {
                  AddItem(eventItems);
              }
  
              return Json(eventItems, JsonRequestBehavior.AllowGet);
          }
  
          Random random = new Random();
          public void AddItem(List<CalendarEvent> eventItems) {
              CalendarEvent item = new CalendarEvent();
  
              DateTime startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, random.Next(1, 30));
  
              item.id = random.Next(1, 100);
              item.start = startDate.ToString("s");
              item.end = startDate.AddDays(random.Next(1, 5)).ToString("s");
              item.allDay = true;
              item.color = "red";
              item.title = "Calendar Item " + item.id;
              eventItems.Add(item);
          }
  
      }
  }
  ```

- Burdaki işlem CalenderEvent  nesnesine 10 elemanlı bir liste oluşturmak.

Bu listeyi takvime çekmek için:

- Viewa index sayfamızı oluşturuyoruz,

- ```
  <!DOCTYPE html>
  
  <html>
  <head>
      <meta name="viewport" content="width=device-width" />
      <title>Index</title>
  
      <link href="~/Content/fullcalendar.min.css" rel="stylesheet" />
  </head>
  <body>
      <div id="calendar">
  
      </div>
  
      <script src="~/Scripts/jquery-2.0.0.min.js"></script>
      <script src="~/Scripts/moment.min.js"></script>
      <script src="~/Scripts/moment-with-locales.min.js"></script>
      <script src="~/Scripts/fullcalendar/fullcalendar.min.js"></script>
      <script src="~/Scripts/fullcalendar/locale/tr.js"></script>
      <script src="~/Scripts/fullcalendar/locale-all.js"></script>
  
      <script>
          $(document).ready(function () {
              GetCalendarEvents();
          });
  
          function GetCalendarEvents() {
              debugger;
              $('#calendar').fullCalendar({
                  lang: 'tr',
                  header: {
                      left: 'prev,next today',
                      center: 'title',
                      right: 'month,agendaWeek,agendaDay'
                  },
                  editable: true,
                  events: '/Calendar/GetCalendarEvents/',
                  eventClick: function (event) {
                      alert('Item ID: ' + event.id  + "\nItem Title: " + event.title);
                  }
              });
          }
      </script>
  
  </body>
  </html>
  ```

### Single vs SingleOrDefault

Int tipinde bir dizi var diyelim. Bu dizi içerisinden seçim yapmak istediğimizde seçim şartı sağlanmıyor ise varsayılan değer olan sıfırın döndürülmesini sağlamak için SingleOrDefault kullanmamız gerekir.

Int tipinde bir dizide seçimimizin sonucunda bir eleman geleceği garanti ise Single kullanılır.

### First vs FirstOrDefault

Yine int tipinde bir diziden, seçilecek olan şarta göre o şarttan büyük ilk eleman seçilir.

Single ile aynı mantıktadır bir elemanın geleceği garanti ise kullanılır ancak şartın bir büyüğü seçilir.

[https://medium.com/@ruveydakardelcetin/single-singleordefault-ve-first-firstordefault-fark%C4%B1-d7657eec8d02]: 

### Null Check

- Null dönen ifadeler çok rastlanan hatalardır.

var a; 

Console.Write(a ?? "boş değer");

- Diyerek a değeri null değil ise ekrana a nın değerini yaz.

- A değeri null ise boş değer ifadesini yaz diyoruz.

  ### Partical View

  - Mantık olarak User Control kavramı ile aynıdır.

  - Kendi başına bir işlvei yoktur, bulunduğu sayfa içerisinde çalışır.

  - Yolladığımız modeller üzerinde işlem yaparlar.

  - Patical View ile arayüzü modüler bir hale getiririz.

  - Bir işlemi birden fazla kez yapacaksak kullanıyoruz.

  - Shared klasörüne Add>View  ciyip Create as partial view seçerek partical bir method olarak oluştururuz.

  - Bir liste oluşturduk diyelim bu listeyi istediğim sayfalarda kullanmak istiyorum.Bu listeyi kaydedip Views/Home/Index.cshtml dosyasına @Html.Partial("~/Views/Home/PartialView.cshtml") satırını ekliyorum.

  - Bu sayede bu satırı nereye yapıştırırsam oluşturduğum liste istediğim sayfada eklenmiş oluyor. 

    
### Authentication

- Veri güvenliği tabiridir. Herhangi bir internet kullanıcısının , uygulamanın veya programın sisteme erişirken kim olduğunu kanıtlama işlemidir.

- Kimlik doğrulama kavramı ile aynı şeydir.

- Kullanıcının girdiği kimlik bilgileri giriş yapmak istediği sistemdeki veri tabanında bulunan bilgilerle karşılaştırılır bilgiler eşleştiğinde giriş izni verilir.

  #### Temel Kimlik Doğrulaması

  - HTTP temel kimlik doğrulaması sunucunun istemciden kimlik bilgilerini istediği basit bir doğrulama şeklidir.

  #### Form Kimlik Doğrulaması

  - Doğrulama işlemi için tarayıcıda bulanan çerezleri kullanır.
  - Çerez bilgisi yok ise kullanıcı sisteme girmek zorundadır.
  - Giriş yapmış bir kullanıcının çerezlerin geçerlilik süresi dolduğunda kullanıcı tekrar giriş sayfasına döner.

  #### OAuth 2 

  - Web uygulamalarının Facebook, GtiHub gibi hizmetlerdeki kullanıcı hesaplarına sınırlı olarak erişim elde etmeyi sağlar.
  -   Kullanıcının, kimlik doğrulamasını kullanıcı hesabını  barındıran hizmete devredip üçüncü taraf uygulamalarının hesabına erişmesini izin vermesi ile çalışır.

  #### Identity Framework

  - Genişletilebilir ve özelleştirilebilir bir yapıya sahiptir.
  - Facebook, Google servisleri, Twitter üzerinden üyelik gerçekleştirmeyi sağlar.
  - Azure ile kolay entegre olur.
  - Güncellenebilir ve yönetilebilir.     

 


 * Shanpshot nedir? nasıl değişir? neden alınır?

*  Jquery Calender--> [Datapicker](https://jqueryui.com/datepicker/) --> DueAt'i takvim tipinde eklemek nasıl yapılır? Araştırınız. (DateTimeUffset tipinden atamalar oluşucak)

*  First- FirstOrDefault ve Single- SingleOrDefault nedir? Aralarındaki farkı araştırınız.

*  En kısa null check nasıl yapılır?

* partial view nedir?

* Farklı authentication bulup,aynı işleri farklı yollar ile yapanları araştırınız.

* Ödev- Razor Pages/MVC Projects karşılaştırmasını yapınız.
