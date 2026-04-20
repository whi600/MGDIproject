# Impeccable Critique — Implementation Plan

## Критичные проблемы (влияют на UX/конверсию)

1. Сломанный якорь в CTA «Наша история»: ссылка ведет на `#why`, но секция `#why` не рендерится на главной. Пользователь кликает и не получает ожидаемого перехода.  
   [02Historyproect2Section.vue:75](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/02Historyproect2Section.vue:75), [HomePage.vue:23](C:/Users/User/Desktop/кодекс/vue-site/src/pages/HomePage.vue:23)

2. Несколько CTA ведут в несуществующие маршруты (`/open-project`, `/projects/...`) при текущем роутере. Это создает «тупики» вместо продолжения сценария.  
   [04GeogrfSection.vue:24](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/04GeogrfSection.vue:24), [04GeogrfSection.vue:34](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/04GeogrfSection.vue:34), [router/index.js:7](C:/Users/User/Desktop/кодекс/vue-site/src/router/index.js:7)

3. Кнопки в финальном блоке имеют `href="#"`, то есть выглядят как ключевые CTA, но ничего не делают. Это ломает доверие к интерфейсу.  
   [06FinalSection.vue:41](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/06FinalSection.vue:41)

1. Перегруженный фон+анимация в секциях 3 и 6 конкурирует с текстом (особенно карточки и lead-тексты). Визуально стильно, но readability местами проседает.  
   [03DavvideoSection.vue:95](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/03DavvideoSection.vue:95), [03DavvideoSection.vue:394](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/03DavvideoSection.vue:394), [06FinalSection.vue:14](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/06FinalSection.vue:14)

2. Производительность: hero-video + `preload="auto"` + множественные непрерывные анимации дорожек (steps-анимация) — риск для слабых девайсов.  
   [01PrivVideoSection.vue:9](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/01PrivVideoSection.vue:9), [03DavvideoSection.vue:181](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/03DavvideoSection.vue:181), [06FinalSection.vue:96](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/06FinalSection.vue:96)

3. Декоративные уголки сильно вынесены за границы и в ряде блоков перетягивают внимание с контента (особенно на узких экранах).  
   [base.css:34](C:/Users/User/Desktop/кодекс/vue-site/src/styles/base.css:34), [base.css:36](C:/Users/User/Desktop/кодекс/vue-site/src/styles/base.css:36), [03DavvideoSection.vue:245](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/03DavvideoSection.vue:245)

## Низкий приоритет (полировка)

1. Копирайт в нескольких местах с языковыми шероховатостями, что снижает “премиальность”.  
   [02Historyproect2Section.vue:7](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/02Historyproect2Section.vue:7)

2. Footer содержит placeholder-контакты/ссылки (`example`, `#`) — визуально ок, но для прод-ощущения это минус.  
   [SiteFooter.vue:16](C:/Users/User/Desktop/кодекс/vue-site/src/components/layout/SiteFooter.vue:16), [SiteFooter.vue:10](C:/Users/User/Desktop/кодекс/vue-site/src/components/layout/SiteFooter.vue:10)

3. В проекте есть неиспользуемая секция `07WhySection.vue` — повышает шум в структуре и усложняет сопровождение.  
   [07WhySection.vue:18](C:/Users/User/Desktop/кодекс/vue-site/src/components/sections/07WhySection.vue:18), [HomePage.vue:4](C:/Users/User/Desktop/кодекс/vue-site/src/pages/HomePage.vue:4)

## Что уже сделано хорошо

1. Единая цветовая система и сильная айдентика держатся через все экраны.
2. Хорошая композиционная ритмика секций (hero → story → service/video → map → moments → final).
3. В целом responsive-структура выстроена аккуратно по брейкпоинтам.


КОНТАКТЫ:
Мгди ОМСК: 
Координатор Валентин Гольштейн 7 996 397 7059

Мгди Красноярск: 
Координатор Павел Долгополов +7 913 565 6201

Мгди Пермь:
Координатор Нона Цинцадзе 89655786517

вк ссылки:
[17.04.2026 19:17] Исаев Григорий: https://vk.ru/mgdiperm
[17.04.2026 19:17] Исаев Григорий: https://vk.ru/mgdi.krsk24
[17.04.2026 19:17] Исаев Григорий: https://vk.ru/club191156935

