# Vue 
<a href="https://ru.vuejs.org/">https://ru.vuejs.org/</a>
***
[Компоненты](#components)
[Директивы](#directives)





***
VueJS представляет CLI для установки vue и начала работы с активацией сервера. 
* npm install --global vue-cli

***
 Создания проекта с использованием Webpack
* vue init webpack myproject

***
Запуск
* cd myproject
* npm run dev

***

## Компоненты <a name="components"></a>
```javascript
// Определяем новый компонент под именем todo-item
Vue.component('todo-item', {
  template: '<li>Это одна задача в списке</li>'
})
```
Теперь его можно использовать в шаблоне другого компонента:

```html
<ol>
  <!-- Создаём экземпляр компонента todo-item -->
  <todo-item></todo-item>
</ol>
```
Когда экземпляр Vue создан, он добавляет все свойства, найденные в опции data, в систему реактивности Vue. Но! Свойства в data будут реактивными, только если они существовали при создании экземпляра. Т.е. необходимо сразу установить начальное значение.

Каждый экземпляр Vue при создании проходит через последовательность шагов инициализации :
1) настраивается наблюдение за данными;
2) компилируется шаблон;
3) монтируется экземпляр в DOM;
4) обновляется DOM при изменении данных.

<img alt='Жизненный цикл компанента' src="manual/images/life.png"/>


## Директивы <a name="directives"></a>

Директивы — это специальные атрибуты с префиксом ```v-```. В качестве значения они принимают одно выражение JavaScript (за исключением v-for). Директива реактивно применяет к DOM изменения при обновлении значения этого выражения. 

Начиная с версии 2.6.0, можно использовать JavaScript-выражение в аргументе директивы, заключив его в квадратные скобки:

```html
<a v-bind:[attributeName]="url"> ... </a>
```

**v-bind** - используется для добавления атрибутов,  реактивного обновления атрибутов HTML.

```html
<button v-bind:disabled="isButtonDisabled">Кнопка</button>
```
Также есть одна особенность, если значением isButtonDisabled будет null, undefined или false, то атрибут disabled не добавится в элемент ```<button>```.

**v-if** - используется

**v-for** - использует данные из массива, для отображения списков.

```app4.todos.push({ text: 'Profit' })``` добавит новый элемент в список.
```html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
```javascript
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Изучить JavaScript' },
      { text: 'Изучить Vue' },
      { text: 'Создать что-нибудь классное' }
    ]
  }
})
```

**v-once** -

**v-on** - используется для отслеживания событий.
```html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Перевернуть сообщение</button>
</div>
```
```javascript
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Привет, Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('');
    }
  }
});
```

**v-model** - связывает элементы форм и состояние приложения.
```html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
```javascript
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Привет, Vue!'
  }
});
```

**v-once** -  переменная подменяется однократно, не обновиляется при изменении данных. Но это повлияет сразу на все связанные переменные в рамках данного элемента
```html
<span v-once>Это сообщение никогда не изменится: {{ msg }}</span>
```

**v-html** - для подстановки HTML.
```html
<p>Директива v-html: <span v-html="rawHtml"></span></p>
```
Содержимое тега *span* будет заменено значением свойства *rawHtml*, интерпретированного как обычный HTML.  Нельзя использовать ```v-html``` для вложения шаблонов друг в друга, потому что движок шаблонов Vue не основывается на строках. 

>Динамическая отрисовка произвольного HTML-кода на сайте крайне опасна, так как может легко привести к XSS-уязвимостям. Использовать интерполяцию HTML можно только для доверенного кода, и нельзя подставлять туда содержимое, создаваемое пользователями.
