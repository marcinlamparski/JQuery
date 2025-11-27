# Lekcja 1: Wprowadzenie do jQuery

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Wyjaśnić, czym jest jQuery i dlaczego warto go używać
- Zainstalować jQuery na swoją stronę
- Napisać pierwsze skrypty jQuery
- Zrozumieć podstawową składnię biblioteki

---

## Co to jest jQuery?

**jQuery** to biblioteka JavaScript, którą napisał John Resig w 2006 roku. Jej głównym celem jest **uproszczenie pisania kodu JavaScript** i czynienie go bardziej czytelnym.

### Motto jQuery: "Write Less, Do More" (Pisz mniej, rób więcej)

```javascript
// JavaScript vanilla
document.getElementById("myButton").addEventListener("click", function() {
    document.getElementById("myDiv").style.display = "none";
});

// jQuery - znacznie krócej i przejrzystej
$("#myButton").on("click", function() {
    $("#myDiv").hide();
});
```

### Główne zalety jQuery

1. **Kompatybilność przeglądarek** - jQuery obsługuje wszystkie popularne przeglądarki
2. **Krótszy kod** - Mniej kodu do osiągnięcia tego samego rezultatu
3. **Łatwiejsze selektory** - Możliwość używania CSS do wyboru elementów
4. **Łańcuchowanie** - Możliwość łączenia wielu operacji w jedną linię
5. **Bogata dokumentacja** - Wiele przykładów i samouczków dostępnych online
6. **Wtyczki** - Rozszerzona funkcjonalność dzięki wtyczkom jQuery

### Czy jQuery jest jeszcze używane?

**TAK.** Mimo że nowoczesne frameworki (React, Vue, Angular) się rozwijają, jQuery wciąż:
- Jest używane w milionach stron internetowych
- Jest łatwe w nauce dla początkujących
- Jest idealne do małych projektów i poprawy istniejących stron
- Nauczanie jQuery uczy fundamentów DOM i JavaScriptu

---

## Instalacja jQuery

### Metoda 1: Pobranie z CDN (Content Delivery Network) - Rekomendowana

Dodaj tę linię w sekcji `<head>` lub przed zamknięciem `</body>`:

```html
<!-- Najnowsza wersja jQuery 3.x (zalecana) -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
```

### Metoda 2: Pobranie pliku

1. Przejdź na stronę [jquery.com](https://jquery.com)
2. Pobierz wersję minimalną (jquery.min.js)
3. Umieść plik w folderze projektu
4. Dodaj referencję:

```html
<script src="jquery-3.6.0.min.js"></script>
```

### Metoda 3: npm (Node Package Manager)

```bash
npm install jquery
```

---

## Podstawowa składnia jQuery

### Składnia ogólna

```javascript
$(selector).action();
```

**Wyjaśnienie:**
- `$` - Symbol jQuery (wejście do biblioteki)
- `selector` - Element HTML do wybrania (np. ID, klasa, tag)
- `action()` - Operacja do wykonania na wybranym elemencie

### Przykłady

```javascript
// Wybierz element z ID "myDiv" i ukryj go
$("#myDiv").hide();

// Wybierz wszystkie paragrafy i zmień ich tekst
$("p").text("Nowy tekst");

// Wybierz wszystkie elementy z klasą "highlight" i zmień kolor tła
$(".highlight").css("background-color", "yellow");
```
**Porównanie JQuery z querySelector w JS**

| Cecha                   | $(selector)jQuery | querySelector() | querySelectorAll() |
| ----------------------- | ----------------- | --------------- | ------------------ |
| Zwraca pierwszy element | Nie (wszystkie)   | Tak             | Nie                |
| Zwraca kolekcję         | Tak (jQuery)      | Nie             | Tak (NodeList)     |
| Pseudo-selektory jQuery | Tak               | Nie             | Nie                |
| Wbudowane metody        | Setki             | Tylko DOM API   | Podstawowe         |
| Łańcuchowanie           | Tak               | Nie             | Nie                |
| Iteracja                | .each()           | .forEach()      | .forEach()         |


|Selektory CSS - obie działają:|                        |
|-----------------|----------------------------------------------|
|$("div")|                          querySelector("div")|
|$("#myId")|                        querySelector("#myId")|
|$(".myClass")|                     querySelector(".myClass")|
|$("div.class")|                    querySelector("div.class")|

// TYLKO jQuery pseudo-selektory - querySelector nie zna:
$(":button")                       // Wszystkie przyciski
$(":text")                         // Wszystkie text inputy
$(":checked")                      // Zaznaczone checkboxy
$("li:odd")                        // Nieparzyste <li>
$("li:even")                       // Parzyste <li>
$("p:contains('hello')")          // Paragrafy zawierające 'hello'
$("div:visible")                   // Tylko widoczne divy
$(":not(.active)")                 // Elementy bez klasy active


---


## Czekanie na gotowość DOM

**Ważne!** Skrypt jQuery powinien czekać, aż cały dokument HTML się załaduje, zanim zacznie szukać elementów.

### Prawidłowy sposób

```javascript
$(document).ready(function() {
    // Tutaj umieść cały kod jQuery
    $("#myButton").click(function() {
        $("#myDiv").hide();
    });
});
```

### Krótka forma

```javascript
$(function() {
    // Równoważne z $(document).ready()
    $("#myButton").click(function() {
        $("#myDiv").hide();
    });
});
```

### Dlaczego to ważne?

Jeśli kod jQuery będzie uruchamiany zanim elementy HTML się załadują, skrypt ich nie znajdzie!

```javascript
// ❌ ŹLE - element może nie być załadowany
$("#myDiv").hide();

// ✅ DOBRZE - czekamy na załadowanie
$(document).ready(function() {
    $("#myDiv").hide();
});
```

---

## Twoja pierwsza strona jQuery

Utwórz plik `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Moja pierwsza strona jQuery</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<h1>Witaj w jQuery!</h1>
<button id="myButton">Kliknij mnie</button>
<div id="myDiv">
    <p>To jest tekst, który zniknie po kliknięciu przycisku.</p>
</div>

<script>
$(document).ready(function() {
    $("#myButton").on("click", function() {
        $("#myDiv").hide();
    });
});
</script>

</body>
</html>
```

---

## Porównanie: jQuery vs. Vanilla JavaScript

Aby lepiej zrozumieć moc jQuery, porównajmy ten sam kod w obu wersjach.

### Zadanie: Zmień kolor paragrafu na niebiesko

**Vanilla JavaScript:**
```javascript
const myParagraph = document.getElementById("myParagraph");
myParagraph.style.color = "blue";
```

**jQuery:**
```javascript
$("#myParagraph").css("color", "blue");
```

### Zadanie: Ukryj wszystkie elementy div

**Vanilla JavaScript:**
```javascript
const allDivs = document.querySelectorAll("div");
for (let i = 0; i < allDivs.length; i++) {
    allDivs[i].style.display = "none";
}
```

**jQuery:**
```javascript
$("div").hide();
```

---

## Ćwiczenie 1: Konfiguracja projektu

### Cel
Przygotować środowisko do pracy z jQuery.

### Polecenie
1. Utwórz folder na projekcie o nazwie `jquery-kurs`
2. Wewnątrz folderu utwórz plik `index.html`
3. Dodaj strukturę HTML z odnośnikiem do jQuery z CDN
4. Stwórz prosty przycisk i div z dowolnym tekstem
5. W skrypcie jQuery dodaj obsługę kliknięcia przycisku - po kliknięciu tekst w div powinien zmienić się na "Kliknąłeś mnie!"

### Szablon do uzupełnienia

```html
<!DOCTYPE html>
<html>
<head>
    <title>jQuery Kurs - Ćwiczenie 1</title>
    <!-- DODAJ TU LINK DO jQuery -->
</head>
<body>

<h1>Pierwsze ćwiczenie jQuery</h1>
<!-- DODAJ TU PRZYCISK O ID "btn" -->
<!-- DODAJ TU DIV O ID "message" Z TEKSTEM -->

<script>
$(function() {
    // TUTAJ NAPISZ KOD
    // Obsługuj kliknięcie przycisku i zmień tekst w div
});
</script>

</body>
</html>
```

### Wskazówka
- Użyj `.on("click", function() { ... })` do obsługi kliknięcia
- Użyj `.text("nowy tekst")` do zmiany tekstu

### Rozwiązanie (zobacz jeśli naprawdę utknąłeś)
```javascript
$(function() {
    $("#btn").on("click", function() {
        $("#message").text("Kliknąłeś mnie!");
    });
});
```

---

## Ćwiczenie 2: Wielokrotne przyciski

### Cel
Nauczyć się obsługi wielu elementów.

### Polecenie
1. Utwórz 3 przyciski z różnymi ID
2. Każdy przycisk powinien mieć inny tekst (np. "Czerwony", "Zielony", "Niebieski")
3. Kliknięcie na przycisk powinno zmienić kolor tekstu w paragrafie poniżej na odpowiadający kolor

```html
<!DOCTYPE html>
<html>
<head>
    <title>jQuery Kurs - Ćwiczenie 2</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<h1>Zmiana kolorów</h1>

<!-- DODAJ 3 PRZYCISKI -->

<p id="textToChange">Ten tekst zmieni kolor!</p>

<script>
$(function() {
    // OBSŁUGUJ KLIKNIĘCIE NA KAŻDY PRZYCISK
    // I ZMIEŃ KOLOR TEKSTU ODPOWIEDNIO
});
</script>

</body>
</html>
```

### Fragmenty kodu do pomocą
```javascript
// Zmiana koloru CSS
$("element").css("color", "red");

// Obsługa przycisku
$("#buttonId").on("click", function() {
    // kod
});
```

### Rozwiązanie
```javascript
$(function() {
    $("#redBtn").on("click", function() {
        $("#textToChange").css("color", "red");
    });
    
    $("#greenBtn").on("click", function() {
        $("#textToChange").css("color", "green");
    });
    
    $("#blueBtn").on("click", function() {
        $("#textToChange").css("color", "blue");
    });
});
```

---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Czym jest jQuery i jakie ma zalety
- Jak zainstalować jQuery na stronie
- Jaką składnię używa jQuery
- Dlaczego warto czekać na $(document).ready()
- Jak obsługiwać kliknięcia przycisków
- Jak zmieniać tekst i style elementów

**Kolejna lekcja:** Селектory - nauczymy się dokładnie, na ile sposobów możemy wybierać elementy HTML!

---

## Zasoby dodatkowe

- [jQuery Dokumentacja](https://api.jquery.com/)
- [jQuery Tutorial na W3Schools](https://www.w3schools.com/jquery/)
- [Try jQuery - Interaktywne tutoriale](https://try.jquery.com/)
