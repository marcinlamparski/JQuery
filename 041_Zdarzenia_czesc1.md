# Lekcja 041: Obsługa zdarzeń - Część 1 (Zdarzenia podstawowe)

## Cele lekcji

Po ukończeniu tej lekcji będziesz potrafić:
- Obsługiwać zdarzenia kliknięcia
- Pracować z zdarzeniami myszy
- Obsługiwać zdarzenia formularza
- Używać metody `.on()` do obsługi zdarzeń

---

## Czym są zdarzenia?

**Zdarzenie** to akcja, która jest wykonywana na stronie web, np.:
- Kliknięcie myszką
- Wpisanie tekstu
- Najechanie myszką na element
- Załadowanie strony

---

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

### Słowo kluczowe .this

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

## Ćwiczenia

### Zadanie 1: Proste kliknięcie

Stwórz przycisk, który po kliknięciu zmienia swój kolor na czerwony.

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="colorBtn">Zmień kolor</button>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 2: Hover na elemencie

Stwórz element `<div>`, który po najechaniu myszką zmienia kolor na żółty, a po opuszczeniu wraca do białego.

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        #box {
            width: 200px;
            height: 200px;
            background-color: white;
            border: 2px solid black;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="box"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 3: Podwójne kliknięcie

Stwórz element, który schowuje się (hide) po podwójnym kliknięciu.

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="disappear">Kliknij mnie dwukrotnie, aby zniknąć</div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 4: Zmiana tekstu przycisku

Stwórz przycisk, który zmienia swój tekst na "Kliknięty!" po kliknięciu.

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="textBtn">Kliknij mnie</button>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 5: Obsługa inputu - Focus i Blur

Stwórz pole tekstowe, które zmienia kolor tła na `lightyellow` gdy otrzyma fokus, i na `white` gdy go utraci.

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<input type="text" id="myInput" placeholder="Wpisz coś">

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 6: Dodawanie klasy CSS

Stwórz przycisk z dwoma elementami div. Po kliknięciu przycisku, pierwszy div powinien dodać sobie klasę `highlight`.

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .highlight {
            background-color: yellow;
            border: 3px solid red;
            padding: 10px;
        }
        .box {
            width: 100px;
            height: 100px;
            background-color: lightblue;
            margin: 10px;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="addClassBtn">Dodaj klasę</button>
<div id="box1" class="box"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 7: Usuwanie klasy CSS

Rozwiń zadanie 6: dodaj przycisk "Usuń klasę", który będzie usuwać klasę `highlight` z elementu.

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .highlight {
            background-color: yellow;
            border: 3px solid red;
            padding: 10px;
        }
        .box {
            width: 100px;
            height: 100px;
            background-color: lightblue;
            margin: 10px;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="addClassBtn">Dodaj klasę</button>
<button id="removeClassBtn">Usuń klasę</button>
<div id="box1" class="box"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 8: Toggle klasy CSS

Stwórz przycisk, który przełącza klasę `highlight` na div (jeśli istnieje, usuń; jeśli nie istnieje, dodaj).

**Wskazówka:** Użyj metody `.toggleClass()`

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .highlight {
            background-color: yellow;
            border: 3px solid red;
        }
        .box {
            width: 100px;
            height: 100px;
            background-color: lightblue;
            margin: 10px;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="toggleBtn">Przełącz klasę</button>
<div id="box1" class="box"></div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 9: Zmiana CSS właściwości

Stwórz element, który po kliknięciu zmienia wiele CSS właściwości jednocześnie:
- background-color na green
- color na white
- padding na 20px

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="box">Kliknij mnie</div>

<script>
$(function() {
    // Napisz kod tutaj
});
</script>

</body>
</html>
```

---

### Zadanie 10: Formularz z focus i blur

Stwórz formularz z polami imię i email. Dla każdego pola:
- Po focus: zmień border na `2px solid blue`
- Po blur: zmień border z powrotem na `1px solid gray`

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        input {
            padding: 8px;
            margin: 10px;
            border: 1px solid gray;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<form>
    <input type="text" id="name" placeholder="Imię">
    <input type="email" id="email" placeholder="Email">
</form>

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
- Obsługiwać zdarzenia kliknięcia (click, dblclick)
- Pracować z zdarzeniami myszy (hover, mouseenter, mouseleave)
- Obsługiwać zdarzenia formularza (focus, blur)
- Używać metody `.on()` do obsługi zdarzeń
- Manipulować klasami CSS za pomocą zdarzeń
- Pracować ze słowem kluczowym `this`

**Następna lekcja:** Część 2 - Delegowanie zdarzeń i zaawansowane techniki!
