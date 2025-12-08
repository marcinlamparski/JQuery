# Lekcja 042: Obsługa zdarzeń - Część 2 (Delegowanie i zaawansowane)

## Cele lekcji

Po ukończeniu tej lekcji będziesz potrafić:
- Rozumieć delegowanie zdarzeń
- Obsługiwać zdarzenia na elementach dodanych dynamicznie
- Pracować z obiektem Event
- Zapobiegać domyślnym zachowaniom
- Usuwać obsługę zdarzeń

---

## Delegowanie zdarzeń

Delegowanie pozwala obsługiwać zdarzenia na elementach dodanych dynamicznie!

### Problem bez delegowania

```javascript
// ❌ To NIE będzie działać dla elementów dodanych później
$(".item").click(function() {
    console.log("Item kliknięty");
});

// Jeśli dodamy nowy element:
$("#list").append('<li class="item">Nowy element</li>');
// Ten nowy element NIE będzie reagować na kliknięcie!
```

### Rozwiązanie - delegowanie

```javascript
// ✅ To będzie działać dla wszystkich elementów, nawet dodanych później
$("#list").on("click", ".item", function() {
    console.log("Item kliknięty");
});

// Teraz nowe elementy także będą reagować:
$("#list").append('<li class="item">Nowy element</li>');
```

### Praktyka delegowania

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<ul id="list">
    <li class="item">Item 1</li>
    <li class="item">Item 2</li>
</ul>

<button id="addBtn">Dodaj item</button>

<script>
$(function() {
    // Delegowanie - .item w #list
    $("#list").on("click", ".item", function() {
        $(this).css("background-color", "yellow");
    });
    
    // Dodawanie nowych itemów
    var count = 3;
    $("#addBtn").on("click", function() {
        $("#list").append('<li class="item">Item ' + count + '</li>');
        count++;
    });
});
</script>

</body>
</html>
```

---

## Obiekt Event

Funkcje obsługujące zdarzenia otrzymują obiekt `event`:

```javascript
$("#myButton").on("click", function(event) {
    // event.type - typ zdarzenia ("click", "keypress", etc.)
    console.log("Typ zdarzenia: " + event.type);
    
    // event.target - element który wyzwolił zdarzenie
    console.log("Element: " + event.target);
    
    // event.preventDefault() - zapobiegaj domyślnemu działaniu
    event.preventDefault();
    
    // event.stopPropagation() - nie propaguj zdarzenia wyżej
    event.stopPropagation();
});
```

### preventDefault() - Zapobieganie domyślnemu działaniu

```javascript
// Zapobiegaj wysłaniu formularza
$("#myForm").on("submit", function(event) {
    event.preventDefault();
    console.log("Wysłanie zablokowane!");
});

// Zapobiegaj przejściu do linku
$("#myLink").on("click", function(event) {
    event.preventDefault();
    console.log("Przejście do linku zablokowane!");
});
```

### stopPropagation() - Zatrzymanie propagacji

```javascript
// Zdarzenia "bąbelkują" (propagują) w górę DOM
$("#child").on("click", function(event) {
    event.stopPropagation();
    console.log("Zdarzenie NIE przejdzie wyżej");
});

$("#parent").on("click", function() {
    console.log("To się nie wywoła");
});
```

---

## .off() - Usuwanie obsługi zdarzeń

```javascript
// Usuń obsługę kliknięcia
$("#myButton").off("click");

// Usuń wszystkie obsługi zdarzeń
$("#myButton").off();
```

---

## Ćwiczenia

### Zadanie 1: Delegowanie - Dodawanie i obsługa elementów

Stwórz listę `<ul>` z kilkoma elementami `<li>`, przycisk "Dodaj" i przycisk "Usuń zaznaczenia".
- Po kliknięciu na `<li>` zmienia się jego kolor na żółty
- Po kliknięciu "Dodaj", dodaj nowy element do listy (element powinien też być klikowalny!)
- Po kliknięciu "Usuń zaznaczenia", przywróć oryginalny kolor wszystkich elementów

**Wskazówka:** Użyj delegowania w `.on()` z selektorem dla `<li>`

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        li {
            padding: 10px;
            margin: 5px;
            background-color: lightgray;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<ul id="myList">
    <li>Element 1</li>
    <li>Element 2</li>
    <li>Element 3</li>
</ul>

<button id="addBtn">Dodaj element</button>
<button id="clearBtn">Usuń zaznaczenia</button>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 2: preventDefault na linku

Stwórz link `<a>`, który normalnie przeszedłby na Google. Po kliknięciu na niego, zamiast przechodzić do Google, pokaż komunikat "Link został zablokowany!".

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<a id="googleLink" href="https://google.com">Idź do Google</a>
<div id="message"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 3: preventDefault na formularzu

Stwórz formularz z polami imię i email. Po wysłaniu formularza (zamiast go wysyłać), pokaż komunikat:
"Dane wysłane: [imię] - [email]"

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<form id="myForm">
    <input type="text" id="name" placeholder="Imię" required>
    <input type="email" id="email" placeholder="Email" required>
    <button type="submit">Wyślij</button>
</form>

<div id="result"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 4: event.type

Stwórz przycisk. Po kliknięciu, pokaż w `<div>` jaki typ zdarzenia został wyzwolony.

**Wskazówka:** Użyj `event.type` aby uzyskać typ zdarzenia

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="myBtn">Kliknij mnie</button>
<div id="info"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 5: event.target

Stwórz kilka przycisków. Po kliknięciu na każdy, pokaż jego ID w `<div>`.

**Wskazówka:** Możesz użyć `$(event.target).attr("id")` aby uzyskać ID elementu

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="btn1">Przycisk 1</button>
<button id="btn2">Przycisk 2</button>
<button id="btn3">Przycisk 3</button>
<div id="info"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 6: Usuwanie obsługi zdarzeń

Stwórz przycisk z dwoma przyciskami pomocniczymi: "Włącz kliknięcie" i "Wyłącz kliknięcie".
- Domyślnie, po kliknięciu głównego przycisku, pokaż komunikat "Przycisk kliknięty!"
- Po kliknięciu "Wyłącz kliknięcie", usunięcie obsługi zdarzenia
- Po kliknięciu "Włącz kliknięcie", ponownie dodaj obsługę zdarzenia

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="mainBtn">Główny przycisk</button>
<button id="toggleOn">Włącz kliknięcie</button>
<button id="toggleOff">Wyłącz kliknięcie</button>
<div id="message"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 7: stopPropagation()

Stwórz zagnieżdżone elementy div: zewnętrzny i wewnętrzny. Przyczep obsługę zdarzeń do obydwu.
- Po kliknięciu na zewnętrzny: pokaż "Kliknięty zewnętrzny div"
- Po kliknięciu na wewnętrzny: pokaż "Kliknięty wewnętrzny div" i zapobiegaj propagacji do zewnętrznego

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        #outer {
            width: 300px;
            height: 300px;
            background-color: lightblue;
            padding: 20px;
            cursor: pointer;
        }
        #inner {
            width: 150px;
            height: 150px;
            background-color: lightcoral;
            cursor: pointer;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="outer">
    Zewnętrzny
    <div id="inner">Wewnętrzny</div>
</div>
<div id="message"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 8: Dynamiczne dodawanie i obsługa z delegowaniem

Stwórz aplikację do-do:
- Lista z elementami
- Przycisk "Dodaj zadanie"
- Każde zadanie powinno być klikalny (zaznaczenie poprzez zmianę koloru)
- Przycisk "Wyczyść wszystkie zaznaczenia"

**Wskazówka:** Pamiętaj że nowe elementy dodane dynamicznie muszą być obsłużone przez delegowanie!

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .task {
            padding: 10px;
            margin: 5px;
            background-color: white;
            border: 1px solid gray;
            cursor: pointer;
        }
        .task.done {
            background-color: lightgreen;
            text-decoration: line-through;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<input type="text" id="taskInput" placeholder="Nowe zadanie">
<button id="addTaskBtn">Dodaj</button>
<button id="clearTasksBtn">Wyczyść zaznaczenia</button>

<div id="tasks"></div>

<script>
$(function() {
    var taskCount = 1;
    
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 9: Walidacja formularza z preventDefault

Stwórz formularz z polami: imię, email, hasło. Przy wysłaniu:
- Jeśli któreś pole jest puste, pokaż komunikat błędu i zapobiegaj wysłaniu
- Jeśli hasło ma mniej niż 6 znaków, pokaż błąd
- Jeśli wszystko OK, pokaż "Formularz wysłany poprawnie!"

**Wskazówka:** Użyj `.length > 0` aby sprawdzić czy element istnieje

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<form id="registerForm">
    <input type="text" id="name" placeholder="Imię" required>
    <input type="email" id="email" placeholder="Email" required>
    <input type="password" id="password" placeholder="Hasło" required>
    <button type="submit">Zarejestruj</button>
</form>

<div id="error" style="color: red;"></div>
<div id="success" style="color: green;"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 10: Kombinacja zdarzeń - Interaktywna lista

Stwórz interaktywną listę:
- Lista produktów z przyciskami "Usuń" przy każdym
- Przycisk "Dodaj produkt" (pyta o nazwę)
- Po najechaniu na produkt, zmień kolor tła
- Po kliknięciu "Usuń", usuń produkt z listy
- Liczyć liczbę produktów i wyświetlać na górze

**Wskazówka:** Delegowanie będzie potrzebne dla przycisków dodanych dynamicznie!

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .product {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            margin: 5px;
            background-color: white;
            border: 1px solid gray;
        }
        .product:hover {
            background-color: #f0f0f0;
        }
        .delete-btn {
            background-color: red;
            color: white;
            border: none;
            padding: 5px 10px;
            cursor: pointer;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<h2>Produkty: <span id="count">0</span></h2>
<button id="addProductBtn">Dodaj produkt</button>

<div id="productList"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

## Podsumowanie

✅ W tej lekcji nauczyłeś się:
- Co to jest delegowanie zdarzeń i dlaczego jest ważne
- Jak obsługiwać zdarzenia na elementach dodanych dynamicznie
- Jak pracować z obiektem Event
- Jak zapobiegać domyślnym zachowaniom z `.preventDefault()`
- Jak zatrzymać propagację zdarzeń z `.stopPropagation()`
- Jak usuwać obsługę zdarzeń z `.off()`

**Gratulacje!** Ukończyłeś lekcję o zdarzeniach w jQuery. Możesz teraz tworzyć interaktywne strony internetowe!

**Następny temat:** Efekty i animacje!
