# scalaxi
Scalaxi Docs

Для создания окна с офертой встроенных методов типа <code>context.PlatformServices.Confirm</code> оказалось недостаточно. Пришлось сверстать свою сырую html-разметку для окна. Вызвать эту сырую разметку нужно было по клику на другую сырую разметку, поэтому пришлось использовать ванильный  JavaScript в инлайн-атрибутах элемента.

Соответственно, сырая разметка-источник выглядела так:
```
<div>Нажимая "Зарегистрироваться", Вы соглашаетесь с условиями <a style="cursor: pointer;" onclick='document.getElementById("offerWidget").style.display = "block";'> оферты </a>  и  <a href = "https://www.cdek.ru/privacy_policy"> политикой обработки персональных данных</a>.</div>
```

Конечно, можно поместить поверх слова "оферта" прозрачную невидимую кнопку, прописать ей в actions функцию из скрипта и с этим как-то жить, но главный минус в том, что на фронте она может съехать с верстки, на мобильных устройствах фатальные последствия неизбежны.

Вызываемое окно пришлось расписать с инлайновыми стилями и целым ворохом костылей, но главное, что это заработало гораздо луше и ближе к верстке заказчика, чем платформенные окна Confirm и ShowDialog:
```
<div
  class="p-dialog-mask p-component-overlay p-dialog-mask-scrollblocker"
  id="offerWidget"
  style="z-index: 1100000; display: none"
>
  <style>
    ::-webkit-scrollbar {
      display: none;
    }
  </style>
  <div
    style="
      padding: 35px 32px 31px;
      isolation: isolate;
      position: absolute;
      width: 791px;
      left: calc(50% - 791px / 2 - 0.5px);
      top: 44px;
      bottom: 44px;
      background: #ffffff;
      box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.12);
      border-radius: 10px;
      margin-top: 50px;
      overflow-y: auto;
    "
  >
    <div class="p-dialog-header" b-uivyuunocn="">
      <h3 style="color: black" class="p-dialog-title" b-uivyuunocn="">
        Оферта
      </h3>
      <div
        onclick='document.getElementById("offerWidget").style.display = "none";'
        class="p-dialog-header-icons"
        b-uivyuunocn=""
        style="color: #53af55"
      >
        <button
          type="button"
          class="p-dialog-header-icon p-dialog-header-close p-link"
          b-uivyuunocn=""
        >
          <!--!--><span class="pi pi-times" b-uivyuunocn=""></span>
        </button>
      </div>
    </div>
    <div style="color: black">
      <p>
        Администрация Сервиса публикует настоящее Пользовательское соглашение,
        далее «Пользовательское соглашение», «Соглашение», либо «Договор»,
        представляющее собой публичную оферту в отношении пользователей Сервиса
        zozi.ru, далее «Пользователь». <br />Перед акцептом настоящего
        Пользовательского соглашения просим Вас внимательно ознакомиться с
        изложенными ниже условиями пользования. <br />Пользуясь услугами Сервиса
        zozi.ru (далее «Сервис»), Вы понимаете изложенные в настоящем
        Пользовательском соглашении условия и обязуетесь соблюдать их.Если Вы не
        согласны с какими-либо пунктами Пользовательского соглашения, либо они
        Вам не ясны, то Вы обязаны отказаться от использования услуг Сервиса.
        Пользование услугами Сервиса без согласия с условиями настоящего
        Пользовательского соглашения не допускается. <br />Настоящее
        Пользовательское соглашение вступает в силу с момента его акцепта
        Пользователем. <br />1. Термины и определения <br />1.1. Для целей
        настоящего Пользовательского соглашения используются следующие термины:
        Акцепт — полное и безоговорочное принятие Пользователем условий
        настоящего Пользовательского соглашения путем регистрации Пользователя
        на Сервисе zozi.ru. <br />Акция — стимулирующее мероприятие, проводимое
        в рамках Сервиса Web-сайтом Партнера и/или третьего лица и/или
        Администрацией, предоставляющее Пользователям Сервиса возможность
        приобретать товары/услуги на Web-сайте Партнера и/или третьего лица на
        льготных условиях. Подробное описание каждой Акции приводится в оферте
        данной Акции и/или на Сервисе и/или на соответствующем Web-сайте
        Партнера и/или третьего лица. Условия акции могут быть изменены и/или
        акция может быть остановлена в соответствии с пожеланиями Партнера,
        Сервиса и/или третьего лица. <br />Виртуальный счет — счет,
        предоставляемый Пользователю, привязанный к его Учетной записи,
        предназначенный для накопления Кэшбэк, полученных Пользователем от
        совершённых покупок. Кэшбэк — скидка в виде возврата части стоимости
        покупки, выплачиваемая в Российских рублях. Активация кэшбэка — процесс
        отправки Пользователя на сайт или приложение интернет-магазина для
        установки Файла cookie привязывающего покупки Пользователя к сервису
        zozi.ru. <br />Личный кабинет — унифицированная форма, предлагаемая
        Пользователю Сервиса для заполнения, и необходимая для надлежащего
        предоставления Администрацией заявленных услуг. <br />Отчет о
        совершенных покупках Пользователей Сервиса — отчет, предоставляемый
        Web-сайтом Партнера и/или третьего лица/его представителем Администрации
        Сервиса, содержащий данные о количестве Фактов покупок, совершенных
        Пользователями Сервиса с использованием Сервиса. <br />Ошибка — любой
        сбой в работе системы Администрации Сервиса, либо системе Web-сайта
        Партнера и/или третьего лица/их представителей, который может привести к
        некорректному указанию какой-либо информации на Сайте Администрации
        Сервиса или Web-сайте Партнера и/или третьего лица, либо некорректному
        отражению количества Кэшбэк на Виртуальном счете Пользователя Сервиса
        или их статуса, либо некорректному указанию информации о причитающемся
        Администрации Сервиса вознаграждении от Web-сайта Партнера и/или
        третьего лица/их представителей в Отчете о совершенных покупках
        Пользователей Сервиса. <br />Партнеры — физические и юридические лица,
        являющиеся контрагентами Администрации Сервиса, с которыми заключены
        соответствующие договоры, соглашения. <br />Плагин — расширение для
        браузера, эмулирующее переход в интернет-магазины и сервисы с сайта
        zozi.ru. С целью разрешения спорных вопросов Плагин определяет наличие
        других расширений, установленных в браузере. <br />Пользователь —
        физическое лицо, достигшее 14-ти лет, зарегистрированное на Сервисе с
        созданием Учетной записи. Пользовательское соглашение — настоящее
        Соглашение (Договор), заключаемое Сторонами в офертно-акцептной форме
        без подписания отдельного письменного документа. Посетитель — физическое
        лицо, посетившее Сервис, но не прошедшее процедуру регистрации на
        Сервисе. <br />Сервис — принадлежащий Администрации сайт в сети
        интернет, расположенный по адресу: https://zozi.ru, предоставляющий
        своим Пользователям возможность совершать покупки на Web-сайтах
        Партнеров и/или третьих лиц и получать за данные покупки денежные
        средства (Кэшбэк) на свой Виртуальный счет (RUB/Российский рубль).
        Сессия — временной интервал с момента открытия Пользователем страницы
        Web-сайта Партнера и/или третьего лица посредством перехода по
        размещенной на Сайте Администрации гиперссылки до наступления одного из
        следующих событий, закрывающих Сессию: — закрытия всех окон
        Интернет-браузера с открытой страницей Web-сайта Партнера и/или третьего
        лица; — истечения 24 часов с момента последнего взаимодействия
        Пользователя Сервиса с Web-сайтом Партнера и/или третьего лица в любом
        из окон интернет-браузера; — перезагрузки Сервера, на котором размещен
        Web-сайт Партнера и/или третьего лица и/или Сервера, на котором размещен
        Сайт Администрации Сервиса. Примечания: открытие дополнительных
        Web-страниц Web-сайта Партнера и/или третьего лица в новом окне
        Интернет-браузера не закрывает Сессию; использование гиперссылки,
        размещенной на Сайте Администрации Сервиса в Интернет-браузере другого
        типа или версии порождает новую Сессию. выход Пользователя Сервиса
        посредством нажатия ссылки «Выйти из аккаунта». Сообщения Сервиса —
        служебные сообщения, новостные сообщения, приглашения принять участие в
        Акциях, обновления, а также иные информационные сообщения, относящиеся к
        работе Сервиса и Web-сайта Партнера и/или третьего лица. Ссылка
        (гиперссылка) — объект гипертекстового документа, содержащий указатель
        на другой гипертекстовый документ или сайт и служащий для осуществления
        перехода к указанному документу или сайту. Стороны — Администрация
        Сервиса и Пользователь совместно. Условия участия (или Условия) —
        основные принципы и правила использования Сервиса, а также условия
        участия в Сервисе, представляющие собой оферту, опубликованную на
        Сервисе по адресу address.ru. Регистрация Пользователя на Сервисе с
        последующим созданием Учетной записи является акцептом Пользователя на
        опубликованную Администрацией оферту и выражает его полное согласие с
        условиями данной оферты (Пользовательского соглашения). Файл cookie —
        небольшой файл данных, хранящийся на компьютере Пользователя, содержащий
        технические неперсонифицированные данные, служащие для обеспечения
        правильной работы Сервиса. Факт покупки — совокупность следующих
        действий, совершенных Пользователем Сервиса: осуществление Пользователем
        Сервиса покупки на Web-сайте Партнера и/или третьего лица с
        использованием Сервиса, полная и надлежащая оплата покупки и ее
        получение Пользователем Сервиса, подтвержденные Web-сайтом Партнера
        и/или третьего лица или их представителями Администрации Сервиса.
        Электронная заявка — унифицированная форма, предлагаемая для заполнения
        Пользователю Сервиса, содержащая информацию, необходимую для
        осуществления платежа Пользователю Сервиса. IP-адрес — уникальный
        сетевой адрес (идентификатор) компьютера в сети Интернет. Web-страница
        (или веб-страница) — логическая единица сети Интернет, определяемая
        индивидуальным, неповторяющимся адресом (URL). Web-сайт Партнера и/или
        третьего лица — сайт в сети Интернет, принадлежащий Партнеру
        Администрации Сервиса и/или третьему лицу, с которым у Партнера
        Администрации Сервиса заключен соответствующий договор/соглашение, на
        котором представлены предлагаемые для приобретения Пользователям
        различные товары и услуги. URL — стандартизированный способ записи
        адреса ресурса в сети Интернет. Вознаграждение — вознаграждение
        Администрации Сервиса за оказание Пользователям услуг по предоставлению
        ресурсов Сервиса, которое складывается из процента от Кэшбэка,
        накопленного на Виртуальном счете Пользователя за учетный период в
        соответствии с условиями настоящего Соглашения, либо от процента с
        вывода средств пользователем (в зависимости от режима), а также от
        невостребованного Кэшбэка с виртуальных счетов удаленных Учетных
        записей. Невостребованный счет (учетные записи подлежащие удалению) —
        если пользователь не посещал личный кабинет сервиса на протяжении двух
        лет (24 месяцев), то счёт такого пользователя подлежит обнулению и
        последующему удалению. Это означает, что если вы хотите копить кэшбэк на
        счёте в течении многих лет, то вам необходимо хотя бы раз в полтора года
        заходить в личный кабинет сервиса, на счёте которого хранятся денежные
        средства. 2.Акцепт Пользовательского соглашения
      </p>
    </div>
  </div>
</div>
```
