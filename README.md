# EGE Robotik Cərrahiyyə Mərkəzi

Robotikcerrahiyye.az.docx sənədinin məzmunu və UX/UI brifi əsasında hazırlanmış sayt.

## Səhifələr

- Ana səhifə: xidmət axtarışı, həkim, rəylər, sual-cavab və əlaqə
- 5 xidmət səhifəsi
- Həkim profili
- Robotik cərrahiyyə haqqında
- Mərkəz haqqında
- Konsultasiya seçimi
- Məxfilik və istifadə

## İstifadə

`dist` qovluğu tam statik saytdır. HTML, CSS və JavaScript fayllarını statik hostinqdə yerləşdirmək kifayətdir. Lokal baxış üçün `dist` qovluğunu HTTP serverlə açın. Faylı birbaşa iki kliklə açmaq əvəzinə server istifadə edilməlidir.

Əsas məzmun və davranış: `dist/app.js`. Vizual üslub: `dist/style.css`. HTML səhifələr: `dist/index.html` və alt qovluqlar.

## Qəbul prosesi

İstifadəçi istiqaməti seçir, sonra telefon və ya WhatsApp-a keçərək komanda ilə vaxtı dəqiqləşdirir. Sayt avtomatik qəbul yaratmır, pasiyent məlumatı saxlamır və mesaj göndərmir. WhatsApp mesajını istifadəçi özü göndərir. Real vaxtlı qəbul, CRM, SMS, pasiyent kabineti və analiz nəticələri inteqrasiyası daxil deyil.

## Mənbələr

- Loqo, əsas tibbi məzmun, əlaqə və təqdim edilmiş rəylər: istifadəçinin Word sənədi.
- Həkim profili və foto: https://egehospital.az/hekimler/108-uzman-dr-emin-memmedov.html
- Robotik sistem təsviri: https://egehospital.az/bloglar/238-prostat-vzi-crrahiyysind-robotik-crrahiyy.html
- Video: https://www.youtube.com/watch?v=EScQbz6EHbM
- Şrift: Google Fonts Manrope.

Rəsmi saytdakı təsvirlər üçün açıq təkrar istifadə lisenziyası müəyyən edilməyib. Geniş ictimai yayımdan əvvəl mərkəz öz vizuallarının və pasiyent rəylərinin istifadə hüququnu, xidmətlərin mövcudluğunu və tibbi mətnlərin son təsdiqini dəqiqləşdirməlidir. Təqdim edilən rəylərə sübutsuz 5 ulduz reytinqi və ümumi qiymətləndirmə əlavə edilməyib.

Robotikcerrahiyye.az domeni avtomatik qoşulmur. İstifadəçinin seçiminə əsasən sayt yalnız lokal saxlanılır.

## 3D açılış

Ana səhifənin ilk açılışında təxminən 3 saniyəlik WebGL animasiyası işləyir. Sağ və soldan daxil olan iki robotik alət real həcmli mesh hissələrdən modelləşdirilib; metal səthlər, oynaqlar, tutucu uclar və işıqlandırma kodla yaradılır. Bu, konkret tibbi cihazın texniki modeli deyil, stilizə edilmiş brend animasiyasıdır. Göndərilmiş WhatsApp videosu yalnız loqo üslubu üçün baxılıb, sayta video kimi əlavə edilməyib.

Animasiya hər brauzer sessiyasında bir dəfə göstərilir. Ana səhifədə “3D açılışa yenidən bax” düyməsi ilə təkrar izləmək olar. `/?intro=1` keçidi açılışı təkrar göstərir. “Keç” və Escape animasiyanı bağlayır. Azaldılmış hərəkət seçimi aktivdirsə avtomatik açılış göstərilmir. WebGL və ya modul yüklənməsi uğursuz olduqda sayt açıq qalır; ehtiyat bağlanma həddi 3.5 saniyədir (üzərinə 0.25 saniyəlik keçid).

Fayllar: `dist/intro.js`, `dist/intro-scene.js`, `dist/intro.css`. Three.js 0.180.0 lokal `dist/vendor` qovluğundadır və MIT lisenziyası daxil edilib. 3D açılış üçün xarici şəbəkə tələb olunmur. Animasiya tamamlandıqda GPU resursları azad edilir.

Model formaları üçün istinad: https://www.intuitive.com/en-in/products-and-services/da-vinci/instruments

Loqo da tam 3D həndəsə ilə yaradılıb: emblemin iki hissəsi, EGE hərfləri, cərrahi yataq və kiçik robotik alətlər. Başlanğıcda dağınıq hissələri iki robotik qol üç mərhələdə tutub loqo şəklində yığır. Loqonun orijinal konturları həcmli həndəsəyə çevrilir; orijinal rənglər ön səth materialında istifadə edilir.


## Node.js ilə lokal başlatmaq

Node.js 18 və ya daha yeni versiya tələb olunur. ZIP-i tam çıxarın. `package.json` olan qovluqda terminal açın:

```sh
npm start
```

Sonra http://127.0.0.1:3000/ ünvanını açın. 3D animasiyaya birbaşa baxış: http://127.0.0.1:3000/?intro=1

Əlavə paket yoxdur: `npm install` və ayrıca build lazım deyil. Alternativ: `node server.cjs` və ya `npm run dev`. Server işlədiyi müddətdə terminalı açıq saxlayın; dayandırmaq üçün Ctrl+C basın. Fayl dəyişikliklərini görmək üçün brauzeri yeniləyin.

Windows-da `Sayti-ac.cmd` faylına iki dəfə klikləməklə də serveri başlatmaq olar. Brauzerdə yuxarıdakı ünvanı açın. Python tələb olunmur.

3000 portu tutulubsa, PowerShell-də:

```powershell
$env:PORT=3001
npm start
```

Bu halda ünvan http://127.0.0.1:3001/ olacaq. macOS/Linux: `PORT=3001 npm start`.

Server yalnız bu kompüterdə işləyir və yalnız `dist` qovluğundakı sayt fayllarını təqdim edir. Sayt internetdə yayımlanmır.

## Mexaniki səhnə yeniləməsi
Qolların sabit çiyin bazaları ekranın sol və sağ sərhədlərindən kənardadır. İki sabit uzunluqlu qol seqmenti tərs kinematika ilə hədəfə yönəlir. Hissələr iş səthində dayanır, tutucu bağlandıqdan sonra qaldırılır və hamar sürət profili ilə yerinə qoyulur. Bu, bədii kinematik animasiyadır; tam rigid-body və toqquşma simulyasiyası deyil. Bir əsas işıq kölgə yaradır, əlavə işıq və studiya əksolunmaları materialların həcmini vurğulayır.
Nümunələr: https://elements.envato.com/robotic-arms-logo-KLLRPLW və https://sites.duke.edu/ddmc/2016/10/13/3d-animation-process-for-the-tec/
Kölgə texnikası: https://threejs.org/manual/pages/shadows.html


## Qısaldılmış UX açılışı
3D ardıcıllıq 2.65 saniyə, səhifəyə keçid 0.25 saniyədir; səhnənin hazırlanma müddəti cihazdan asılıdır. Daşıma məsafələri və fırlanmalar qısaldılıb. Sessiyada yalnız bir dəfə avtomatik oynayır. Hash ilə birbaşa bölməyə girişdə avtomatik intro atlanır. Keç/Escape və azaldılmış hərəkət dəstəyi saxlanılıb. ?intro=1 yalnız təkrar önbaxış üçündür.



UI yenilənməsi: intro sonunda saytın orijinal loqosu göstərilir, üst-üstə düşən ayrıca yazı çıxarılıb. Həkim bölmələri şəkilsizdir. Pasiyentin yolu çıxarılıb. Xidmət kartları, standart ox ikonları, açıq FAQ rəngi və əlaqə CTA bölməsi yenilənib.

Son yeniləmə: 3D loqo yığıldıqdan sonra model gizlədilmir və 2D şəkilə keçid edilmir. Kiçik yazılar da orijinal loqonun konturlarından yaranır. Texnologiya bölməsi yığcam tipoqrafiya və brend rəngləri ilə yenilənib.
