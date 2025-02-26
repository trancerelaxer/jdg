# Рутинные операции ИП (ежемесячно) с использованием infakt.pl

Disclaimer: подразумевается, что список активностей ИП-шника по учету деятельности на Ryczałt включает следующие типичные операции:

1. выставление 1 или нескольких фактур (инвойсов)
1. оплата налогов
1. составление декларации ZUS DRA и оплата взносов в ZUS
1. получение оплаты и учет курсовых разниц

Данный документ описывает шаги в программе infakt.pl, необходимые для выполнения операций из списка выше.
Вы должны уже знать свою ставку Ryczałt (обычно это 12% для программистов, 15% для прожект менеджеров,
8.5% для мануальных тестировщиков), перед тем как начинать вести деятельность, выясните Вашу ставку
в компетентных органах.

Зарегистрируйтесь в infakt по моей [ссылке][24] и получите 10% скидку на первую оплату (или пользуйтесь бесплатно).

Вот [тут][3] можно посмотреть минимальную настройку для infakt.pl.

## Выставление фактуры

В последний день месяца (если у вас с заказчиком договоренность на помесячную оплату), или по факту выполнения (отгрузки) работ необходимо сгенерировать и выставить фактуру заказчику. Для этого перейдите в раздел [Przychody -> Faktury][1] и нажать кнопку **Nowa faktura (dawny rachunek)**.

![new_fakture.png][2]

То же самое можно получить из списка контрагентов:

**Przychody -> Klienti -> Nowa faktura**

для выбранного заказчика, либо из списка услуг:

**Przychody -> Produkty**, чекнуть нужную услугу, и выбрать **Nowa faktura**, выбираем Faktura VAT.

В новой фактуре выбираем/корректируем необходимые поля (если не выбрано):

1. заказчика (из списка)
2. дату оказания услуги (последний день месяца либо дату фактической услуги, если они нерегулярны)
3. номер банковского счета (если больше одного)
4. услугу
5. количество "услуги" (если почасовая, то кол-во отработанных часов, если фиксированная ставка, то оставляем 1, так как сумма нетто уже есть ставка)

![4]

Нажимаете кнопку **Zapisz fakturę** для сохранения данных. Фактура записана!

> Важно: На этом этапе фактура еще не участвует в расчете налоговой базы за выбранный месяц (пока она находится в статусе `SZKIC`). Для того чтобы фактура попала в зачет, необходимо ее напечатать или выслать клиенту.

Для этого нужно в [списке фактур][1] выбрать нужную фактуру, и выбрать **Drukuj** либо **Wyślij e-mailem**. Правда в этом случае нет возможности выбрать язык фактуры (TODO: возможно какая-то настройка на это влияет).

Для возможности выбора языка фактуры надо открыть саму фактуру (щелкнув на нее), и оттуда выбрать **Drukuj fakturę**.

![5]

Ссылка на фактуру придет на почту и сама PDF откроется в новом окне.

После печати статус фактуры сменяется на `WYDRUKOWANO` и она начинает считаться в налог на следующий месяц и в ZUS.

![6]

## Оплата налогов

> Убедитесь что все фактуры добавлены и в статусе `WYDRUKOWANO` или `WYSŁANO`, а так же все курсовые разницы за отчетный период внесены и учтены.

*(Подразумевается что вы знаете номер своего налогового счета. См [тут](taxes.md#Как узнать свой счет для оплаты налогов). Infakt получает номер счета автоматически при настройке)*

До 20го числа каждого месяца (по состоянию на июль 2022) необходимо оплатить налог. В infakt в разделе [Księgowość -> Przegląd][7] отображает сумму для уплаты в текущем месяце исходя из выставленных фактур и внесенных курсовых разниц.

Есть два варианта оплаты:

1. вручную - из своего банковского приложения
1. с помощью infakt

Вторая опция платная, стоимость зависит от суммы оплаты (что-то в районе 3-5 зл сам налог). Однако она самая простая и удобная, необходимо просто нажать **Opłać z inFakt** и завершить платеж с помощью интересующих способов оплаты.

![9]

Оплата вручную происходит в банковском приложении.

На примере PKO: Выполните Przelew Podatkowy

1. выберите секцию `Pozostałe`
2. вводите в поиске `PPE`
3. введите номер своего налогового счета
4. введите за какой период оплачивается налог
5. выберите в списке Typ identyfikatora `NIP`
6. введите свой номер NIP

Выберите счет с которого платить (имеет смысл платить с фирмового, так как в банках движение по счету может быть условием бесплатности пакета), введите сумму платежа со страницы infakt и совершите платеж.

По окончанию отметьте налог как оплаченный.

![10]
## Составление декларации ZUS DRA и оплата взносов в ZUS

*(Подразумевается что вы знаете номер своего микросчета ZUS. См детали как настроить [тут](infakt_settings.md#Настройка данных ZUS))*

До 20го числа каждого месяца (по состоянию на июль 2022) необходимо оплатить складку ZUS и отправить декларацию. Как и в случае с налогами, есть те же две опции для оплаты. Для платежей в ZUS комиссия infakt немного меньше (1-2 зл).

Для оплаты напрямую через приложение банка необходимо выполнить Przelew Krajowy, выбрать счет, с которого оплачивать (как писал выше, имеет смысл платить с фирмового):

1. ввести получателя
2. ввести номер своего микросчета ZUS
3. Tytul указать "SKLADKA ZUS 22M06" (пометить период, за который осуществляется платеж)

Ввести сумму со странички infakt и совершить платеж.

![11]

По окончанию отметьте складку как оплаченную.

Для генерации декларации ZUS(файла ZUS DRA) пройдите к нужной складке в списке складок (`Przejdź do składki`).

![12]

1. Имеет смысл (для истории) прикрепить чек оплаты ZUS к записи в infakt (`Dodaj załącznik`)
2. Нажмите `Pobierz ZUS DRA` чтобы скачать файл DRA

![13]

Скачанный файл можно импортировать на портале ZUS. Альтернативно, можно создать такую же декларацию руками, но импорт файла немного быстрее.

Для импорта файла нужно зайти на портал ZUS, перейти на закладку [ePłatnik][14] в раздел Dokumenty и там выбрать Import KEDU

![15]

Проходим Dalej до шага 2 (`Wybór pliku do importu i generacja dokumentów synchronizujących`), нажимаем `Wybierz plik...` и выберите скачаный файл, и переходим на шаг 3 (`Utworzenie i walidacja dokumentów`).

![16]

По какой-то причине кнопка `Veryfikuj` не обновляет статус документов и показывает ошибку, так что можно

1. выбрать DRA и нажать `Edytuj`, в открывшемся окне нажать `Sprawdź` для валидации и вывода отчета. Чаще всего все будет все хорошо и можно закрыть редактор без изменений.
2. нажать `Zakończ` чтобы сохранить документы в папку `Dokumenty robocze`.

![17]

1. Если по какой-то причине статут документа не OK - нажмите `Weryfikuj`
2. Если статус документа OK - нажмите `Zatwierdź`

![18]

Нажимаем `Wyślij`, подписываем документ (например, profilem zaufanym ePUAP) и на этом все. Документ должен появиться в папке `Dokumenty wysłane`.

## Получение оплаты и учет курсовых разниц

При получении оплаты в иностранной валюте могут возникать курсовые разницы. Закон предписывает учитывать курсовые разницы. Учитывать ли только положительные разницы или и отрицательные тоже - мнения расходятся. Сам [infakt.pl][19] советует вносить как положительную, так и отрицательную курсовую разницу. Тут стоит каждому для себя решить какие разницы учитывать.

Для учета курсовых разниц нужно знать курс (`К1`), по которому выставлена фактура, и курс нацбанка Польши (`К2`) на последний рабочий день, предшествующий дате поступления оплаты. Если валюта с фирмового счета продается позже, то в момент продажи валюты может возникать еще один курс (`К3`). Он, как и в случае с поступлением оплаты, считается на предыдущий рабочий день от даты перевода или продажи. Перевод иностранной валюты с валютного счета JDG на личный валютный счет не приводит к возникновению курсовой разницы, поскольку вывод этих средств не связан с предпринимательской деятельностью. Вот [тут][20] и [тут][21] есть калькуляторы курсовых разниц, если лень самому считать.

Для внесения курсовой разницы (`K2` != `K1`, или `K3` != `K2`), необходимо добавить `Dowód wewnętrzny`. Для этого переходим в [Przychody -> Faktury][1], и там:

1. кликаем по "бургер-кнопке"
2. выбираем `Dowód wewnętrzny`

![22]

Тут выбираем:

1. `Pozostałe przychody`
2. вписываем `dodatnia różnica kursowa` или `ujemna różnica kursowa` в зависимости от курсовой разницы
3. вводим сумму курсовой разницы (со знаком минус если она отрицательная)
4. опционально можно добавить детали по курсам, которые считали

![23]

Записываем изменения и документ сразу начинает участвовать в расчете налоговой базы.

[1]: https://app.infakt.pl/app/faktury
[2]: images/infakt_routine/new_fakture.png
[3]: infakt_settings.md
[4]: images/infakt_routine/new_fakture_2.png
[5]: images/infakt_routine/drukuj_fakture.png
[6]: images/infakt_routine/ksiegowosc_przeglad.png
[7]: https://app.infakt.pl/app/ksiegowosc
[8]: https://www.podatki.gov.pl/generator-mikrorachunku-podatkowego
[9]: images/infakt_routine/podatek_zryczaltowany.png
[10]: images/infakt_routine/podatek_zryczaltowany_pko.png
[11]: images/infakt_routine/zus_pko.png
[12]: images/infakt_routine/ksiegowosc_przeglad_2.png
[13]: images/infakt_routine/zus_dra.png
[14]: https://www.zus.pl/portal/eplMain.npi
[15]: images/infakt_routine/zus_import_kedu.png
[16]: images/infakt_routine/zus_import_kedu_2.png
[17]: images/infakt_routine/zus_import_kedu_3.png
[18]: images/infakt_routine/zus_import_kedu_4.png
[19]: https://www.infakt.pl/blog/jak-rozliczyc-roznice-kursowe-na-ryczalcie/
[20]: https://kalkulatory2.gofin.pl/Kalkulator-roznic-kursowych-przychodow,12.html
[21]: https://kalkulatory2.gofin.pl/Kalkulator-roznic-kursowych-od-srodkow-wlasnych,12.html
[22]: images/infakt_routine/dowod_wewnetrzny.png
[23]: images/infakt_routine/dodatnia_ruznica.png
[24]: https://www.infakt.pl/polecam/sobolevbel
