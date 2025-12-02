# Lekcja 3: Manipulacja DOM - Zawartość i atrybuty

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Zmieniać zawartość HTML elementów
- Pobierać i ustawiać atrybuty
- Modyfikować klasy CSS
- Zmieniać style CSS
- Pracować z wartościami formularz

---

## Metody do zmiany zawartości

### .text() - Zmiana tekstu

Ustawia lub pobiera **tylko tekst** (bez HTML):

```javascript
// Pobranie tekstu
var tekst = $("#myDiv").text();

// Ustawienie tekstu
$("#myDiv").text("Nowy tekst");
```

```html
<div id="myDiv">
    <p>Stary tekst</p>
</div>

<script>
$(function() {
    $("#myDiv").text("Całkowicie nowy tekst");
    // Wynik: <div id="myDiv">Całkowicie nowy tekst</div>
    // Tag <p> został usunięty!
});
</script>
```

### .html() - Zmiana HTML

Ustawia lub pobiera **zawartość HTML** (z tagami):

```javascript
// Pobranie HTML
var html = $("#myDiv").html();

// Ustawienie HTML
$("#myDiv").html("<strong>Ważny tekst</strong>");
```

```html
<div id="myDiv">
    <p>Stary tekst</p>
</div>

<script>
$(function() {
    $("#myDiv").html("<p>Nowy paragraf</p><p>Drugi paragraf</p>");
    // Wynik: <div id="myDiv">
    //     <p>Nowy paragraf</p>
    //     <p>Drugi paragraf</p>
    // </div>
});
</script>
```

### Różnica między .text() a .html()

```javascript
// text() - usuwa wszystkie tagi HTML
$("div").text("<b>To nie będzie pogrubione</b>");
// Wynik: <div>&lt;b&gt;To nie będzie pogrubione&lt;/b&gt;</div>

// html() - interpretuje tagi HTML
$("div").html("<b>To będzie pogrubione</b>");
// Wynik: <div><b>To będzie pogrubione</b></div>
```

### .append() i .prepend() - Dodawanie zawartości

```javascript
// Dodaj na końcu
$("#myDiv").append("<p>Nowy paragraf na końcu</p>");

// Dodaj na początek
$("#myDiv").prepend("<p>Nowy paragraf na początek</p>");
```

```html
<div id="myDiv">
    <p>Istniejący tekst</p>
</div>

<script>
$(function() {
    $("#myDiv").append("<hr>");
    // Wynik: <div><p>Istniejący tekst</p><hr></div>
    
    $("#myDiv").prepend("<h3>Tytuł</h3>");
    // Wynik: <div><h3>Tytuł</h3><p>Istniejący tekst</p><hr></div>
});
</script>
```

---

## Metody do pracy z atrybutami

### .attr() - Pobieranie i ustawianie atrybutów

```javascript
// Pobranie atrybutu
var href = $("a").attr("href");

// Ustawienie atrybutu
$("a").attr("href", "https://example.com");

// Ustawienie wielu atrybutów naraz
$("img").attr({
    "src": "image.jpg",
    "alt": "Opis obrazka",
    "width": "200"
});
```

```html
<img id="myImg" src="old.jpg" alt="Stary opis">
<a id="myLink" href="old.html">Stary link</a>

<script>
$(function() {
    // Zmień źródło obrazka
    $("#myImg").attr("src", "new.jpg");
    
    // Zmień URL linku
    $("#myLink").attr("href", "new.html");
    
    // Zmień wiele atrybutów
    $("#myImg").attr({
        "src": "best.jpg",
        "alt": "Nowy opis"
    });
});
</script>
```

### .removeAttr() - Usuwanie atrybutów

```javascript
// Usuń atrybut
$("img").removeAttr("alt");
```

---

## Praca z klasami CSS

### .addClass() - Dodawanie klasy

```javascript
$("#myDiv").addClass("highlight");
$("p").addClass("text-large"); // Dodaj klasę do wszystkich <p>
```

### .removeClass() - Usuwanie klasy

```javascript
$("#myDiv").removeClass("highlight");
```

### .toggleClass() - Przełączanie klasy

Dodaje klasę jeśli jej nie ma, usuwa jeśli jest:

```javascript
$("#myDiv").toggleClass("active");
```

### .hasClass() - Sprawdzenie klasy

```javascript
if ($("#myDiv").hasClass("active")) {
    console.log("Element ma klasę active");
}
```

### Praktyk z klasami

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .highlight {
            background-color: yellow;
            font-weight: bold;
        }
        .selected {
            border: 2px solid red;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<p id="para1" class="highlight">Paragraf 1</p>
<p id="para2">Paragraf 2</p>

<button id="btnToggle">Przełącz klasę selected</button>

<script>
$(function() {
    $("#btnToggle").on("click", function() {
        $("#para1").toggleClass("selected");
    });
});
</script>

</body>
</html>
```

---

## Zmiana stylów CSS

### .css() - Zmiana stylów

```javascript
// Zmiana jednego stylu
$("#myDiv").css("color", "red");

// Zmiana wielu stylów naraz
$("#myDiv").css({
    "color": "blue",
    "background-color": "yellow",
    "font-size": "20px"
});

// Pobranie wartości stylu
var kolor = $("#myDiv").css("color");
```

```html
<div id="box">Pudełko</div>

<script>
$(function() {
    // Metoda 1: Jeden styl
    $("#box").css("background-color", "lightblue");
    
    // Metoda 2: Wiele stylów
    $("#box").css({
        "color": "white",
        "padding": "20px",
        "border": "2px solid navy",
        "text-align": "center"
    });
});
</script>
```

### .css() vs .addClass()

```javascript
// .css() - style inline
$("div").css("color", "red");
// Wynik: <div style="color: red;">

// .addClass() - nowa klasa CSS
$("div").addClass("red-text");
// Wynik: <div class="red-text">
// (o ile w CSS jest: .red-text { color: red; })
```

**Kiedy używać czego?**
- `.css()` - do szybkich zmian, dynamicznych wartości
- `.addClass()` - do organizacji kodu, wielokrotnych stylów

---

## Praca z wartościami formularza

### .val() - Pobieranie i ustawianie wartości

```javascript
// Pobranie wartości
var wartość = $("#myInput").val();

// Ustawienie wartości
$("#myInput").val("Nowa wartość");
```

```html
<input type="text" id="username" placeholder="Użytkownik">
<input type="password" id="password" placeholder="Hasło">
<textarea id="message"></textarea>
<select id="country">
    <option value="">Wybierz kraj</option>
    <option value="pl">Polska</option>
    <option value="en">Anglia</option>
</select>

<script>
$(function() {
    // Ustaw wartości
    $("#username").val("Jan");
    $("#password").val("tajne123");
    $("#message").val("Wiadomość testowa");
    $("#country").val("pl");
});
</script>
```

### Specjalne przypadki formularza

```javascript
// Checkbox - czy jest zaznaczony?
if ($("#remember").is(":checked")) {
    console.log("Checkbox zaznaczony");
}

// Radio - która opcja?
var selected = $("input[name='gender']:checked").val();

// Select - wybrana opcja
var kraj = $("#country").val();
```

---

## Łańcuchowanie operacji

jQuery pozwala na łańcuchowanie - wykonywanie wielu operacji na raz:

```javascript
$("#myDiv")
    .css("color", "blue")
    .addClass("highlight")
    .text("Nowy tekst");
// Równoważne z trzema osobnymi wierszami:
// $("#myDiv").css("color", "blue");
// $("#myDiv").addClass("highlight");
// $("#myDiv").text("Nowy tekst");
```

---

## Ćwiczenie 1: Zmiana zawartości

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie - Zawartość</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="container">
    <p>Stary tekst</p>
</div>

<button id="btnText">Zmień na tekst</button>
<button id="btnHTML">Zmień na HTML</button>
<button id="btnAppend">Dodaj tekst</button>

<script>
$(function() {
    // Zadanie 1: Po kliknięciu #btnText zmień tekst na "Tekst został zmieniony"
    // ...
    
    // Zadanie 2: Po kliknięciu #btnHTML zmień HTML na "<strong>HTML został zmieniony</strong>"
    // ...
    
    // Zadanie 3: Po kliknięciu #btnAppend dodaj "<p>Nowy paragraf</p>"
    // ...
});
</script>

</body>
</html>
```



---

## Ćwiczenie 2: Atrybuty i style

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .highlight { background-color: yellow; }
        .large { font-size: 20px; }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<img id="myImg" src="old.jpg" alt="Stary obraz">
<a id="myLink" href="old.html">Link</a>

<button id="btnImage">Zmień obrazek</button>
<button id="btnLink">Zmień link</button>
<button id="btnStyle">Zmień styl</button>

<script>
$(function() {
    // Zadanie 1: Po kliknięciu #btnImage zmień src na "new.jpg" i alt na "Nowy obraz"
    // ...
    
    // Zadanie 2: Po kliknięciu #btnLink zmień href na "new.html"
    // ...
    
    // Zadanie 3: Po kliknięciu #btnStyle dodaj klasy "highlight" i "large" do obu elementów
    // ...
});
</script>

</body>
</html>
```

### Wskazówka
- Użyj `.attr()` do zmiany atrybutów
- Użyj `.addClass()` do dodawania klas
- Możesz łańcuchować operacje


---

## Ćwiczenie 3: Formularz

### Polecenie

Stwórz prosty formularz i manipuluj jego wartościami:

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<input type="text" id="name" placeholder="Imię">
<input type="email" id="email" placeholder="Email">
<select id="country">
    <option value="">Wybierz</option>
    <option value="pl">Polska</option>
    <option value="en">Anglia</option>
</select>

<button id="btnFill">Wypełnij dane</button>
<button id="btnClear">Wyczyść dane</button>
<button id="btnShow">Pokaż dane</button>

<div id="output"></div>

<script>
$(function() {
    // Zadanie 1: Po kliknięciu #btnFill wypełnij wszystkie pola testowymi danymi
    // ...
    
    // Zadanie 2: Po kliknięciu #btnClear wyczyść wszystkie pola
    // ...
    
    // Zadanie 3: Po kliknięciu #btnShow pokaż wartości w #output
    // ...
});
</script>

</body>
</html>
```

### Wskazówka
- Użyj `.val()` do pobierania/ustawiania wartości
- Możesz łączenia wiele `.val()` razem


---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Różnica między .text() i .html()
- Jak dodawać zawartość za pomocą append/prepend
- Jak pracować z atrybutami HTML
- Jak manipulować klasami CSS
- Jak zmieniać style bezpośrednio
- Jak pracować z formularzami

**Kolejna lekcja:** Obsługa zdarzeń - nauczymy się reagować na kliknięcia, hovering i inne akcje użytkownika!
