# Lekcja 6: Filtrowanie i nawigacja po DOM

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Filtrować elementy z zestawu zaznaczonych
- Nawigować po DOM (rodzice, dzieci, sąsiedzi)
- Pracować z metodami wyszukiwania
- Iterować po zbiorze elementów

---

## Metody filtrowania

### .filter() - Przefiltruj zaznaczone elementy

Wybiera tylko elementy, które spełniają warunek:

```javascript
// Zaznacz <p> z klasą "important"
$("p").filter(".important");

// Zaznacz <p> które zawierają "Hello"
$("p").filter(":contains('Hello')");
```

```html
<p>Tekst 1</p>
<p class="important">Ważny 1</p>
<p>Tekst 2</p>
<p class="important">Ważny 2</p>

<script>
$(function() {
    // Zaznacz tylko paragrafy z klasą "important"
    $("p").filter(".important").css("color", "red");
});
</script>
```

### .not() - Wyklucz zaznaczone elementy

Przeciwieństwo `.filter()`:

```javascript
// Zaznacz wszystkie <p> OPRÓCZ tych z klasą "important"
$("p").not(".important");
```

### .eq() - Zaznacz element po indeksie

```javascript
$("p").eq(0);  // Pierwszy <p>
$("p").eq(2);  // Trzeci <p>
$("p").eq(-1);  // Ostatni <p>
```

### .first() i .last()

```javascript
$("p").first();  // Pierwszy <p>
$("p").last();   // Ostatni <p>
```

---

## Nawigacja po DOM

### .parent() - Rodzic

```javascript
$("#child").parent();  // Bezpośredni rodzic
```

```html
<div id="parent">
    <p id="child">Tekst</p>
</div>

<script>
$(function() {
    $("#child").parent().css("border", "2px solid red");
});
</script>
```

### .parents() - Wszyscy przodkowie

```javascript
$("#child").parents();  // Wszyscy przodkowie
$("#child").parents(".container");  // Przodkowie z klasą "container"
```

### .children() - Dzieci

```javascript
$("#parent").children();  // Wszystkie bezpośrednie dzieci
$("#parent").children("p");  // Tylko dzieci <p>
```

```html
<div id="parent">
    <p>Paragraf 1</p>
    <p>Paragraf 2</p>
    <span>Span</span>
</div>

<script>
$(function() {
    // Zaznacz wszystkie paragrafy
    $("#parent").children("p").css("color", "blue");
});
</script>
```

### .find() - Wszyscy potomkowie

```javascript
$("#parent").find("p");  // Wszystkie <p> w #parent (na każdym poziomie)
```

### .next() i .prev() - Sąsiedzi

```javascript
$("#item2").next();      // Następny sąsiad
$("#item2").prev();      // Poprzedni sąsiad
$("#item2").nextAll();   // Wszyscy następni sąsiedzi
$("#item2").prevAll();   // Wszyscy poprzedni sąsiedzi
```

```html
<ul>
    <li id="item1">Item 1</li>
    <li id="item2">Item 2</li>
    <li id="item3">Item 3</li>
</ul>

<script>
$(function() {
    // Zaznacz Item 3 (następny sąsiad Item 2)
    $("#item2").next().css("color", "red");
});
</script>
```

### .siblings() - Wszyscy sąsiedzi

```javascript
$("#item2").siblings();  // Wszyscy elementy na tym samym poziomie
```

---

## Iteracja - .each()

Wykonaj funkcję dla każdego elementu:

```javascript
$("p").each(function(index, element) {
    // index - numer elementu (0, 1, 2, ...)
    // element - element HTML
    
    console.log("Paragraf " + index + ": " + $(element).text());
});
```

```html
<p>Tekst 1</p>
<p>Tekst 2</p>
<p>Tekst 3</p>

<script>
$(function() {
    $("p").each(function(index) {
        // Zmień kolor każdego paragrafu
        if (index % 2 === 0) {
            $(this).css("background-color", "yellow");
        } else {
            $(this).css("background-color", "lightblue");
        }
    });
});
</script>
```

---

## Metody wyszukiwania

### .is() - Sprawdzenie czy spełnia warunek

```javascript
if ($("#myDiv").is(".highlight")) {
    console.log("Element ma klasę highlight");
}

if ($("input").is(":checked")) {
    console.log("Input zaznaczony");
}
```

### .has() - Sprawdzenie czy zawiera

```javascript
// Zaznacz <div> które zawierają <p>
$("div").has("p");
```

---

## Łańcuchowanie nawigacji

```javascript
// Przejdź do rodzica, potem do następnego sąsiada
$("#myDiv").parent().next().css("color", "red");

// Przejdź do rodzica, znajdź wszystkie <p>, zastosuj styl
$("#myDiv").parent().find("p").css("font-weight", "bold");

// Filtruj i zmień styl
$("p").filter(".important").not(".hidden").css("color", "red");
```

---

## Praktyka - Tabela

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        table { border-collapse: collapse; }
        th, td { border: 1px solid black; padding: 10px; }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<table id="myTable">
    <tr>
        <td>Jan</td>
        <td>5.0</td>
    </tr>
    <tr>
        <td>Maria</td>
        <td>4.5</td>
    </tr>
    <tr>
        <td>Piotr</td>
        <td>3.5</td>
    </tr>
</table>

<script>
$(function() {
    // Zaznacz wszystkie <tr> i zmień background na alternate
    $("#myTable tr").each(function(index) {
        if (index % 2 === 0) {
            $(this).css("background-color", "lightgray");
        }
    });
});
</script>

</body>
</html>
```

---

## Ćwiczenie 1: Filtrowanie

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<p>Paragraf 1</p>
<p class="special">Paragraf ważny 1</p>
<p>Paragraf 2</p>
<p class="special">Paragraf ważny 2</p>
<p>Paragraf 3</p>

<button id="btnSpecial">Pokaż specjalne</button>
<button id="btnNormal">Pokaż zwykłe</button>
<button id="btnFirst">Pokaż pierwszy</button>

<script>
$(function() {
    // Zadanie 1: #btnSpecial - zaznacz i wyświetl tylko .special
    // ...
    
    // Zadanie 2: #btnNormal - zaznacz i wyświetl tylko zwykłe (nie .special)
    // ...
    
    // Zadanie 3: #btnFirst - zaznacz i wyświetl tylko pierwszy paragraf
    // ...
});
</script>

</body>
</html>
```

### Wskazówka
- Użyj `.filter()` do filtrowania
- Użyj `.not()` do wykluczenia
- Użyj `.first()` i `.eq()` do zaznaczenia indeksu

### Rozwiązanie
```javascript
$(function() {
    $("#btnSpecial").on("click", function() {
        $("p").hide();
        $("p").filter(".special").show();
    });
    
    $("#btnNormal").on("click", function() {
        $("p").hide();
        $("p").not(".special").show();
    });
    
    $("#btnFirst").on("click", function() {
        $("p").hide();
        $("p").first().show();
    });
});
```

---

## Ćwiczenie 2: Nawigacja po DOM

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="container">
    <div class="section">
        <h2 id="title1">Sekcja 1</h2>
        <p id="para1">Paragraf 1</p>
    </div>
    
    <div class="section">
        <h2 id="title2">Sekcja 2</h2>
        <p id="para2">Paragraf 2</p>
    </div>
</div>

<script>
$(function() {
    // Zadanie 1: Od #para1 przejdź do rodzica i zaznacz go
    // Zmień background na yellow
    // ...
    
    // Zadanie 2: Od #title1 zaznacz następny sąsiad (paragraf)
    // Zmień tekst na "Znaleziony paragraf"
    // ...
    
    // Zadanie 3: W #container zaznacz wszystkie <p> i pogrubij
    // ...
});
</script>

</body>
</html>
```

### Wskazówka
- `.parent()` - rodzic
- `.next()` - następny sąsiad
- `.find()` - wszystkie potomkowie

### Rozwiązanie
```javascript
$(function() {
    // Zadanie 1
    $("#para1").parent().css("background-color", "yellow");
    
    // Zadanie 2
    $("#title1").next().text("Znaleziony paragraf");
    
    // Zadanie 3
    $("#container").find("p").css("font-weight", "bold");
});
```

---

## Ćwiczenie 3: Iteracja i zmiana

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        li { padding: 5px; margin: 5px 0; }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<ul id="myList">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
    <li>Item 4</li>
    <li>Item 5</li>
</ul>

<script>
$(function() {
    // Zadanie: Użyj .each() aby:
    // 1. Dodaj do każdego <li> numer pozycji (np. "1. Item 1")
    // 2. Zaznacz nieparzyste <li> background na lightgreen
    // 3. Zaznacz parzyste <li> background na lightblue
    // ...
});
</script>

</body>
</html>
```

### Wskazówka
- `index` w `.each()` zaczyna się od 0
- `index % 2 === 0` to parzyste
- `index % 2 === 1` to nieparzyste

### Rozwiązanie
```javascript
$(function() {
    $("#myList li").each(function(index) {
        // Dodaj numer
        var numer = index + 1;
        var tekst = $(this).text();
        $(this).text(numer + ". " + tekst);
        
        // Zmień background
        if (index % 2 === 0) {
            $(this).css("background-color", "lightblue");
        } else {
            $(this).css("background-color", "lightgreen");
        }
    });
});
```

---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Jak filtrować elementy
- Jak nawigować po DOM
- Jak używać parent/children/find
- Jak iterować po zbiorach elementów
- Jak łączyć metody nawigacji

**Kolejna lekcja:** Formularze - nauczymy się pracować z formularzami i ich walidacją!
