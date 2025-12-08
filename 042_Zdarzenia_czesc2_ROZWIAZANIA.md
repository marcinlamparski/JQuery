# Lekcja 042: Obsługa zdarzeń - Część 2 (Delegowanie i zaawansowane)
## PLIK NAUCZYCIELA - ROZWIĄZANIA

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

## Ćwiczenia - ROZWIĄZANIA

### Zadanie 1: Delegowanie - Dodawanie i obsługa elementów

**Cel:** Stwórz listę `<ul>` z kilkoma elementami `<li>`, przycisk "Dodaj" i przycisk "Usuń zaznaczenia".
- Po kliknięciu na `<li>` zmienia się jego kolor na żółty
- Po kliknięciu "Dodaj", dodaj nowy element do listy (element powinien też być klikowalny!)
- Po kliknięciu "Usuń zaznaczenia", przywróć oryginalny kolor wszystkich elementów

**Rozwiązanie:**
```javascript
$(function() {
    var count = 4;
    
    // Delegowanie - obsługa kliknięcia na <li>
    $("#myList").on("click", "li", function() {
        $(this).css("background-color", "yellow");
    });
    
    // Dodaj nowy element
    $("#addBtn").on("click", function() {
        $("#myList").append("<li>Element " + count + "</li>");
        count++;
    });
    
    // Wyczyść zaznaczenia
    $("#clearBtn").on("click", function() {
        $("#myList li").css("background-color", "lightgray");
    });
});
```

**Wyjaśnienie:**
- Delegowanie: `$("#myList").on("click", "li", ...)` - obsługuje kliknięcia na wszystkich `<li>` w `#myList`, nawet tych dodanych później
- `.append()` dodaje nowy element do listy
- `$("#myList li")` wybiera wszystkie `<li>` w liście

---

### Zadanie 2: preventDefault na linku

**Cel:** Stwórz link `<a>`, który normalnie przeszedłby na Google. Po kliknięciu na niego, zamiast przechodzić do Google, pokaż komunikat "Link został zablokowany!".

**Rozwiązanie:**
```javascript
$(function() {
    $("#googleLink").on("click", function(event) {
        event.preventDefault();
        $("#message").text("Link został zablokowany!");
    });
});
```

**Wyjaśnienie:**
- `event.preventDefault()` zapobiega domyślnemu działaniu (przejściu do linku)
- Zamiast tego możemy wykonać inny kod

---

### Zadanie 3: preventDefault na formularzu

**Cel:** Stwórz formularz z polami imię i email. Po wysłaniu formularza (zamiast go wysyłać), pokaż komunikat:
"Dane wysłane: [imię] - [email]"

**Rozwiązanie:**
```javascript
$(function() {
    $("#myForm").on("submit", function(event) {
        event.preventDefault();
        
        var imie = $("#name").val();
        var email = $("#email").val();
        
        $("#result").text("Dane wysłane: " + imie + " - " + email);
    });
});
```

**Wyjaśnienie:**
- `event.preventDefault()` zapobiega wysłaniu formularza
- `.val()` pobiera wartość pola tekstowego
- Wyświetlamy dane zamiast wysyłać formularz

---

### Zadanie 4: event.type

**Cel:** Stwórz przycisk. Po kliknięciu, pokaż w `<div>` jaki typ zdarzenia został wyzwolony.

**Rozwiązanie:**
```javascript
$(function() {
    $("#myBtn").on("click", function(event) {
        $("#info").text("Typ zdarzenia: " + event.type);
    });
});
```

**Wyjaśnienie:**
- `event.type` zawiera typ zdarzenia ("click", "dblclick", itp.)

---

### Zadanie 5: event.target

**Cel:** Stwórz kilka przycisków. Po kliknięciu na każdy, pokaż jego ID w `<div>`.

**Rozwiązanie:**
```javascript
$(function() {
    // Możemy obsługiwać wszystkie przyciski naraz za pomocą selektora button
    $("button").on("click", function(event) {
        var btnId = $(event.target).attr("id");
        $("#info").text("Kliknięty przycisk: " + btnId);
    });
});
```

**Wyjaśnienie:**
- `event.target` to element, na którym wyzwolono zdarzenie
- `$(event.target).attr("id")` pobiera atrybut ID tego elementu

**Alternatywne rozwiązanie (używając this):**
```javascript
$(function() {
    $("button").on("click", function() {
        var btnId = $(this).attr("id");
        $("#info").text("Kliknięty przycisk: " + btnId);
    });
});
```

---

### Zadanie 6: Usuwanie obsługi zdarzeń

**Cel:** Stwórz przycisk z dwoma przyciskami pomocniczymi: "Włącz kliknięcie" i "Wyłącz kliknięcie".
- Domyślnie, po kliknięciu głównego przycisku, pokaż komunikat "Przycisk kliknięty!"
- Po kliknięciu "Wyłącz kliknięcie", usunięcie obsługi zdarzenia
- Po kliknięciu "Włącz kliknięcie", ponownie dodaj obsługę zdarzenia

**Rozwiązanie:**
```javascript
$(function() {
    // Funkcja obsługi zdarzenia
    var handleClick = function() {
        $("#message").text("Przycisk kliknięty!");
    };
    
    // Domyślnie włącz obsługę
    $("#mainBtn").on("click", handleClick);
    
    // Wyłącz obsługę zdarzenia
    $("#toggleOff").on("click", function() {
        $("#mainBtn").off("click", handleClick);
        $("#message").text("Obsługa wyłączona");
    });
    
    // Włącz obsługę zdarzenia
    $("#toggleOn").on("click", function() {
        $("#mainBtn").on("click", handleClick);
        $("#message").text("Obsługa włączona");
    });
});
```

**Wyjaśnienie:**
- Definiujemy funkcję obsługi zdarzenia poza `.on()`, aby móc ją później usunąć
- `.off("click", handleClick)` usuwa konkretną obsługę zdarzenia
- `.on("click", handleClick)` ponownie dodaje obsługę

---

### Zadanie 7: stopPropagation()

**Cel:** Stwórz zagnieżdżone elementy div: zewnętrzny i wewnętrzny. Przyczep obsługę zdarzeń do obydwu.
- Po kliknięciu na zewnętrzny: pokaż "Kliknięty zewnętrzny div"
- Po kliknięciu na wewnętrzny: pokaż "Kliknięty wewnętrzny div" i zapobiegaj propagacji do zewnętrznego

**Rozwiązanie:**
```javascript
$(function() {
    // Obsługa zewnętrznego divu
    $("#outer").on("click", function() {
        $("#message").text("Kliknięty zewnętrzny div");
    });
    
    // Obsługa wewnętrznego divu
    $("#inner").on("click", function(event) {
        event.stopPropagation();
        $("#message").text("Kliknięty wewnętrzny div");
    });
});
```

**Wyjaśnienie:**
- Bez `stopPropagation()`, kliknięcie na wewnętrzny div wyzwolałoby też zdarzenie na zewnętrznym (bąbelkowanie)
- `event.stopPropagation()` zatrzymuje bąbelkowanie

---

### Zadanie 8: Dynamiczne dodawanie i obsługa z delegowaniem

**Cel:** Stwórz aplikację do-do:
- Lista z elementami
- Przycisk "Dodaj zadanie"
- Każde zadanie powinno być klikalny (zaznaczenie poprzez zmianę koloru)
- Przycisk "Wyczyść wszystkie zaznaczenia"

**Rozwiązanie:**
```javascript
$(function() {
    var taskCount = 1;
    
    // Delegowanie - obsługa kliknięcia na zadania
    $("#tasks").on("click", ".task", function() {
        $(this).toggleClass("done");
    });
    
    // Dodaj zadanie
    $("#addTaskBtn").on("click", function() {
        var taskName = $("#taskInput").val();
        if (taskName.trim() !== "") {
            $("#tasks").append('<div class="task">Zadanie ' + taskCount + ': ' + taskName + '</div>');
            taskCount++;
            $("#taskInput").val(""); // Wyczyść input
        }
    });
    
    // Wyczyść zaznaczenia
    $("#clearTasksBtn").on("click", function() {
        $("#tasks .task").removeClass("done");
    });
});
```

**Wyjaśnienie:**
- Delegowanie `.on("click", ".task", ...)` obsługuje wszystkie zadania, nawet dodane dynamicznie
- `.toggleClass("done")` przełącza klasę
- `.trim()` usuwa białe znaki z obu stron stringa
- `.val("")` czyszcza pole tekstowe

---

### Zadanie 9: Walidacja formularza z preventDefault

**Cel:** Stwórz formularz z polami: imię, email, hasło. Przy wysłaniu:
- Jeśli któreś pole jest puste, pokaż komunikat błędu i zapobiegaj wysłaniu
- Jeśli hasło ma mniej niż 6 znaków, pokaż błąd
- Jeśli wszystko OK, pokaż "Formularz wysłany poprawnie!"

**Rozwiązanie:**
```javascript
$(function() {
    $("#registerForm").on("submit", function(event) {
        event.preventDefault();
        
        // Pobierz wartości pól
        var name = $("#name").val();
        var email = $("#email").val();
        var password = $("#password").val();
        
        // Wyczyść poprzednie komunikaty
        $("#error").text("");
        $("#success").text("");
        
        // Walidacja
        if (name === "" || email === "" || password === "") {
            $("#error").text("Błąd: Wszystkie pola są wymagane!");
            return;
        }
        
        if (password.length < 6) {
            $("#error").text("Błąd: Hasło musi mieć co najmniej 6 znaków!");
            return;
        }
        
        // Wszystko OK
        $("#success").text("Formularz wysłany poprawnie!");
    });
});
```

**Wyjaśnienie:**
- Sprawdzamy czy pola są puste: `name === ""`
- Sprawdzamy długość hasła: `password.length < 6`
- `return` zatrzymuje dalsze wykonywanie kodu
- Wyświetlamy odpowiedni komunikat

---

### Zadanie 10: Kombinacja zdarzeń - Interaktywna lista

**Cel:** Stwórz interaktywną listę:
- Lista produktów z przyciskami "Usuń" przy każdym
- Przycisk "Dodaj produkt" (pyta o nazwę)
- Po najechaniu na produkt, zmień kolor tła
- Po kliknięciu "Usuń", usuń produkt z listy
- Liczyć liczbę produktów i wyświetlać na górze

**Rozwiązanie:**
```javascript
$(function() {
    // Delegowanie - obsługa kliknięcia "Usuń"
    $("#productList").on("click", ".delete-btn", function() {
        $(this).parent().remove(); // Usuń element nadrzędny (.product)
        updateCount();
    });
    
    // Dodaj produkt
    $("#addProductBtn").on("click", function() {
        var productName = prompt("Wpisz nazwę produktu:");
        if (productName && productName.trim() !== "") {
            var html = '<div class="product">' +
                       '<span>' + productName + '</span>' +
                       '<button class="delete-btn">Usuń</button>' +
                       '</div>';
            $("#productList").append(html);
            updateCount();
        }
    });
    
    // Funkcja do aktualizacji licznika
    function updateCount() {
        var count = $("#productList .product").length;
        $("#count").text(count);
    }
});
```

**Wyjaśnienie:**
- Delegowanie na `.delete-btn` obsługuje przyciski nawet dodane dynamicznie
- `.parent().remove()` usuwa element nadrzędny (cały `.product`)
- `prompt()` wyświetla okno dialogowe do wpisania tekstu
- `updateCount()` liczy elementy `.product` i aktualizuje licznik

---

## Notatki dla nauczyciela

### Trudności, które mogą napotkać uczniowie:

1. **Nierozumienie delegowania** - To jest trudny koncept. Tłumacz, że zdarzenia się propagują (bąbelkują) w górę DOM, i dlatego możemy obsługiwać je na elemencie nadrzędnym.

2. **Zapominanie o event.preventDefault()** - Uczniowie mogą zapomnieć, że domyślne zachowanie linku/formularza zostanie wykonane bez `preventDefault()`.

3. **Problemy z `$(this)` vs `event.target`** - Wytłumacz różnicę: `$(this)` to zawsze element, na którym wyzwolono event; `event.target` może być inne w delegowaniu.

4. **Usuwanie obsługi zdarzeń** - W zadaniu 6 uczniowie mogą nie wiedzieć, że trzeba zdefiniować funkcję poza `.on()` aby ją później usunąć.

5. **Zagęszczenie HTML w JavaScript** - W zadaniu 10 uczniowie mogą mieć problemy z konstruowaniem HTML jako stringów. Podpowiedź: można też używać jQuery do tworzenia elementów.

### Rozszerzenia dla zainteresowanych uczniów:

- W zadaniu 9 dodaj walidację emailu (sprawdzenie czy zawiera @)
- W zadaniu 10 dodaj możliwość edycji nazwy produktu
- Stwórz aplikację z localStorage, która zapisuje produkty między odświeżeniami

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
