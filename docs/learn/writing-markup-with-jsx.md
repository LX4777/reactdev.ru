# Написание разметки с помощью JSX

**JSX** - это расширение синтаксиса для JavaScript, позволяющее писать HTML-подобную разметку внутри файла JavaScript. Хотя существуют и другие способы написания компонентов, большинство разработчиков React предпочитают лаконичность JSX, и большинство кодовых баз используют именно его.

!!!tip "Вы узнаете"

    -   Почему React смешивает разметку с логикой рендеринга
    -   Чем JSX отличается от HTML
    -   Как отображать информацию с помощью JSX

## JSX: размещение разметки в JavaScript

Веб был построен на HTML, CSS и JavaScript. В течение многих лет веб-разработчики хранили содержимое в HTML, дизайн в CSS, а логику в JavaScript - часто в отдельных файлах! Контент размечался внутри HTML, а логика страницы жила отдельно в JavaScript:

<figure markdown>
![HTML разметка с фиолетовым фоном и div с двумя дочерними тегами: p и form.](writing_jsx_html.webp)
<figurecaption>HTML</figurecaption>
</figure>

<figure markdown>
![Три JavaScript обработчика с желтым фоном: onSubmit, onLogin и onClick.](writing_jsx_js.webp)
<figurecaption>JavaScript</figurecaption>
</figure>

Но по мере того, как веб становился все более интерактивным, логика все больше определяла содержание. JavaScript стал отвечать за HTML! Вот почему **в React логика рендеринга и разметка живут вместе в одном месте - в компонентах.**.

<figure markdown>
![React компонент с HTML и JavaScript из предыдущих примеров. Имя функции - Sidebar, которая вызывает функцию isLoggedIn, выделенную желтым цветом. Внутри функции, выделенной фиолетовым, находится тег p из предыдущего примера и тег Form, ссылающийся на компонент, показанный на следующей диаграмме.](writing_jsx_sidebar.webp)
<figurecaption markdown>`Sidebar.js` React компонент</figurecaption>
</figure>

<figure markdown>
![React компонент со смешанными HTML и JavaScript из предыдущих примеров. Имя функции - Form, содержащая два обработчика onClick и onSubmit, выделенные желтым цветом. За обработчиками следует HTML, выделенный фиолетовым цветом. HTML содержит элемент формы с вложенным элементом ввода, каждый из которых имеет свойство onClick.](writing_jsx_form.webp)
<figurecaption markdown>`Form.js` React компонент</figurecaption>
</figure>

Совместное использование логики рендеринга и разметки кнопки гарантирует, что они будут синхронизироваться друг с другом при каждом редактировании. И наоборот, детали, не связанные между собой, такие как разметка кнопки и разметка боковой панели, изолированы друг от друга, что делает более безопасным изменение любой из них по отдельности.

Каждый компонент React - это функция JavaScript, которая может содержать некоторую разметку, которую React отображает в браузере. Компоненты React используют расширение синтаксиса под названием JSX для представления этой разметки. JSX очень похож на HTML, но он немного строже и может отображать динамическую информацию. Лучший способ понять это - преобразовать некоторую HTML-разметку в JSX-разметку.

!!!note ""

    JSX и React - это две разные вещи. Их часто используют вместе, но вы _можете_ использовать их независимо.

<!-- 0001.part.md -->

## Преобразование HTML в JSX

Предположим, что у вас есть некоторый (совершенно правильный) HTML:

<!-- 0002.part.md -->

```html
<h1>Hedy Lamarr's Todos</h1>
<img
    src="https://i.imgur.com/yXOvdOSs.jpg"
    alt="Hedy Lamarr"
    class="photo"
/>
<ul>
    <li>Invent new traffic lights</li>
    <li>Rehearse a movie scene</li>
    <li>Improve the spectrum technology</li>
</ul>
```

<!-- 0003.part.md -->

И вы хотите поместить его в свой компонент:

<!-- 0004.part.md -->

```js
export default function TodoList() {
  return (
    // ???
  )
}
```

<!-- 0005.part.md -->

Если вы скопируете и вставите его как есть, он не будет работать:

=== "App.js"

    ```js
    export default function TodoList() {
    return (
    	// This doesn't quite work!
    	<h1>Hedy Lamarr's Todos</h1>
    	<img
    	src="https://i.imgur.com/yXOvdOSs.jpg"
    	alt="Hedy Lamarr"
    	class="photo"
    	>
    	<ul>
    	<li>Invent new traffic lights
    	<li>Rehearse a movie scene
    	<li>Improve the spectrum technology
    	</ul>
    );
    }
    ```

=== "Результат"

    ![Результат](writing-markup-with-jsx-1.png)

<!-- 0009.part.md -->

Это связано с тем, что JSX более строгий и имеет несколько больше правил, чем HTML! Если вы прочитаете приведенные выше сообщения об ошибках, они подскажут вам, как исправить разметку, или вы можете следовать руководству, приведенному ниже.

!!!note ""

    В большинстве случаев экранные сообщения об ошибках React помогут вам найти причину проблемы. Прочитайте их, если вы застряли!

## Правила JSX

### 1. Возвращает один корневой элемент

Чтобы вернуть несколько элементов из компонента, **оберните их одним родительским тегом.**.

Например, вы можете использовать `<div>`:

<!-- 0010.part.md -->

```js
<div>
  <h1>Hedy Lamarr's Todos</h1>
  <img
    src="https://i.imgur.com/yXOvdOSs.jpg"
    alt="Hedy Lamarr"
    class="photo"
  >
  <ul>
    ...
  </ul>
</div>
```

<!-- 0011.part.md -->

Если вы не хотите добавлять в разметку лишние `<div>`, вместо них можно написать `<>` и <code>&lt;/&gt;</code>:

<!-- 0012.part.md -->

```js
<>
  <h1>Hedy Lamarr's Todos</h1>
  <img
    src="https://i.imgur.com/yXOvdOSs.jpg"
    alt="Hedy Lamarr"
    class="photo"
  >
  <ul>
    ...
  </ul>
</>
```

<!-- 0013.part.md -->

Этот пустой тег называется _[Фрагмент](../reference/Fragment.md)_. Фрагменты позволяют группировать элементы, не оставляя никаких следов в HTML-дереве браузера.

!!!note "Почему несколько тегов JSX должны быть обернуты?"

    JSX выглядит как HTML, но под капотом он преобразуется в обычные объекты JavaScript. Вы не можете вернуть два объекта из функции, не обернув их в массив. Это объясняет, почему вы также не можете вернуть два тега JSX, не обернув их в другой тег или фрагмент.

### 2. Закройте все теги

JSX требует, чтобы теги были явно закрыты: самозакрывающиеся теги, такие как `<img>` должны стать `<img />`, а оберточные теги типа `<li>oranges` должны быть записаны как `<li>oranges</li>`.

Так выглядит закрытый образ Хеди Ламарр и элементы списка:

<!-- 0014.part.md -->

```js
<>
    <img
        src="https://i.imgur.com/yXOvdOSs.jpg"
        alt="Hedy Lamarr"
        class="photo"
    />
    <ul>
        <li>Invent new traffic lights</li>
        <li>Rehearse a movie scene</li>
        <li>Improve the spectrum technology</li>
    </ul>
</>
```

<!-- 0015.part.md -->

### 3. camelCase <s>всё</s> большинство вещей!

JSX превращается в JavaScript, а атрибуты, записанные в JSX, становятся ключами объектов JavaScript. В ваших собственных компонентах вы часто захотите считать эти атрибуты в переменные. Но JavaScript имеет ограничения на имена переменных. Например, их имена не могут содержать тире или быть зарезервированными словами, такими как `class`.

Вот почему в React многие атрибуты HTML и SVG записываются в camelCase. Например, вместо `stroke-width` вы используете `strokeWidth`. Поскольку `class` является зарезервированным словом, в React вместо него пишется `className`, названный в честь [соответствующего свойства DOM](https://developer.mozilla.org/docs/Web/API/Element/className):

<!-- 0016.part.md -->

```js
<img
    src="https://i.imgur.com/yXOvdOSs.jpg"
    alt="Hedy Lamarr"
    className="photo"
/>
```

<!-- 0017.part.md -->

Вы можете найти все эти атрибуты в списке атрибутов компонентов DOM. Если вы ошибетесь, не волнуйтесь - React выведет сообщение с возможным исправлением в [консоль браузера](https://developer.mozilla.org/docs/Tools/Browser_Console).

!!!warning "Внимание"

    По историческим причинам атрибуты [`aria-*`](https://developer.mozilla.org/docs/Web/Accessibility/ARIA) и [`data-*`](https://developer.mozilla.org/docs/Learn/HTML/Howto/Use_data_attributes) записываются как в HTML с тире.

### Совет: Используйте JSX-конвертер

Преобразование всех этих атрибутов в существующей разметке может быть утомительным! Мы рекомендуем использовать [конвертер](https://transform.tools/html-to-jsx) для перевода существующих HTML и SVG в JSX. Конвертеры очень полезны на практике, но все же стоит понимать, что происходит, чтобы вам было удобно писать JSX самостоятельно.

Вот ваш конечный результат:

<!-- 0018.part.md -->

=== "App.js"

    ```js
    export default function TodoList() {
    	return (
    		<>
    			<h1>Hedy Lamarr's Todos</h1>
    			<img
    				src="https://i.imgur.com/yXOvdOSs.jpg"
    				alt="Hedy Lamarr"
    				className="photo"
    			/>
    			<ul>
    				<li>Invent new traffic lights</li>
    				<li>Rehearse a movie scene</li>
    				<li>Improve the spectrum technology</li>
    			</ul>
    		</>
    	);
    }
    ```

=== "Результат"

    ![Результат](writing-markup-with-jsx-2.png)

<!-- 0021.part.md -->

!!!note "Итоги"

    Теперь вы знаете, зачем существует JSX и как использовать его в компонентах:

    -   Компоненты React группируют логику рендеринга вместе с разметкой, потому что они связаны.
    -   JSX похож на HTML, с некоторыми отличиями. При необходимости вы можете использовать [конвертер](https://transform.tools/html-to-jsx).
    -   Сообщения об ошибках часто указывают вам правильное направление для исправления разметки.

## Задача

### 1. Преобразование HTML в JSX

Этот HTML был вставлен в компонент, но это не валидный JSX. Исправьте это:

=== "App.js"

    ```
    export default function Bio() {
    	return (
    		<div class="intro">
    			<h1>Welcome to my website!</h1>
    		</div>
    		<p class="summary">
    			You can find my thoughts here.
    			<br><br>
    			<b>And <i>pictures</b></i> of scientists!
    		</p>
    	);
    }
    ```

=== "Результат"

    ![Результат](writing-markup-with-jsx-3.png)

<!-- 0025.part.md -->

Делать ли это вручную или с помощью конвертера - решать вам!

<!-- 0026.part.md -->

???success "Показать решение"

    === "App.js"

    	```js
    	export default function Bio() {
    		return (
    			<div>
    				<div className="intro">
    					<h1>Welcome to my website!</h1>
    				</div>
    				<p className="summary">
    					You can find my thoughts here.
    					<br />
    					<br />
    					<b>
    						And <i>pictures</i>
    					</b> of scientists!
    				</p>
    			</div>
    		);
    	}
    	```

    === "Результат"

    	![Результат](writing-markup-with-jsx-4.png)

## Ссылки

-   [https://react.dev/learn/writing-markup-with-jsx](https://react.dev/learn/writing-markup-with-jsx)
