# Lekcja 8: AJAX - Asynchroniczne żądania

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Rozumieć czym jest AJAX
- Używać $.ajax() do pobierania danych
- Pracować z JSON
- Obsługiwać odpowiedzi z serwera
- Wyświetlać dane dynamicznie

---

## Czym jest AJAX?

**AJAX** = Asynchronous JavaScript and XML

AJAX pozwala na:
- Wysyłanie żądań do serwera bez przeładowywania strony
- Pobieranie danych w tle
- Aktualizowanie zawartości strony dynamicznie

Dzisiaj zamiast XML używamy głównie **JSON**.

---

## $.ajax() - Podstawowe żądanie

```javascript
$.ajax({
    url: "https://api.example.com/data",  // Adres URL
    type: "GET",  // Typ żądania (GET, POST, PUT, DELETE)
    success: function(data) {
        // Kod uruchamiany gdy żądanie się uda
        console.log("Dane otrzymane:", data);
    },
    error: function(error) {
        // Kod uruchamiany gdy żądanie się nie uda
        console.log("Błąd:", error);
    }
});
```

---

## GET - Pobieranie danych

### $.get() - Krótsza forma

```javascript
$.get("https://api.example.com/users", function(data) {
    console.log(data);
});
```

### $.ajax() z GET

```javascript
$.ajax({
    url: "https://api.example.com/users",
    type: "GET",
    dataType: "json",  // Oczekujemy JSON
    success: function(data) {
        console.log(data);
    },
    error: function(error) {
        console.log("Błąd żądania");
    }
});
```

### Praktyka - Pobieranie użytkowników

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="loadBtn">Załaduj użytkowników</button>
<div id="users"></div>

<script>
$(function() {
    $("#loadBtn").on("click", function() {
        $.ajax({
            url: "https://jsonplaceholder.typicode.com/users",
            type: "GET",
            dataType: "json",
            success: function(data) {
                // data to tablica użytkowników
                var html = "";
                $.each(data, function(index, user) {
                    html += "<p>" + user.name + " (" + user.email + ")</p>";
                });
                $("#users").html(html);
            },
            error: function() {
                $("#users").html("<p>Błąd ładowania danych</p>");
            }
        });
    });
});
</script>

</body>
</html>
```

---

## POST - Wysyłanie danych

```javascript
$.ajax({
    url: "https://api.example.com/users",
    type: "POST",
    dataType: "json",
    data: {
        name: "Jan Kowalski",
        email: "jan@example.com"
    },
    success: function(response) {
        console.log("Dane wysłane pomyślnie!");
        console.log(response);
    },
    error: function() {
        console.log("Błąd wysyłania danych");
    }
});
```

### Praktyka - Wysyłanie formularza

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<form id="createForm">
    <input type="text" id="name" placeholder="Imię" required>
    <input type="email" id="email" placeholder="Email" required>
    <button type="submit">Wyślij</button>
</form>

<div id="message"></div>

<script>
$(function() {
    $("#createForm").on("submit", function(e) {
        e.preventDefault();
        
        $.ajax({
            url: "https://jsonplaceholder.typicode.com/users",
            type: "POST",
            dataType: "json",
            data: {
                name: $("#name").val(),
                email: $("#email").val()
            },
            success: function(response) {
                $("#message").html("<p style='color:green;'>Wysłano pomyślnie!</p>");
                $("#createForm")[0].reset();  // Wyczyść formularz
            },
            error: function() {
                $("#message").html("<p style='color:red;'>Błąd wysyłania</p>");
            }
        });
    });
});
</script>

</body>
</html>
```

---

## JSON - Format danych

JSON (JavaScript Object Notation) to format danych:

```json
{
    "id": 1,
    "name": "Jan Kowalski",
    "email": "jan@example.com",
    "active": true
}
```

Tablica obiektów JSON:

```json
[
    {
        "id": 1,
        "name": "Jan",
        "email": "jan@example.com"
    },
    {
        "id": 2,
        "name": "Maria",
        "email": "maria@example.com"
    }
]
```

---

## Obsługa błędów i stanów

```javascript
$.ajax({
    url: "https://api.example.com/data",
    type: "GET",
    beforeSend: function() {
        // Wywoływane przed wysłaniem żądania
        console.log("Wysyłam żądanie...");
        $("#loading").show();
    },
    success: function(data) {
        // Powodzenie (kod 200-299)
        console.log("Sukces!");
    },
    error: function(xhr, status, error) {
        // Błąd
        console.log("Status:" + xhr.status);  // 404, 500, etc.
        console.log("Błąd: " + error);
    },
    complete: function() {
        // Zawsze wykonywane (niezależnie od sukcesu/błędu)
        console.log("Żądanie zakończone");
        $("#loading").hide();
    }
});
```

---

## Ćwiczenie 1: Pobieranie danych

### Polecenie

Pobierz listę postów z API i wyświetl je na stronie:

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .post { border: 1px solid #ccc; padding: 10px; margin: 10px 0; }
        .post h3 { margin: 0; }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<button id="loadBtn">Załaduj posty</button>
<div id="posts"></div>

<script>
$(function() {
    $("#loadBtn").on("click", function() {
        // Zadanie: Użyj $.ajax() aby pobrac posty z:
        // https://jsonplaceholder.typicode.com/posts?userId=1
        // Wyświetl każdy post w formacie:
        // <div class="post">
        //     <h3>[Title]</h3>
        //     <p>[Body]</p>
        // </div>
        // ...
    });
});
</script>

</body>
</html>
```

### Wskazówka
- Użyj $.each() aby iterować po postach
- Odpowiedź będzie tablicą JSON obiektów
- Każdy post ma właściwości: id, title, body, userId

### Rozwiązanie
```javascript
$(function() {
    $("#loadBtn").on("click", function() {
        $.ajax({
            url: "https://jsonplaceholder.typicode.com/posts?userId=1",
            type: "GET",
            dataType: "json",
            success: function(data) {
                var html = "";
                $.each(data, function(index, post) {
                    html += '<div class="post">';
                    html += '<h3>' + post.title + '</h3>';
                    html += '<p>' + post.body + '</p>';
                    html += '</div>';
                });
                $("#posts").html(html);
            },
            error: function() {
                $("#posts").html("<p>Błąd ładowania postów</p>");
            }
        });
    });
});
```

---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Czym jest AJAX i po co go używać
- Jak używać $.ajax() do żądań
- Różnicę między GET i POST
- Jak pracować z JSON
- Jak obsługiwać błędy
- Jak wyświetlać dynamiczne dane

**Kolejna lekcja:** jQuery UI - komponenty interfejsu użytkownika!
