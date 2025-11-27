# Podsumowanie - TOP Metody jQuery z przykładami

## 📊 SZYBKA TABELA POLECEŃ

```
┌─────────────────────────────────────────────────────────────────┐
│                    NAJCZĘŚCIEJ UŻYWANE METODY                   │
└─────────────────────────────────────────────────────────────────┘

┌─ SELEKCJA I NAWIGACJA ────────────────────────────────────┐
│  .find("selector")        - Wszyscy potomkowie            │
│  .children("selector")    - Bezpośrednie dzieci           │
│  .parent()                - Rodzic elementu               │
│  .eq(index)               - Element po indeksie           │
│  .filter(".class")        - Filtruj wybrane elementy      │
│  .not(".class")           - Wyklucz elementy              │
└───────────────────────────────────────────────────────────┘

┌─ ZAWARTOŚĆ ───────────────────────────────────────────────┐
│  .text("tekst")           - Zmień/pobrań tekst            │
│  .html("<b>HTML</b>")     - Zmień/pobrań HTML            │
│  .append("<p>Nowy</p>")   - Dodaj na koniec               │
│  .prepend("<p>Nowy</p>")  - Dodaj na początek             │
│  .remove()                - Usuń element z DOM            │
│  .empty()                 - Wyczyść zawartość             │
└───────────────────────────────────────────────────────────┘

┌─ ATRYBUTY ────────────────────────────────────────────────┐
│  .attr("href", "url")     - Ustaw atrybut HTML            │
│  .prop("checked", true)   - Ustaw właściwość DOM          │
│  .val("tekst")            - Ustaw wartość formularza      │
│  .addClass("active")      - Dodaj klasę CSS               │
│  .removeClass("active")   - Usuń klasę CSS                │
│  .toggleClass("active")   - Przełącz klasę CSS            │
│  .hasClass("active")      - Czy ma klasę?                 │
└───────────────────────────────────────────────────────────┘

┌─ STYLE CSS ───────────────────────────────────────────────┐
│  .css("color", "red")     - Zmień styl pojedynczy         │
│  .css({color: "red", ... })- Zmień wiele stylów           │
│  .width(200)              - Pobierz/ustaw szerokość       │
│  .height(300)             - Pobierz/ustaw wysokość        │
│  .offset()                - Pozycja względem dokumentu    │
│  .position()              - Pozycja względem rodzica      │
└───────────────────────────────────────────────────────────┘

┌─ ZDARZENIA ───────────────────────────────────────────────┐
│  .on("click", fn)         - Obsługuj zdarzenie            │
│  .on("click", ".sel", fn) - Delegowanie zdarzeń           │
│  .click(fn)               - Skrót: kliknięcie             │
│  .submit(fn)              - Obsługa wysłania formularza    │
│  .hover(fn1, fn2)         - Najechanie i opuszczenie      │
│  .off("click")            - Usuń obsługę zdarzenia        │
└───────────────────────────────────────────────────────────┘

┌─ EFEKTY I ANIMACJE ───────────────────────────────────────┐
│  .show() / .hide()        - Pokaż/ukryj element           │
│  .toggle()                - Przełącz widoczność           │
│  .fadeIn(500)             - Pojawiaj się (500ms)          │
│  .fadeOut(500)            - Zanikaj (500ms)               │
│  .slideDown(300)          - Rozwijaj menu                 │
│  .slideUp(300)            - Zwijaj menu                   │
│  .animate({...}, 1000)    - Niestandardowa animacja       │
│  .delay(1000)             - Czekaj 1 sekundę              │
└───────────────────────────────────────────────────────────┘

┌─ ITERACJA ────────────────────────────────────────────────┐
│  .each(fn)                - Iteruj po elementach          │
│  $.each(arr, fn)          - Iteruj po tablicy/obiekcie    │
│  $.map(arr, fn)           - Transformuj tablicę           │
│  $.grep(arr, fn)          - Filtruj tablicę               │
│  $.inArray(val, arr)      - Szukaj w tablicy              │
└───────────────────────────────────────────────────────────┘

┌─ AJAX ────────────────────────────────────────────────────┐
│  $.ajax({...})            - Uniwersalne żądanie HTTP      │
│  $.get("url", fn)         - GET - pobieranie danych       │
│  $.post("url", data, fn)  - POST - wysyłanie danych       │
│  $.load("url")            - Załaduj HTML z pliku          │
└───────────────────────────────────────────────────────────┘
```

---

## 🎯 PRAKTYCZNE KOMBINACJE

### Wzór 1: Zmiana zawartości + Style
```javascript
$("#myDiv")
    .text("Nowy tekst")
    .css("color", "red")
    .css("font-weight", "bold");

// Lub krócej:
$("#myDiv")
    .text("Nowy tekst")
    .css({
        "color": "red",
        "font-weight": "bold"
    });
```

### Wzór 2: Event listener + Manipulacja
```javascript
$(".button").on("click", function() {
    $(this)
        .addClass("active")
        .text("Aktywny")
        .css("background-color", "green");
});
```

### Wzór 3: Iteracja + Warunki
```javascript
$("li").each(function(index) {
    if (index % 2 === 0) {
        $(this).css("background-color", "lightgray");
    }
});
```

### Wzór 4: AJAX + Dynamiczne dodawanie
```javascript
$.ajax({
    url: "api/items",
    success: function(data) {
        $.each(data, function(i, item) {
            $("ul").append("<li>" + item.name + "</li>");
        });
    }
});
```

### Wzór 5: Filtrowanie + Animacja
```javascript
$(".item")
    .filter(".important")
    .fadeIn(500);

// Równoważnie:
$(".item.important").fadeIn(500);
```

---

## 💪 MINI PROJEKTY DO ĆWICZENIA

### Projekt 1: Przycisk Toggle (wymaga 3 metody)
```javascript
$("#toggleBtn").on("click", function() {
    $("#content").slideToggle();
    $(this).toggleClass("active");
});
```
**Metody:** `.on()`, `.slideToggle()`, `.toggleClass()`

---

### Projekt 2: Filtrowanie listy (wymaga 5 metod)
```javascript
$("#searchInput").on("keyup", function() {
    var szukaj = $(this).val().toLowerCase();
    
    $(".item").filter(function() {
        return $(this).text().toLowerCase().indexOf(szukaj) < 0;
    }).hide();
    
    $(".item").filter(function() {
        return $(this).text().toLowerCase().indexOf(szukaj) > -1;
    }).show();
});
```
**Metody:** `.on()`, `.val()`, `.filter()`, `.hide()`, `.show()`

---

### Projekt 3: Licznik kliknięć (wymaga 4 metody)
```javascript
var count = 0;

$("#button").on("click", function() {
    count++;
    $("#counter").text(count);
    
    if (count % 5 === 0) {
        $("#counter").addClass("milestone");
    }
});
```
**Metody:** `.on()`, `.text()`, `.addClass()`

---

### Projekt 4: Todo aplikacja (wymaga 10 metod)
```javascript
$("#addBtn").on("click", function() {
    var tekst = $("#input").val();
    
    if (tekst === "") return;
    
    var item = $("<li>" + tekst + " <button class='delete'>X</button></li>");
    $("#list").append(item);
    $("#input").val("");
});

$("#list").on("click", ".delete", function() {
    $(this).parent().remove();
});

$("#list").on("click", "li", function() {
    $(this).toggleClass("completed");
});
```
**Metody:** `.on()`, `.val()`, `.append()`, `.remove()`, `.toggleClass()`

---

## 📈 GRAPH - Połączenia między metodami

```
                            START: $(selector)
                                    |
                    ________________|________________
                   |                |                |
            SELEKCJA          ZAWARTOŚĆ         ATRYBUTY
              .find()            .text()          .attr()
            .children()          .html()          .css()
            .parent()          .append()        .addClass()
            .eq()              .remove()        .val()
                                                    |
                                    _______________|___________
                                   |                |          |
                              ZDARZENIA         EFEKTY    AJAX
                              .on()           .show()    $.ajax()
                              .click()        .hide()    $.get()
                              .submit()      .animate()  $.post()
                              .hover()       .fadeIn()
                                            .slideUp()
```

---

## ✨ SZTUCZKI I PORADY

### Sztuka 1: Łańcuchowanie zamiast powtórzeń
```javascript
// ❌ ŹLE - 4 selekcje DOM
$("#btn").css("color", "red");
$("#btn").css("background", "blue");
$("#btn").text("Click me");
$("#btn").show();

// ✅ DOBRZE - 1 selekcja + łańcuch
$("#btn")
    .css("color", "red")
    .css("background", "blue")
    .text("Click me")
    .show();

// ✅ NAJLEPIEJ - 1 selekcja + jeden .css()
$("#btn")
    .css({ color: "red", background: "blue" })
    .text("Click me")
    .show();
```

### Sztuka 2: Użyj `.on()` zawsze!
```javascript
// ❌ STARE - nie działa na dynamicznych elementach
$(".item").click(fn);

// ✅ NOWE - działa też na elementach dodanych później
$(document).on("click", ".item", fn);
```

### Sztuka 3: Cache selektory!
```javascript
// ❌ ŹLE - szuka DOM 5x
for (let i = 0; i < 5; i++) {
    $("#container").append("<p>Tekst</p>");
}

// ✅ DOBRZE - szuka 1x
var $container = $("#container");
for (let i = 0; i < 5; i++) {
    $container.append("<p>Tekst</p>");
}
```

### Sztuka 4: Sprawdzaj czy element istnieje!
```javascript
// ❌ ŹLE - błąd jeśli element nie istnieje
$("#nonexistent").text("Test");

// ✅ DOBRZE - sprawdź warunek
if ($("#nonexistent").length) {
    $("#nonexistent").text("Test");
}

// ✅ NAJLEPIEJ - skorzystaj z tego
if ($("#nonexistent").length > 0) {
    // Element istnieje
}
```

---

## 🎓 CHECKLIST - Co powinieneś umieć

Zaznacz co już potrafisz:

- [ ] Mogę wybrać element po ID
- [ ] Mogę wybrać elementy po klasie
- [ ] Mogę znaleźć potomków elementu
- [ ] Mogę zmienić tekst elementu
- [ ] Mogę zmienić HTML elementu
- [ ] Mogę dodać CSS klasę
- [ ] Mogę usunąć CSS klasę
- [ ] Mogę zmienić styl inline
- [ ] Mogę obsługiwać kliknięcie
- [ ] Mogę obsługiwać formularz
- [ ] Mogę pokazać/ukryć element
- [ ] Mogę zanimować element
- [ ] Mogę iterować po kolekcji
- [ ] Mogę wysłać AJAX żądanie
- [ ] Mogę łączyć metody w chain

---

## 📞 SOS - Szybka pomoc

| Problem | Rozwiązanie |
|---------|------------|
| Nie działa moja metoda | Sprawdź czy selektor znajduje elementy: `$("selector").length` |
| Event nie działa | Użyj `.on()` i upewnij się że element istnieje przy załadowaniu |
| Efekt nie jest płynny | Dodaj czas: `.show(500)` zamiast `.show()` |
| Dynamiczny element nie reaguje | Użyj delegowania: `.on("event", ".selector", fn)` |
| Kod jest wolny | Cache selektor: `var $el = $("selector"); $el.method()` |
| HTML się nie zmienia | Użyj `.html()` zamiast `.text()` |

---

## 🚀 NASTĘPNE KROKI

1. **Naucz się Top 10** - poznaj dobrze najpopularniejsze metody
2. **Ćwicz Mini Projekty** - wykonaj wszystkie 4 projekty powyżej
3. **Buduj coś swojego** - stwórz swój projekt
4. **Czytaj dokumentację** - jQuery API docs
5. **Słuchaj wyzwań** - Codewars, HackerRank jQuery challenges

---

## 💾 Plik do wydruku

Wydrukuj tę stronę lub zapisz jako PDF do szybkiej referencji! 🖨️
