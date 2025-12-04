# Lekcja 7: Formularze i walidacja

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Pracować z różnymi typami pól formularza
- Walidować dane wpisane przez użytkownika
- Wyświetlać komunikaty błędów
- Dynamicznie zarządzać formularzami

---

## Typy pól formularza

### Input tekstowy

```javascript
// Pobranie wartości
var tekst = $("input[type='text']").val();

// Ustawienie wartości
$("input[type='text']").val("Nowa wartość");

// Focus na input
$("input[type='text']").focus();

// Sprawdzenie czy jest pusty
if ($("input[type='text']").val() === "") {
    console.log("Pole jest puste");
}
```

### Textarea

```javascript
// Pobranie tekstu
var tekst = $("textarea").val();

// Ustawienie tekstu
$("textarea").val("Nowy tekst...");
```

### Checkbox

```javascript
// Sprawdzenie czy zaznaczony
if ($("input[type='checkbox']").is(":checked")) {
    console.log("Checkbox zaznaczony");
}

// Zaznaczenie checkbox
$("input[type='checkbox']").prop("checked", true);

// Odznaczenie
$("input[type='checkbox']").prop("checked", false);

// Liczba zaznaczonych
var zaznaczone = $("input[type='checkbox']:checked").length;
```

### Radio button

```javascript
// Pobranie wybranej wartości
var wybrana = $("input[name='gender']:checked").val();

// Zaznaczenie konkretnego radio
$("input[name='gender'][value='male']").prop("checked", true);
```

### Select (Dropdown)

```javascript
// Pobranie wybranej opcji
var opcja = $("select").val();

// Ustawienie wybranej opcji
$("select").val("option2");

// Pobranie tekstu wybranej opcji
var tekst = $("select option:selected").text();
```

---

## Walidacja formularza

### Walidacja podstawowa

```javascript
// Sprawdzenie czy pole jest puste
function walidujPuste(pole) {
    if ($(pole).val().trim() === "") {
        return false;
    }
    return true;
}

// Użycie
if (!walidujPuste("#username")) {
    alert("Pole nie może być puste!");
}
```

### Walidacja emailu

```javascript
function walidujEmail(email) {
    var regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
}

// Użycie
var email = $("#email").val();
if (!walidujEmail(email)) {
    alert("Nieprawidłowy email!");
}
```

### Walidacja długości hasła

```javascript
function walidujHaslo(haslo) {
    if (haslo.length < 8) {
        return false;
    }
    return true;
}
```

### Walidacja liczby

```javascript
function walidujLiczbe(wartosc) {
    return !isNaN(wartosc) && isFinite(wartosc);
}
```

---

## Praktyka - Walidacja formularza

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .error { color: red; font-size: 12px; }
        input { padding: 5px; margin: 5px 0; width: 200px; }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<form id="register">
    <h2>Rejestracja</h2>
    
    <label>Użytkownik:</label>
    <input type="text" id="username" placeholder="Nazwa użytkownika">
    <div class="error" id="userError"></div>
    
    <label>Email:</label>
    <input type="email" id="email" placeholder="E-mail">
    <div class="error" id="emailError"></div>
    
    <label>Hasło:</label>
    <input type="password" id="password" placeholder="Minimum 8 znaków">
    <div class="error" id="passError"></div>
    
    <button type="submit">Zarejestruj się</button>
    <div id="success"></div>
</form>

<script>
$(function() {
    $("#register").on("submit", function(e) {
        e.preventDefault();
        
        // Wyczyszczenie błędów
        $(".error").text("");
        $("#success").text("");
        
        var username = $("#username").val().trim();
        var email = $("#email").val().trim();
        var password = $("#password").val();
        
        var valid = true;
        
        // Walidacja użytkownika
        if (username === "") {
            $("#userError").text("Pole nie może być puste!");
            valid = false;
        } else if (username.length < 3) {
            $("#userError").text("Nazwa musi mieć co najmniej 3 znaki!");
            valid = false;
        }
        
        // Walidacja emailu
        var emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (email === "") {
            $("#emailError").text("Pole nie może być puste!");
            valid = false;
        } else if (!emailRegex.test(email)) {
            $("#emailError").text("Nieprawidłowy format emailu!");
            valid = false;
        }
        
        // Walidacja hasła
        if (password === "") {
            $("#passError").text("Pole nie może być puste!");
            valid = false;
        } else if (password.length < 8) {
            $("#passError").text("Hasło musi mieć co najmniej 8 znaków!");
            valid = false;
        }
        
        if (valid) {
            $("#success").text("Rejestracja udana!").css("color", "green");
        }
    });
});
</script>

</body>
</html>
```

---

## Ćwiczenie 1: Podstawowe pole formularza

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<input type="text" id="myInput" placeholder="Wpisz coś">
<button id="showBtn">Pokaż wartość</button>
<button id="clearBtn">Wyczyść</button>
<div id="output"></div>

<script>
$(function() {
    // Zadanie 1: Po kliknięciu #showBtn pokaż wartość input w #output
    // ...
    
    // Zadanie 2: Po kliknięciu #clearBtn wyczyść input
    // ...
    
    // Zadanie 3: Po wpisaniu czegoś w input, wyświetlaj na bieżąco ilość znaków
    // ...
});
</script>

</body>
</html>
```

### Rozwiązanie
```javascript
$(function() {
    $("#showBtn").on("click", function() {
        var wartosc = $("#myInput").val();
        $("#output").text("Wartość: " + wartosc);
    });
    
    $("#clearBtn").on("click", function() {
        $("#myInput").val("");
    });
    
    $("#myInput").on("keyup", function() {
        var dlugos = $(this).val().length;
        $("#output").text("Znaków: " + dlugos);
    });
});
```

---

## Ćwiczenie 2: Walidacja emailu

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .error { color: red; }
        .success { color: green; }
        input { padding: 8px; margin: 10px 0; }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<label>Email:</label>
<input type="email" id="email" placeholder="Wpisz email">
<button id="validateBtn">Waliduj</button>
<div id="message"></div>

<script>
$(function() {
    $("#validateBtn").on("click", function() {
        var email = $("#email").val().trim();
        var emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        
        // Zadanie: Sprawdź czy email jest prawidłowy
        // Jeśli tak, wyświetl "Email prawidłowy!" (kolor zielony, klasa "success")
        // Jeśli nie, wyświetl "Email nieprawidłowy!" (kolor czerwony, klasa "error")
        // ...
    });
});
</script>

</body>
</html>
```

### Rozwiązanie
```javascript
$(function() {
    $("#validateBtn").on("click", function() {
        var email = $("#email").val().trim();
        var emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        
        if (emailRegex.test(email)) {
            $("#message").text("Email prawidłowy!").removeClass("error").addClass("success");
        } else {
            $("#message").text("Email nieprawidłowy!").removeClass("success").addClass("error");
        }
    });
});
```

---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Jak pracować z różnymi typami pól formularza
- Jak pobierać i ustawiać wartości
- Jak walidować dane
- Jak wyświetlać komunikaty
- Jak tworzyć pełną walidację formularza

**Kolejna lekcja:** AJAX - nauczymy się pobierać dane z serwera bez przeładowywania strony!
