Чтобы создать модальное окно с платформенными кнопками, сырой html-компонент использовать нельзя. Чтобы разместить на компоненте кнопки, он должен быть панелью или чем-то подобным.
Но сделать панель с <code>position: absolute;</code>, <code>box-shadow</code> и другими необходимыми css-параметрами невозможно, по крайней мере платформенными способами. 
Как же быть?

Создадим панель с указанным заказчиком фигме css-атрибутами. В консоли разработчика она будет выглядеть так:
```
<div
  id="4e5ced6e-4ac9-41e8-90df-de5b3ccfecd9"
  style="
    padding: 24px 24px 24px 24px;
    width: 600px;
    flex-basis: auto;
    border-radius: 12px 12px 12px 12px;
    background-color: #ffffffff;
    flex-direction: column;
  "
  class="dynamic-component dynamic-panel dynamic-content-container"
  b-j0thnc85bb=""
>
  <!--!--><!--!-->
  <div
    id="c7cf9105-cf91-4f18-aafe-60d7ce1ba47b"
    class="dynamic-component bindable-property dynamic-raw-html"
    style=""
    b-b876jhrjnf=""
  >
    <!--!-->
    <h4
      style="font-weight: 700; font-size: 20px; line-height: 28px; color: black"
    >
      Вы точно хотите отменить изменения?
    </h4>
  </div>
  <!--!--><!--!-->
  <div
    id="53191f45-7195-47e8-9969-f6d7470f988b"
    class="dynamic-component bindable-property dynamic-raw-html"
    style=""
    b-b876jhrjnf=""
  >
    <!--!-->
    <div
      style="
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 24px;
        color: black;
      "
    >
      Вы действительно хотите удалить изменения без возможности восстановления?
    </div>
  </div>
  <!--!--><!--!-->
  <div
    id="a87c563d-9caf-4de1-8a3d-19f260fe8b00"
    style="
      margin: 30px 0px 0px 0px;
      background-color: #ffffffff;
      flex-direction: row;
    "
    class="dynamic-component dynamic-panel dynamic-content-container"
    b-j0thnc85bb=""
  >
    <!--!--><!--!--><style b-4mda96z8eu="">
      [data-prefix-id="sp-a1c131c8-ecfd-4d95-829e-3b18f46028f4"].p-button:enabled:hover {
        background-color: #ffffffff !important;
      }</style
    ><button
      id="a1c131c8-ecfd-4d95-829e-3b18f46028f4"
      data-prefix-id="sp-a1c131c8-ecfd-4d95-829e-3b18f46028f4"
      type="button"
      class="p-button p-component dynamic-component icon-left"
      style="
        width: 100px;
        height: 36px;
        flex-basis: auto;
        border-top: 1px solid;
        border-right: 1px solid;
        border-left: 1px solid;
        border-bottom: 1px solid;
        border-radius: 10px 10px 10px 10px;
        background-color: #ffffffff;
        border-color: #069798ff !important;
        color: #069798ff;
        color: #069798ff;
      "
      b-4mda96z8eu=""
    >
      <span class="p-button-label" style="color: #069798ff" b-4mda96z8eu=""
        >ОТМЕНА</span
      ></button
    ><!--!--><!--!--><button
      id="3cba578d-1530-41fc-8f69-4ad3f9ea62e9"
      data-prefix-id="sp-3cba578d-1530-41fc-8f69-4ad3f9ea62e9"
      type="button"
      class="p-button p-component dynamic-component icon-left"
      style="
        margin: 0px 0px 0px 10px;
        width: 200px;
        height: 36px;
        flex-basis: auto;
        background-color: #069798ff;
        border-color: #069798ff !important;
      "
      b-4mda96z8eu=""
    >
      <span class="p-button-label" style="" b-4mda96z8eu="">ПОДТВЕРДИТЬ</span>
    </button>
  </div>
</div>
```

Видно, что у элемента в html, сгенерированном платформой, есть class, id и style. Class единый для всех панелей, id меняется с каждой перезагрузкой страницы. Остается только инлайновый стиль, с его помощью можно сделать селектор для css. Стили можно прописать в сыром html-элементе с таким содержанием:
```
<style>
  div[style*="padding: 24px 24px 24px 24px; width: 600px; flex-basis: auto; border-radius: 12px 12px 12px 12px; background-color: #FFFFFFFF; flex-direction: column;"] {
    position: absolute;
    width: 600px;
    height: 208px;
    left: 420px;
    top: 408px;
    background: #ffffff;
    box-shadow: 0px 20px 40px -5px rgba(0, 54, 159, 0.2);
    border-radius: 12px;
    z-index: 10000;
  }
</style>
```
Результатом в платформе будет такое отображение:
![alt text](https://github.com/gleb-skobinsky/scalaxi/blob/main/modal_in_studio.png?raw=true)

Отлично. Теперь панель выглядит как модальное окно с тенью. Для большей красоты добавим сырой html с фоном, который будет отображаться одновременно с модалкой:
```
<div
  style="
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 9999;
    background-color: rgba(0, 0, 0, 0.4);
  "
></div>
```

```diff
- ВАЖНО! После редактирования html-элемента надо снять галочку с Visible. Рендеринг сырого html прямо в студии может привести к тому, что весь интерфейс студии будет перекрыт маской, и с этим ничего нельзя будет сделать. 
```

В конце для открытия и закрытия модального окна нам нужно дополнить Component Script соответствующими функциями и прописать их в Actions кнопок.
```
import clr
clr.AddReference("System.Reactive")
import System
clr.ImportExtensions(System)
from System import ObservableExtensions

context.Properties.StackPanel_527.Visible = False
context.Properties.RawHtml_026.Visible = False

def showModalConfirmation(*args, **kwargs):
    context.Properties.StackPanel_527.Visible = True
    context.Properties.RawHtml_026.Visible = True

def hideModalConfirmation(*args, **kwargs):
    context.Properties.StackPanel_527.Visible = False
    context.Properties.RawHtml_026.Visible = False
    
def hideAndNavigate(*args, **kwargs):
    context.Properties.StackPanel_527.Visible = False
    context.Properties.RawHtml_026.Visible = False
    context.Commands.NavigationBack()
```

Стоит заметить, что прежде чем выполнить переход назад по истории браузера, нужно закрыть и модалку, и ее фон. Если компонент состоит из множества страниц, открытие одной из страниц не приведет к новому выполнению скрипта, и модалка останется открытой при следующем открытии страницы.
