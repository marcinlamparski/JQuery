# Lekcja 2: Selektory jQuery

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Używać podstawowych selektorów (ID, klasa, tag)
- Tworzyć zaawansowane selektory
- Kombinować selektory dla precyzyjnego wyboru
- Filtrować elementy
- Pracować z pseudo-selektorami jQuery

---

## Czym są selektory?

**Selektor** to sposób na wybranie elementów HTML, na których chcemy pracować. jQuery używa składni CSS, którą już znasz!

```javascript
// Składnia
$(selector).action();

// Przykład
$("#myDiv").hide();  // Schowaj element z ID "myDiv"
```

---

## Selektory podstawowe

### 1. Selektor ID (#)
Wybiera element o unikalnym ID:

```javascript
$("#myId").text("Zmieniony tekst");
// Wybiera: <div id="myId">
```

```html
<div id="header">
    <h1>Nagłówek</h1>
</div>

<script>
$(function() {
    $("#header").css("background-color", "lightblue");
});
</script>
```

### 2. Selektor klasy (.)
Wybiera wszystkie elementy z daną klasą:

```javascript
$(".highlight").text("Podświetlony tekst");
// Wybiera: <p class="highlight">
```

```html
<p class="highlight">Tekst 1</p>
<p class="highlight">Tekst 2</p>
<span class="highlight">Tekst 3</span>

<script>
$(function() {
    $(".highlight").css("background-color", "yellow");
});
</script>
```

### 3. Selektor elementu (tag)
Wybiera wszystkie elementy danego typu:

```javascript
$("p").text("Nowy tekst");
// Wybiera wszystkie: <p>
```

```html
<p>Paragraf 1</p>
<p>Paragraf 2</p>
<div>Div</div>

<script>
$(function() {
    $("p").css("color", "blue");
});
</script>
```

### 4. Selektor uniwersalny (*)
Wybiera WSZYSTKIE elementy HTML na stronie.

```javascript
$("*").css("margin", "0");
```

Co dokładnie wybiera

```HTML
<!DOCTYPE html>
<html>
<head>
    <title>Strona</title>
</head>
<body>
    <h1>Nagłówek</h1>
    <p>Paragraf</p>
    <div>Div</div>
</body>
</html>

<script>
$(function() {
    console.log($("*").length);  // Wypisze: ~8
    
    // Wybrane elementy:
    // <html>
    // <head>
    // <title>
    // <body>
    // <h1>
    // <p>
    // <div>
    // <script>
});
</script>
```
Przykład 1: Zmiana marginesów wszystkich elementów

```js
$("*").css("margin", "0");
$("*").css("padding", "0");
// Reset wszystkich marginesów i paddingow - typowo w CSS reset
```

Przykład 2: Dodanie granic do wszystkiego (do debugowania)

```js

$("*").css("border", "1px solid red");
// Widać teraz każdy element na stronie!
```

Przykład 3: Liczenie wszystkich elementów

```js
var count = $("*").length;
console.log("Elementów na stronie: " + count);
```

### 5. Selektory wielokrotne (,)
Wybiera elementy pasujące do któregokolwiek selektora:

```javascript
$("h1, h2, h3").css("color", "red");
// Wybiera: <h1>, <h2> i <h3>
```

---

## Selektory hierarchiczne

Pozwala na wybór elementów na podstawie ich pozycji w dokumencie.

### Selektory potomków

```javascript
$("div p")  // Wszystkie <p> wewnątrz <div>
$("#container p")  // Wszystkie <p> wewnątrz elementu z id="container"
```

```html
<div id="container">
    <p>Tekst 1</p>  ← Zostanie zaznaczony
    <section>
        <p>Tekst 2</p>  ← Również zaznaczony (potomek)
    </section>
</div>

<p>Tekst 3</p>  ← Nie będzie zaznaczony (nie w #container)

<script>
$(function() {
    $("#container p").css("color", "green");
});
</script>
```

### Selektory dzieci (>)
Wybiera bezpośrednie dzieci:

```javascript
$("#container > p")  // Tylko bezpośrednie <p> w #container
```

```html
<div id="container">
    <p>Tekst 1</p>  ← Zaznaczony (bezpośrednie dziecko)
    <section>
        <p>Tekst 2</p>  ← NIE zaznaczony (dziecko <section>)
    </section>
</div>

<script>
$(function() {
    $("#container > p").css("color", "red");
});
</script>
```

### Selektory sąsiadów

```javascript
$("h1 + p")  // <p> bezpośrednio po <h1>
$("h1 ~ p")  // Wszystkie <p> na tym samym poziomie co <h1>
```

---

## Selektory atrybutów

Wybiera elementy na podstawie atrybutów HTML.

### Podstawowe selektory atrybutów

```javascript
$("[href]")           // Elementy z atrybutem href
$("[type='text']")    // Inputy tekstowe
$("input[name='age']")  // Input o nazwie "age"
```

```html
<a href="strona.html">Link 1</a>
<a>Link bez href</a>
<input type="text" name="username">
<input type="password" name="password">

<script>
$(function() {
    // Zaznacz wszystkie elementy z href
    $("[href]").css("color", "blue");
    
    // Zaznacz tylko inputy tekstowe
    $("input[type='text']").css("background-color", "lightyellow");
});
</script>
```

### Zaawansowane selektory atrybutów

```javascript
$("[href*='facebook']")    // href zawiera "facebook"
$("[href^='https']")       // href zaczyna się od "https"
$("[href$='.pdf']")        // href kończy się na ".pdf"
$("[href!='#']")           // href nie równy "#"
```

---

## Pseudo-selektory jQuery

### Selektory pozycji

```javascript
$("p:first")      // Pierwszy <p>
$("p:last")       // Ostatni <p>
$("p:eq(2)")      // Trzeci <p> (indeks od 0)
$("p:odd")        // Wszystkie <p> na pozycjach nieparzystych
$("p:even")       // Wszystkie <p> na pozycjach parzystych
```

```html
<p>Paragraf 0 (parzysty)</p>
<p>Paragraf 1 (nieparzysty)</p>
<p>Paragraf 2 (parzysty)</p>
<p>Paragraf 3 (nieparzysty)</p>

<script>
$(function() {
    $("p:even").css("background-color", "lightgray");
    $("p:odd").css("background-color", "white");
});
</script>
```

### Selektory zawartości

```javascript
$("p:contains('hello')")    // <p> zawierające tekst "hello"
$("div:empty")              // Puste <div>
$("li:parent")              // <li> które mają dzieci
```

```html
<p>Hello World</p>
<p>Goodbye</p>
<div></div>
<div>Zawartość</div>

<script>
$(function() {
    $("p:contains('Hello')").css("color", "red");
    $("div:empty").text("To była pusta div!");
});
</script>
```

### Selektory formularzy

```javascript
$(":button")           // Wszystkie przyciski
$(":text")            // Wszystkie inputy tekstowe
$(":password")        // Wszystkie inputy hasła
$(":checkbox:checked") // Zaznaczone checkboxy
$(":radio:checked")   // Zaznaczane radio
$("option:selected")  // Zaznaczone opcje
```

```html
<form>
    <input type="text" name="username">
    <input type="password" name="password">
    <input type="checkbox" name="remember"> Zapamiętaj mnie
    <button>Wyślij</button>
</form>

<script>
$(function() {
    $(":button").css("background-color", "blue").css("color", "white");
    $(":checkbox:checked").css("outline", "2px solid green");
});
</script>
```

---

## Łańcuchowanie selektorów

Możesz łączyć wiele selektorów, aby być bardziej precyzyjnym:

```javascript
// Paragraf w div z ID "main" i klasą "important"
$("#main div p.important")

// Input tekstowy o ID "search"
$("input[type='text']#search")

// Wszystkie zaznaczone checkboxy w formularzu
$("#myForm :checkbox:checked")
```

---

## Łączy selektorów - praktyka

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="main">
    <div class="section">
        <h2>Sekcja 1</h2>
        <p class="important">Ważny tekst 1</p>
        <p>Zwykły tekst 1</p>
    </div>
    
    <div class="section">
        <h2>Sekcja 2</h2>
        <p class="important">Ważny tekst 2</p>
        <p>Zwykły tekst 2</p>
    </div>
</div>

<script>
$(function() {
    // Zaznacz wszystkie paragrafy z klasą "important" w #main
    $("#main p.important").css("color", "red").css("font-weight", "bold");
    
    // Zaznacz wszystkie h2 w sekcjach
    $("#main .section h2").css("border-bottom", "2px solid blue");
});
</script>

</body>
</html>
```

---

## Ćwiczenie 1: Podstawowe selektory

### Polecenie
Utwórz plik HTML z następującą strukturą i napisz selektory jQuery:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie Selektory 1</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="header">
    <h1>Moja strona</h1>
</div>

<div id="main">
    <p class="important">Tekst ważny 1</p>
    <p>Tekst zwykły 1</p>
    <p class="important">Tekst ważny 2</p>
    <p>Tekst zwykły 2</p>
</div>

<script>
$(function() {
    // Zadanie 1: Zaznacz #header i zmień background na lightblue
    // ...
    
    // Zadanie 2: Zaznacz wszystkie paragrafy z klasą "important" i ustaw kolor na red
    // ...
    
    // Zadanie 3: Zaznacz wszystkie paragrafy i ustaw font-size na 18px
    // ...
});
</script>

</body>
</html>
```

### Wskazówki
- Pamiętaj o `$("#id")` dla ID
- Pamiętaj o `$(".class")` dla klas
- Możesz łączyć selektory np. `$("#main p")`



---

## Ćwiczenie 2: Zaawansowane selektory

### Polecenie
Pracuj z poniższą tabelą i napisz selektory:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie Selektory 2</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<table id="students">
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
    <tr>
        <td>Anna</td>
        <td>4.0</td>
    </tr>
</table>

<script>
$(function() {
    // Zadanie 1: Zaznacz wszystkie <tr> z indeksem parzystym i zmień background
    // ...
    
    // Zadanie 2: Zaznacz pierwszy <tr> i ustaw background na gold
    // ...
    
    // Zadanie 3: Zaznacz ostatni <tr> i zmień kolor tekstu na green
    // ...
    
    // Zadanie 4: Zaznacz komórkę zawierającą "Maria" i ustaw font-weight na bold
    // ...
});
</script>

</body>
</html>
```

### Wskazówki
- `:even` i `:odd` dla pozycji
- `:first` i `:last` dla pierwszego/ostatniego
- `:contains()` do wyszukiwania tekstu
- `td` to komórka tabeli


---

## Ćwiczenie 3: Hierarchia elementów

### Polecenie
Stwórz strukturę HTML i zaznacz elementy używając selektorów hierarchicznych:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie Selektory 3</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="container">
    <div class="box">
        <h2>Box 1</h2>
        <p>Paragraf bezpośrednio w box</p>
        <section>
            <p>Paragraf w sekcji</p>
        </section>
    </div>
    
    <div class="box">
        <h2>Box 2</h2>
        <p>Inny paragraf</p>
    </div>
</div>

<script>
$(function() {
    // Zadanie 1: Zaznacz TYLKO bezpośrednie <p> w .box (nie te w section)
    // Powinno zaznączyć 2 paragrafy
    // ...
    
    // Zadanie 2: Zaznacz WSZYSTKIE <p> w #container (wszędzie)
    // Powinno zaznączyć 3 paragrafy
    // ...
    
    // Zadanie 3: Zaznacz wszystkie <h2> i ustaw kolor na blue
    // ...
});
</script>

</body>
</html>
```

### Wskazówki
- `>` wybiera tylko bezpośrednie dzieci
- Spacja wybiera wszystkich potomków na każdym poziomie


```

---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Jak używać selektory ID, klasy i tagi
- Jak wybierać elementy hierarchicznie
- Jak używać pseudo-selektorów
- Jak tworzyć zaawansowane selektory atrybutów
- Jak łączyć selektory dla precyzyjnego wyboru

**Kolejna lekcja:** Manipulacja DOM - nauczymy się zmieniać zawartość, atrybuty i strukturę HTML!

---

## Zasoby dodatkowe

- [jQuery Selectors](https://api.jquery.com/category/selectors/)
- [CSS Selectors Reference](https://www.w3schools.com/cssref/css_selectors.php)

[miejsce na pliki kl IV](https://www.dropbox.com/request/TCdWyGukVwbNmVAXBCPe)
