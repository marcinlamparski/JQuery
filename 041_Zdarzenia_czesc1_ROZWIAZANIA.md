# Lekcja 041: Obsługa zdarzeń - Część 1 (Zdarzenia podstawowe)
## PLIK NAUCZYCIELA - ROZWIĄZANIA

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

## Ćwiczenia - ROZWIĄZANIA

### Zadanie 1: Proste kliknięcie

**Cel:** Stwórz przycisk, który po kliknięciu zmienia swój kolor na czerwony.

**Rozwiązanie:**
```javascript
$(function() {
    $("#colorBtn").on("click", function() {
        $(this).css("background-color", "red");
    });
});
```

**Wyjaśnienie:** Używamy `.on("click")` aby obsłużyć kliknięcie na element z ID `colorBtn`. `$(this)` odnosi się do przycisku, a `.css()` zmienia jego kolor tła.

---

### Zadanie 2: Hover na elemencie

**Cel:** Stwórz element `<div>`, który po najechaniu myszką zmienia kolor na żółty, a po opuszczeniu wraca do białego.

**Rozwiązanie:**
```javascript
$(function() {
    $("#box").hover(
        function() {
            $(this).css("background-color", "yellow");
        },
        function() {
            $(this).css("background-color", "white");
        }
    );
});
```

**Wyjaśnienie:** Metoda `.hover()` przyjmuje dwie funkcje - pierwsza dla `mouseenter`, druga dla `mouseleave`.

**Alternatywne rozwiązanie:**
```javascript
$(function() {
    $("#box").on("mouseenter", function() {
        $(this).css("background-color", "yellow");
    });
    
    $("#box").on("mouseleave", function() {
        $(this).css("background-color", "white");
    });
});
```

---

### Zadanie 3: Podwójne kliknięcie

**Cel:** Stwórz element, który schowuje się (hide) po podwójnym kliknięciu.

**Rozwiązanie:**
```javascript
$(function() {
    $("#disappear").on("dblclick", function() {
        $(this).hide();
    });
});
```

**Wyjaśnienie:** Używamy `.on("dblclick")` do obsługi podwójnego kliknięcia. Metoda `.hide()` schowuje element.

---

### Zadanie 4: Zmiana tekstu przycisku

**Cel:** Stwórz przycisk, który zmienia swój tekst na "Kliknięty!" po kliknięciu.

**Rozwiązanie:**
```javascript
$(function() {
    $("#textBtn").on("click", function() {
        $(this).text("Kliknięty!");
    });
});
```

**Wyjaśnienie:** Metoda `.text()` zmienia zawartość tekstową elementu.

---

### Zadanie 5: Obsługa inputu - Focus i Blur

**Cel:** Stwórz pole tekstowe, które zmienia kolor tła na `lightyellow` gdy otrzyma fokus, i na `white` gdy go utraci.

**Rozwiązanie:**
```javascript
$(function() {
    $("#myInput").on("focus", function() {
        $(this).css("background-color", "lightyellow");
    });
    
    $("#myInput").on("blur", function() {
        $(this).css("background-color", "white");
    });
});
```

**Wyjaśnienie:** 
- `focus` - wyzwolony gdy użytkownik kliknie na input
- `blur` - wyzwolony gdy użytkownik kliknie poza inputem

**Alternatywne rozwiązanie (bardziej zwięzłe):**
```javascript
$(function() {
    $("#myInput").focus(function() {
        $(this).css("background-color", "lightyellow");
    });
    
    $("#myInput").blur(function() {
        $(this).css("background-color", "white");
    });
});
```

---

### Zadanie 6: Dodawanie klasy CSS

**Cel:** Stwórz przycisk z dwoma elementami div. Po kliknięciu przycisku, pierwszy div powinien dodać sobie klasę `highlight`.

**Rozwiązanie:**
```javascript
$(function() {
    $("#addClassBtn").on("click", function() {
        $("#box1").addClass("highlight");
    });
});
```

**Wyjaśnienie:** Metoda `.addClass()` dodaje klasę CSS do elementu. Możemy też dobrać się do elementu poprzez selektor ID.

---

### Zadanie 7: Usuwanie klasy CSS

**Cel:** Dodaj przycisk "Usuń klasę", który będzie usuwać klasę `highlight` z elementu.

**Rozwiązanie:**
```javascript
$(function() {
    $("#addClassBtn").on("click", function() {
        $("#box1").addClass("highlight");
    });
    
    $("#removeClassBtn").on("click", function() {
        $("#box1").removeClass("highlight");
    });
});
```

**Wyjaśnienie:** Metoda `.removeClass()` usuwa klasę CSS z elementu.

---

### Zadanie 8: Toggle klasy CSS

**Cel:** Stwórz przycisk, który przełącza klasę `highlight` na div (jeśli istnieje, usuń; jeśli nie istnieje, dodaj).

**Wskazówka:** Użyj metody `.toggleClass()`

**Rozwiązanie:**
```javascript
$(function() {
    $("#toggleBtn").on("click", function() {
        $("#box1").toggleClass("highlight");
    });
});
```

**Wyjaśnienie:** Metoda `.toggleClass()` przełącza klasę - jeśli klasa istnieje, usuwa ją; jeśli nie istnieje, dodaje ją.

---

### Zadanie 9: Zmiana CSS właściwości

**Cel:** Stwórz element, który po kliknięciu zmienia wiele CSS właściwości jednocześnie:
- background-color na green
- color na white
- padding na 20px

**Rozwiązanie:**
```javascript
$(function() {
    $("#box").on("click", function() {
        $(this).css({
            "background-color": "green",
            "color": "white",
            "padding": "20px"
        });
    });
});
```

**Wyjaśnienie:** Można przekazać obiekt JSON do metody `.css()`, aby zmienić wiele właściwości jednocześnie.

**Alternatywne rozwiązanie (mniej eleganckie):**
```javascript
$(function() {
    $("#box").on("click", function() {
        $(this).css("background-color", "green");
        $(this).css("color", "white");
        $(this).css("padding", "20px");
    });
});
```

---

### Zadanie 10: Formularz z focus i blur

**Cel:** Stwórz formularz z polami imię i email. Dla każdego pola:
- Po focus: zmień border na `2px solid blue`
- Po blur: zmień border z powrotem na `1px solid gray`

**Rozwiązanie:**
```javascript
$(function() {
    $("#name, #email").on("focus", function() {
        $(this).css("border", "2px solid blue");
    });
    
    $("#name, #email").on("blur", function() {
        $(this).css("border", "1px solid gray");
    });
});
```

**Wyjaśnienie:** Selektor `#name, #email` pozwala na wybór obu elementów naraz. Wtedy obsługujemy zdarzenia dla obydwu jednocześnie.

**Alternatywne rozwiązanie (przy większej liczbie pól):**
```javascript
$(function() {
    $("input").on("focus", function() {
        $(this).css("border", "2px solid blue");
    });
    
    $("input").on("blur", function() {
        $(this).css("border", "1px solid gray");
    });
});
```

Tutaj wybieramy wszystkie elementy `input` na stronie.

---

## Notatki dla nauczyciela

### Trudności, które mogą napotkać uczniowie:

1. **Zamieszanie między `.click()` a `.on("click")`** - Wytłumacz, że `.on()` jest nowszym, bardziej elastycznym sposobem.

2. **Niepewność co do `$(this)`** - Pokaż, że `$(this)` zawsze odnosi się do elementu, na którym został wyzwolony event.

3. **Zapomniane nawiasy w `.css()`** - Uczniowie mogą zapomnieć o cudzysłowach wokół nazw właściwości CSS.

4. **Mieszanie `.addClass()` z `.css()`** - Objaśnij, że `.addClass()` dodaje klasę CSS, a `.css()` zmienia style bezpośrednio.

5. **Problemy ze złożoną selektorami** - W zadaniu 10 selektor `#name, #email` może być niejasny dla początkujących.

### Rozszerzenia dla zainteresowanych uczniów:

- Dodaj opcję "undo" do zadania 7 (przycisk, który przywraca stan)
- W zadaniu 10 dodaj walidację: zmień border na czerwony, jeśli pole jest puste
- Stwórz licznik kliknięć dla każdego elementu osobno

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
