# Lekcja 4: Obsługa zdarzeń (Events)

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Obsługiwać zdarzenia kliknięcia
- Pracować z zdarzeniami myszy i klawiatury
- Używać delegowania zdarzeń
- Rozumieć różne rodzaje zdarzeń jQuery

---

## Czym są zdarzenia?

**Zdarzenie** to akcja, która jest wykonywana na stronie web, np.:
- Kliknięcie myszką
- Wpisanie tekstu
- Najechanie myszką na element
- Załadowanie strony

## Podstawowe zdarzenia

### .click() - Obsługa kliknięcia

```javascript
// Obsługuj kliknięcie na element
$("#myButton").click(function() {
    console.log("Przycisk został kliknięty!");
});

// Alternatywnie (nowoczesniejszy sposób)
$("#myButton").on("click", function() {
    console.log("Przycisk został kliknięty!");
});
```

```html
<button id="myButton">Kliknij mnie</button>

<script>
$(function() {
    $("#myButton").on("click", function() {
        alert("Przycisk kliknięty!");
    });
});
</script>
```

### .dblclick() - Podwójne kliknięcie

```javascript
$("#myDiv").dblclick(function() {
    $(this).hide();  // Schowaj się
});
```

### Zdarzenia myszy

```javascript
// Najechanie myszką
$("#myDiv").mouseenter(function() {
    $(this).css("background-color", "yellow");
});

// Opuszczenie myszy
$("#myDiv").mouseleave(function() {
    $(this).css("background-color", "white");
});

// Lub lepiej - .hover()
$("#myDiv").hover(
    function() {
        $(this).css("background-color", "yellow");
    },
    function() {
        $(this).css("background-color", "white");
    }
);
```

### Zdarzenia formularza

```javascript
// Focus - kliknięcie na input
$("#myInput").focus(function() {
    $(this).css("background-color", "lightyellow");
});

// Blur - opuszczenie inputu
$("#myInput").blur(function() {
    $(this).css("background-color", "white");
});

// Change - zmiana wartości select/radio/checkbox
$("#mySelect").change(function() {
    var wartosc = $(this).val();
    console.log("Nowa wartość: " + wartosc);
});

// Submit - wysłanie formularza
$("#myForm").submit(function(event) {
    event.preventDefault();  // Zapobiegaj domyślnemu wysłaniu
    console.log("Formularz został wysłany!");
});

// Keypress - wciśnięcie klawisza
$("#myInput").keypress(function(event) {
    console.log("Kod klawisza: " + event.which);
});
```

---

## Metoda .on() - Uniwersalna obsługa zdarzeń

`.on()` jest najbardziej elastyczną metodą obsługi zdarzeń:

```javascript
// Syntax
$(selector).on(event, function() { ... });

// Przykłady
$("button").on("click", function() { ... });
$("input").on("keypress", function() { ... });
$("#myDiv").on("mouseenter mouseleave", function() { ... });
```

### Wiele zdarzeń naraz

```javascript
$("#myDiv").on("mouseenter mouseleave", function() {
    $(this).toggleClass("active");
});
```

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

---

## .off() - Usuwanie obsługi zdarzeń

```javascript
// Usuń obsługę kliknięcia
$("#myButton").off("click");

// Usuń wszystkie obsługi zdarzeń
$("#myButton").off();
```

---

## Słowo kluczowe .this

W funkcji obsługi zdarzenia, `this` odnosi się do elementu, który wyzwolił zdarzenie:

```javascript
$(".button").on("click", function() {
    // this - element z klasą "button", na który kliknęliśmy
    $(this).css("background-color", "red");
    $(this).text("Kliknięty!");
});
```

```html
<button class="button">Przycisk 1</button>
<button class="button">Przycisk 2</button>

<script>
$(function() {
    $(".button").on("click", function() {
        // $(this) - przycisk na który kliknęliśmy
        $(this).css("background-color", "blue");
        $(this).text("Kliknąłeś mnie!");
    });
});
</script>
```

---

## Praktyka - Licznik kliknięć

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="counter">Kliknięcia: 0</button>

<script>
$(function() {
    var count = 0;
    
    $("#counter").on("click", function() {
        count++;
        $(this).text("Kliknięcia: " + count);
    });
});
</script>

</body>
</html>
```

---

## Ćwiczenie 1: Podstawowe zdarzenia

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .box {
            width: 100px;
            height: 100px;
            background-color: blue;
            margin: 10px;
        }
        .highlight {
            background-color: yellow !important;
            border: 2px solid red;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="box1" class="box"></div>
<div id="box2" class="box"></div>

<script>
$(function() {
    // Zadanie 1: Po kliknięciu na #box1 zmień jej background na red
    // ...
    
    // Zadanie 2: Po najechaniu myszką na #box2 dodaj klasę "highlight"
    // Po opuszczeniu myszy usuń klasę "highlight"
    // ...
    
    // Zadanie 3: Po podwójnym kliknięciu na #box1 zmień tekst na "Podwójnie kliknięty!"
    // ...
});
</script>

</body>
</html>
```

### Rozwiązanie
```javascript
$(function() {
    // Zadanie 1
    $("#box1").on("click", function() {
        $(this).css("background-color", "red");
    });
    
    // Zadanie 2
    $("#box2").hover(
        function() {
            $(this).addClass("highlight");
        },
        function() {
            $(this).removeClass("highlight");
        }
    );
    
    // Zadanie 3
    $("#box1").on("dblclick", function() {
        $(this).text("Podwójnie kliknięty!");
    });
});
```

---

## Ćwiczenie 2: Formularz z walidacją

### Polecenie

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
    // Zadanie 1: Obsługuj focus na inputach - zmień background na lightyellow
    // ...
    
    // Zadanie 2: Obsługuj blur - zmień background z powrotem na white
    // ...
    
    // Zadanie 3: Obsługuj submit - sprawdź czy pola są wypełnione
    // Jeśli nie, pokaż komunikat "Wszystkie pola wymagane!"
    // Jeśli tak, pokaż "Dane wysłane: [imię] - [email]"
    // ...
});
</script>

</body>
</html>
```

### Wskazówka
- Użyj `.val()` do pobrania wartości
- Użyj `.preventDefault()` aby zapobiec wysłaniu formularza

### Rozwiązanie
```javascript
$(function() {
    $(":text, :email").on("focus", function() {
        $(this).css("background-color", "lightyellow");
    });
    
    $(":text, :email").on("blur", function() {
        $(this).css("background-color", "white");
    });
    
    $("#myForm").on("submit", function(event) {
        event.preventDefault();
        
        var imie = $("#name").val();
        var email = $("#email").val();
        
        if (imie === "" || email === "") {
            $("#result").text("Wszystkie pola wymagane!");
        } else {
            $("#result").text("Dane wysłane: " + imie + " - " + email);
        }
    });
});
```

---

## Ćwiczenie 3: Delegowanie zdarzeń

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<ul id="myList">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

<button id="addBtn">Dodaj nowy item</button>
<button id="clearBtn">Wyczyść zaznaczenia</button>

<script>
$(function() {
    // Zadanie 1: Obsługuj kliknięcie na <li> za pomocą delegowania
    // Po kliknięciu zmień background na yellow i tekst na "Zaznaczony!"
    // ...
    
    // Zadanie 2: Po kliknięciu #addBtn dodaj nowy <li> do listy
    // Liczenie: Item 4, Item 5, etc.
    // ...
    
    // Zadanie 3: Po kliknięciu #clearBtn usuń zaznaczenia (przywróć styl)
    // ...
});
</script>

</body>
</html>
```

### Wskazówka
- Użyj `.on()` z selektorem dla delegowania: `$("#myList").on("click", "li", function() { ... })`
- Użyj `.append()` do dodawania elementów

### Rozwiązanie
```javascript
$(function() {
    var count = 4;
    
    // Zadanie 1: Delegowanie
    $("#myList").on("click", "li", function() {
        $(this).css("background-color", "yellow");
        $(this).text("Zaznaczony!");
    });
    
    // Zadanie 2: Dodaj nowy item
    $("#addBtn").on("click", function() {
        $("#myList").append("<li>Item " + count + "</li>");
        count++;
    });
    
    // Zadanie 3: Wyczyść zaznaczenia
    $("#clearBtn").on("click", function() {
        $("#myList li").css("background-color", "white");
        
        // Przywróć tekst (opcjonalnie możemy skaszerować oryginalne teksty)
        $("#myList li:contains('Zaznaczony')").each(function(index) {
            $(this).text("Item " + (index + 1));
        });
    });
});
```

---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Jak obsługiwać kliknięcia i inne zdarzenia
- Jak pracować z formularzami
- Co to jest delegowanie zdarzeń i dlaczego jest ważne
- Jak używać obiektu event
- Jak zapobiegać domyślnym zachowaniom

**Kolejna lekcja:** Efekty i animacje - nauczymy się tworzyć piękne przejścia i ruchy!
