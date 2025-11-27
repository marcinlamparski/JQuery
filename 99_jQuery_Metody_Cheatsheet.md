# Najpotrzebniejsze metody jQuery - Referencyjna lista

## 🎯 Top 30 metod jQuery które MUSISZ znać

---

## I. SELEKCJA I NAWIGACJA

### 1. `.find()` - Znajdź wszystkich potomków
```javascript
// Wszystkie <p> wewnątrz #container
$("#container").find("p");

// Równoważne:
$("#container p");
```
**Kiedy:** Szukanie zagnieżdżonych elementów
**Wydajność:** ⭐⭐⭐⭐⭐

---

### 2. `.children()` - Bezpośrednie dzieci
```javascript
// Tylko bezpośrednie <p> w #container (nie w głębi)
$("#container").children("p");
```
**Kiedy:** Tylko bezpośrednie dzieci
**Różnica od find():** Nie idzie w głąb

---

### 3. `.parent()` - Rodzic
```javascript
// Bezpośredni rodzic elementu
$("#item").parent();
```
**Kiedy:** Przejście do rodzica

---

### 4. `.siblings()` - Sąsiedzi
```javascript
// Wszystkie elementy na tym samym poziomie
$("#item2").siblings();
```
**Kiedy:** Interakcje między równorzędnymi elementami

---

### 5. `.eq()` - Element po indeksie
```javascript
// Trzeci paragraf (indeks 2)
$("p").eq(2);

// Ostatni element
$("p").eq(-1);
```
**Kiedy:** Wybór konkretnego elementu z kolekcji

---

### 6. `.filter()` - Filtruj zaznaczone
```javascript
// Tylko paragrafy z klasą "important"
$("p").filter(".important");
```
**Kiedy:** Zawężanie kolekcji

---

### 7. `.not()` - Wyklucz elementy
```javascript
// Wszystkie paragrafy OPRÓCZ tych z klasą "important"
$("p").not(".important");
```
**Kiedy:** Odwrotne filtrowanie

---

## II. MANIPULACJA ZAWARTOŚCIĄ

### 8. `.text()` - Zmiana/pobieranie tekstu
```javascript
// Pobranie
var tekst = $("#heading").text();

// Ustawienie
$("#heading").text("Nowy tekst");

// WSZYSTKIE pasujące elementy
$("p").text("Każdy p ma ten tekst");
```
**Kiedy:** Praca z tekstem (bez HTML)
**Uwaga:** Usuwa tagi HTML

---

### 9. `.html()` - Zmiana/pobieranie HTML
```javascript
// Pobranie
var html = $("#container").html();

// Ustawienie
$("#container").html("<strong>Ważny tekst</strong>");
```
**Kiedy:** Praca z HTML (z tagami)
**Uwaga:** Interpretuje tagi

---

### 10. `.append()` - Dodaj na koniec
```javascript
// Dodaj na koniec
$("#container").append("<p>Nowy paragraf</p>");
```
**Kiedy:** Dodawanie zawartości dynamicznie

---

### 11. `.prepend()` - Dodaj na początek
```javascript
// Dodaj na początek
$("#container").prepend("<h3>Nowy tytuł</h3>");
```
**Kiedy:** Dodawanie elementu na początek

---

### 12. `.remove()` - Usuń element
```javascript
// Usuń element z DOM
$("#item").remove();

// Usuń wszystkie elementy z klasą "temp"
$(".temp").remove();
```
**Kiedy:** Całkowite usuwanie elementów

---

### 13. `.empty()` - Wyczyść zawartość
```javascript
// Usuń zawartość ale nie sam element
$("#container").empty();
// <div id="container"></div> - ciągle istnieje!
```
**Kiedy:** Czyszczenie zawartości

---

## III. ATRYBUTY I KLASY

### 14. `.attr()` - Atrybuty HTML
```javascript
// Pobranie
var href = $("a").attr("href");

// Ustawienie
$("a").attr("href", "https://example.com");

// Wiele atrybutów
$("img").attr({
    "src": "image.jpg",
    "alt": "Opis",
    "width": "200"
});
```
**Kiedy:** Praca z atrybutami HTML

---

### 15. `.prop()` - Właściwości DOM
```javascript
// Zaznaczony checkbox?
if ($("input[type='checkbox']").prop("checked")) {
    console.log("Zaznaczony");
}

// Zaznacz checkbox
$("input[type='checkbox']").prop("checked", true);
```
**Kiedy:** Zaznaczenia, wyłączenia, selected
**Różnica od attr():** Dla dynamicznych właściwości

---

### 16. `.addClass()` - Dodaj klasę CSS
```javascript
// Dodaj klasę
$("#item").addClass("active");

// Wiele klas
$("#item").addClass("active highlight");
```
**Kiedy:** Zmiana wyglądu poprzez CSS

---

### 17. `.removeClass()` - Usuń klasę
```javascript
// Usuń klasę
$("#item").removeClass("active");

// Usuń wszystkie klasy
$("#item").removeClass();
```
**Kiedy:** Usuwanie stylów CSS

---

### 18. `.toggleClass()` - Przełącz klasę
```javascript
// Dodaj jeśli brak, usuń jeśli jest
$("#item").toggleClass("active");

// Przełącz na podstawie warunku
$("#item").toggleClass("active", shouldBeActive);
```
**Kiedy:** Toggle on/off

---

### 19. `.hasClass()` - Czy ma klasę?
```javascript
if ($("#item").hasClass("active")) {
    console.log("Element jest aktywny");
}
```
**Kiedy:** Sprawdzenie warunku

---

### 20. `.val()` - Wartość formularza
```javascript
// Pobranie
var imie = $("#username").val();

// Ustawienie
$("#username").val("Jan");

// U selecta - wybrana opcja
var kraj = $("#country").val();
```
**Kiedy:** Praca z formularzami

---

## IV. STYLE CSS

### 21. `.css()` - Zmieniaj styl inline
```javascript
// Pobranie
var kolor = $("#box").css("color");

// Ustawienie
$("#box").css("color", "red");

// Wiele stylów
$("#box").css({
    "color": "white",
    "background-color": "blue",
    "padding": "20px"
});
```
**Kiedy:** Dynamiczne zmiany stylów
**Uwaga:** Styl inline - ma wyższy priorytet

---

## V. ZDARZENIA

### 22. `.on()` - Obsługa zdarzeń (uniwersalna)
```javascript
// Kliknięcie
$("#button").on("click", function() {
    console.log("Kliknięto");
});

// Delegowanie - dla elementów dynamicznych
$("#container").on("click", ".item", function() {
    console.log("Item kliknięty");
});

// Wiele zdarzeń
$("#element").on("mouseenter mouseleave", function() {
    $(this).toggleClass("hover");
});
```
**Kiedy:** Obsługa zdarzeń
**Best practice:** Zawsze używaj `.on()`

---

### 23. `.click()` - Skrót dla kliknięcia
```javascript
// Obsługa kliknięcia
$("#button").click(function() {
    console.log("Kliknięto");
});

// Programowe kliknięcie
$("#button").click();
```
**Kiedy:** Szybkie obsługi kliknięć

---

### 24. `.submit()` - Obsługa formularza
```javascript
$("#form").submit(function(e) {
    e.preventDefault();  // Zapobiegaj wysłaniu
    console.log("Formularz wysłany");
});
```
**Kiedy:** Obsługa wysyłania formularza

---

### 25. `.hover()` - Najechanie myszy
```javascript
$("#element").hover(
    function() {
        $(this).addClass("hovered");
    },
    function() {
        $(this).removeClass("hovered");
    }
);
```
**Kiedy:** Efekty hover

---

### 26. `.off()` - Usuń obsługę zdarzenia
```javascript
// Usuń wszystkie handlery kliknięcia
$("#button").off("click");

// Usuń wszystkie zdarzenia
$("#button").off();
```
**Kiedy:** Czyszczenie eventów

---

## VI. EFEKTY I ANIMACJE

### 27. `.hide()` / `.show()` / `.toggle()`
```javascript
// Ukryj
$("#box").hide();

// Pokaż z animacją 500ms
$("#box").show(500);

// Przełącz
$("#box").toggle(300);
```
**Kiedy:** Prostej widoczności

---

### 28. `.fadeIn()` / `.fadeOut()` / `.fadeToggle()`
```javascript
// Pojawiaj się
$("#box").fadeIn(1000);

// Zanikaj
$("#box").fadeOut(500);

// Zanik do 50% opacności
$("#box").fadeTo(1000, 0.5);
```
**Kiedy:** Zanikające efekty

---

### 29. `.slideDown()` / `.slideUp()` / `.slideToggle()`
```javascript
// Rozwiń
$("#menu").slideDown(300);

// Zwiń
$("#menu").slideUp(300);

// Akordeon - przełącz
$("#menu").slideToggle();
```
**Kiedy:** Rozkładane menu

---

### 30. `.animate()` - Niestandardowa animacja
```javascript
// Animuj właściwości CSS
$("#box").animate({
    left: '200px',
    opacity: 0.5,
    width: '100px'
}, 1000);  // 1 sekunda

// Z callback'iem
$("#box").animate({ left: '100px' }, 1000, function() {
    console.log("Animacja gotowa!");
});
```
**Kiedy:** Złożone animacje

---

## VII. ITERACJA

### 31. `.each()` - Pętla po elementach
```javascript
// Iteruj po każdym paragrafie
$("p").each(function(index, element) {
    console.log(index + ": " + $(element).text());
});

// Użycie this
$("p").each(function() {
    $(this).addClass("processed");
});
```
**Kiedy:** Operacje na wielu elementach

---

### 32. $.each() - Pętla po danych
```javascript
// Pętla po tablicy
$.each([1, 2, 3], function(index, value) {
    console.log(index + ": " + value);
});

// Pętla po obiekcie
$.each({a: 1, b: 2}, function(key, value) {
    console.log(key + ": " + value);
});
```
**Kiedy:** Iteracja po danych (nie DOM)

---

## VIII. AJAX

### 33. $.ajax() - Asynchroniczne żądania
```javascript
$.ajax({
    url: "https://api.example.com/data",
    type: "GET",
    dataType: "json",
    success: function(data) {
        console.log("Dane:", data);
    },
    error: function() {
        console.log("Błąd");
    }
});
```
**Kiedy:** Komunikacja z serwerem

---

### 34. $.get() / $.post() - Skróty
```javascript
// GET - pobieranie danych
$.get("api/users", function(data) {
    console.log(data);
});

// POST - wysłanie danych
$.post("api/users", { name: "Jan" }, function(data) {
    console.log(data);
});
```
**Kiedy:** Szybkie AJAX żądania

---

## IX. UTILITY

### 35. $.map() - Transformuj tablicę
```javascript
var liczby = [1, 2, 3, 4];
var podwojone = $.map(liczby, function(n) {
    return n * 2;  // [2, 4, 6, 8]
});
```
**Kiedy:** Transformacja danych

---

### 36. $.grep() - Filtruj tablicę
```javascript
var liczby = [1, 2, 3, 4, 5];
var parzyste = $.grep(liczby, function(n) {
    return n % 2 === 0;  // [2, 4]
});
```
**Kiedy:** Filtrowanie tablic

---

### 37. $.inArray() - Szukaj w tablicy
```javascript
var index = $.inArray("jabłko", ["jabłko", "gruszka"]);
// index = 0 (znalezione)
// index = -1 (nie znalezione)
```
**Kiedy:** Sprawdzenie czy element w tablicy

---

## ⭐ TOP 10 NAJCZĘŚCIEJ UŻYWANE

| Lp. | Metoda | Zastosowanie |
|-----|--------|--------------|
| 1 | `.on()` | Obsługa zdarzeń |
| 2 | `.text()` / `.html()` | Zmiana zawartości |
| 3 | `.addClass()` / `.removeClass()` | Zmiana klas CSS |
| 4 | `.css()` | Zmiany stylów |
| 5 | `.val()` | Wartości formularzy |
| 6 | `.attr()` | Atrybuty HTML |
| 7 | `.append()` / `.prepend()` | Dodawanie elementów |
| 8 | `.find()` | Szukanie elementów |
| 9 | `.each()` | Iteracja po kolekcji |
| 10 | $.ajax() | Żądania do serwera |

---

## 📊 Wydajność i praktyka

### Łańcuchowanie (SZYBKO - jedna iteracja DOM)
```javascript
$("#item")
    .addClass("active")
    .css("color", "red")
    .text("Zmieniony");
```

### Bez łańcuchowania (WOLNO - cztery iteracje)
```javascript
$("#item").addClass("active");
$("#item").css("color", "red");
$("#item").text("Zmieniony");
$("#item").show();
```

---

## 🎓 Szybka referencyjna tabela

```
SELEKCJA          ZAWARTOŚĆ         ATRYBUTY          ZDARZENIA
.find()           .text()           .attr()           .on()
.children()       .html()           .prop()           .click()
.parent()         .append()         .addClass()       .submit()
.siblings()       .prepend()        .removeClass()    .hover()
.eq()             .remove()         .toggleClass()    
.filter()         .empty()          .css()            
.not()            .val()            .hasClass()       

EFEKTY            ITERACJA          AJAX              UTILITY
.show()           .each()           $.ajax()          $.map()
.hide()           $.each()          $.get()           $.grep()
.toggle()                           $.post()          $.inArray()
.fadeIn()                           $.load()          
.fadeOut()                                            
.slideDown()                                          
.animate()                                            
```

---

## 💡 Poradnik dla nauczyciela

### Phase 1 (Lekcja 1-2): Basics
Ucz tylko: `.find()`, `.text()`, `.html()`, `.addClass()`, `.on()`

### Phase 2 (Lekcja 3-5): Intermediate
Dodaj: `.css()`, `.attr()`, `.append()`, `.each()`, `.val()`

### Phase 3 (Lekcja 6-8): Advanced
Dodaj: `.animate()`, `$.ajax()`, `.filter()`, `.prop()`

### Phase 4 (Lekcja 9-10): Expert
Wszystko razem w projekt

---

## ✅ Checklist dla uczniów

Po każdej lekcji sprawdź czy znasz:

- [ ] Mogę wybrać elementy (find, children, parent)
- [ ] Mogę zmienić zawartość (text, html, append)
- [ ] Mogę zmienić styl (addClass, css)
- [ ] Mogę obsługiwać eventy (.on, .click)
- [ ] Mogę animować elementy (show, hide, animate)
- [ ] Mogę iterować po kolekcji (.each)
- [ ] Mogę pracować z formularzami (.val, .prop)
- [ ] Mogę wysyłać dane na serwer ($.ajax)

---

## 🚀 Zapamiętaj:

> **Prawie wszystkie operacje jQuery to:**
> 
> 1. **Selekcja:** `$(selector)`
> 2. **Operacja:** `.metoda()`
> 3. **Łańcuchowanie:** `$(selector).metoda1().metoda2()`

---

## 📚 Linki do dokumentacji

- [jQuery API Reference](https://api.jquery.com/)
- [jQuery Tutorial - W3Schools](https://www.w3schools.com/jquery/)
- [Cheat Sheet](https://oscarotero.com/jquery/)
