# Lekcja 5: Efekty i animacje

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Używać efektów Show/Hide
- Tworzyć zanikające i pojawiające się elementy (Fade)
- Tworzyć efekty przesuwania (Slide)
- Tworzyć niestandardowe animacje
- Łączyć animacje w sekwencje

---

## Efekty podstawowe: Show i Hide

### .hide() - Ukrywanie elementu

```javascript
$("#myDiv").hide();  // Ukryj element
$("#myDiv").hide(1000);  // Ukryj z animacją przez 1000ms
```

### .show() - Pokazywanie elementu

```javascript
$("#myDiv").show();  // Pokaż element
$("#myDiv").show(1000);  // Pokaż z animacją przez 1000ms
```

### .toggle() - Przełączanie widoczności

```javascript
$("#myDiv").toggle();  // Pokaż jeśli ukryty, ukryj jeśli widoczny
$("#myDiv").toggle(1000);  // Z animacją
```

### Praktyka

```html
<button id="show">Pokaż</button>
<button id="hide">Ukryj</button>
<button id="toggle">Przełącz</button>

<div id="box" style="width:100px; height:100px; background-color:blue;"></div>

<script>
$(function() {
    $("#show").on("click", function() {
        $("#box").show(500);
    });
    
    $("#hide").on("click", function() {
        $("#box").hide(500);
    });
    
    $("#toggle").on("click", function() {
        $("#box").toggle(500);
    });
});
</script>
```

---

## Efekty zanikania: Fade

### .fadeIn() - Pojawianie się

```javascript
$("#myDiv").fadeIn();  // Pojawiaj natychmiast
$("#myDiv").fadeIn(1000);  // Pojawiaj przez 1 sekundę
```

### .fadeOut() - Zanikanie

```javascript
$("#myDiv").fadeOut();  // Zanika natychmiast
$("#myDiv").fadeOut(1000);  // Zanika przez 1 sekundę
```

### .fadeToggle() - Przełączanie zanikania

```javascript
$("#myDiv").fadeToggle(1000);
```

### .fadeTo() - Zanik do konkretnej nieprzezroczystości

```javascript
$("#myDiv").fadeTo(1000, 0.5);  // Zanik do 50% opacności w 1 sekundzie
```

### Praktyka

```html
<div id="fadebox" style="width:100px; height:100px; background-color:red;"></div>

<button id="fadeIn">Pojawiaj</button>
<button id="fadeOut">Zanikaj</button>
<button id="fadeTo">Zanik do 50%</button>

<script>
$(function() {
    $("#fadeIn").on("click", function() {
        $("#fadebox").fadeIn(1000);
    });
    
    $("#fadeOut").on("click", function() {
        $("#fadebox").fadeOut(1000);
    });
    
    $("#fadeTo").on("click", function() {
        $("#fadebox").fadeTo(1000, 0.5);
    });
});
</script>
```

---

## Efekty przesuwania: Slide

### .slideDown() - Rozwijanie

```javascript
$("#myDiv").slideDown();  // Rozwiń element
$("#myDiv").slideDown(1000);  // Rozwiń przez 1 sekundę
```

### .slideUp() - Zwijanie

```javascript
$("#myDiv").slideUp();  // Zwiń element
$("#myDiv").slideUp(1000);  // Zwiń przez 1 sekundę
```

### .slideToggle() - Przełączanie rozwijania

```javascript
$("#myDiv").slideToggle(1000);
```

### Praktyka - Akordeon

```html
<button class="toggle-btn">Sekcja 1</button>
<div class="section" style="display:none;">
    <p>Zawartość sekcji 1</p>
</div>

<button class="toggle-btn">Sekcja 2</button>
<div class="section" style="display:none;">
    <p>Zawartość sekcji 2</p>
</div>

<script>
$(function() {
    $(".toggle-btn").on("click", function() {
        $(this).next(".section").slideToggle(500);
    });
});
</script>
```

---

## Niestandardowe animacje: .animate()

`.animate()` pozwala tworzyć animacje dla prawie każdej właściwości CSS:

```javascript
$("#myDiv").animate({
    left: '250px',
    opacity: 0.5,
    height: '150px'
}, 1000);  // Animuj przez 1 sekundę
```

### Parametry

```javascript
$("#myDiv").animate({
    // właściwości CSS do animacji
    left: '250px',
    width: '200px',
    height: '200px'
}, 
1000,  // czas trwania (ms)
'linear',  // funkcja przejścia
function() {  // callback - wykonaj po animacji
    console.log("Animacja zakończona!");
});
```

### Praktyka - Animacja pozycji

```html
<div id="box" style="width:50px; height:50px; background-color:blue; position:absolute; left:0; top:0;"></div>
<button id="animate">Animuj</button>

<script>
$(function() {
    $("#animate").on("click", function() {
        $("#box").animate({
            left: '250px',
            top: '250px',
            opacity: 0.5
        }, 2000);
    });
});
</script>
```

---

## Callback - Działania po animacji

Callback to funkcja, która wykonuje się po zakończeniu animacji:

```javascript
$("#myDiv").slideDown(1000, function() {
    console.log("Animacja slideDown zakończona!");
    $(this).css("border", "2px solid red");
});

// Lub z .animate()
$("#myDiv").animate({ left: '100px' }, 1000, function() {
    $(this).addClass("animated");
});
```

### Sekwencja animacji

Możesz łączyć animacje w sekwencję:

```javascript
$("#myDiv")
    .slideDown(1000)  // Najpierw rozwiń
    .animate({ left: '100px' }, 1000)  // Potem animuj pozycję
    .fadeOut(1000);  // Na koniec zanikaj
```

---

## .delay() - Opóźnienie

```javascript
$("#myDiv")
    .slideDown(1000)
    .delay(2000)  // Czekaj 2 sekundy
    .slideUp(1000);
```

---

## .stop() - Zatrzymanie animacji

```javascript
$("#myDiv").animate({ left: '200px' }, 2000);

// Po 500ms zatrzymaj animację
setTimeout(function() {
    $("#myDiv").stop();
}, 500);

// Lub kliknięciem
$("#stopBtn").on("click", function() {
    $("#myDiv").stop();
});
```

---

## Ćwiczenie 1: Efekty podstawowe

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="box" style="width:100px; height:100px; background-color:green;"></div>

<button id="btn1">Show</button>
<button id="btn2">Hide</button>
<button id="btn3">Toggle</button>

<script>
$(function() {
    // Zadanie: Obsługuj każdy przycisk odpowiednim efektem
    // Wszystkie efekty powinny trwać 500ms
    // ...
});
</script>

</body>
</html>
```

### Rozwiązanie
```javascript
$(function() {
    $("#btn1").on("click", function() {
        $("#box").show(500);
    });
    
    $("#btn2").on("click", function() {
        $("#box").hide(500);
    });
    
    $("#btn3").on("click", function() {
        $("#box").toggle(500);
    });
});
```

---

## Ćwiczenie 2: Fade efekty

### Polecenie

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="fadebox" style="width:100px; height:100px; background-color:purple;"></div>

<button id="fadeInBtn">Fade In</button>
<button id="fadeOutBtn">Fade Out</button>
<button id="fadeToggleBtn">Fade Toggle</button>
<button id="fadeToBtn">Fade to 30%</button>

<script>
$(function() {
    // Obsługuj każdy przycisk odpowiednim efektem fade
    // Czas trwania: 1000ms
    // ...
});
</script>

</body>
</html>
```

### Rozwiązanie
```javascript
$(function() {
    $("#fadeInBtn").on("click", function() {
        $("#fadebox").fadeIn(1000);
    });
    
    $("#fadeOutBtn").on("click", function() {
        $("#fadebox").fadeOut(1000);
    });
    
    $("#fadeToggleBtn").on("click", function() {
        $("#fadebox").fadeToggle(1000);
    });
    
    $("#fadeToBtn").on("click", function() {
        $("#fadebox").fadeTo(1000, 0.3);
    });
});
```

---

## Ćwiczenie 3: Animacja niestandardowa

### Polecenie

Stwórz animacje, które przesuwają element po ekranie:

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        #animbox {
            width: 50px;
            height: 50px;
            background-color: orange;
            position: absolute;
            left: 0;
            top: 100px;
        }
    </style>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div id="animbox"></div>

<button id="moveRight">Przesuń w prawo</button>
<button id="moveDown">Przesuń w dół</button>
<button id="reset">Reset</button>
<button id="stop">Stop</button>

<script>
$(function() {
    // Zadanie 1: #moveRight - animuj left do 300px w 1 sekundę
    // ...
    
    // Zadanie 2: #moveDown - animuj top do 400px w 1 sekundę
    // ...
    
    // Zadanie 3: #reset - wróć do pozycji początkowej
    // ...
    
    // Zadanie 4: #stop - zatrzymaj bieżącą animację
    // ...
});
</script>

</body>
</html>
```

### Rozwiązanie
```javascript
$(function() {
    $("#moveRight").on("click", function() {
        $("#animbox").animate({ left: '300px' }, 1000);
    });
    
    $("#moveDown").on("click", function() {
        $("#animbox").animate({ top: '400px' }, 1000);
    });
    
    $("#reset").on("click", function() {
        $("#animbox").animate({ 
            left: '0',
            top: '100px'
        }, 1000);
    });
    
    $("#stop").on("click", function() {
        $("#animbox").stop();
    });
});
```

---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Jak używać efektów Show/Hide/Toggle
- Jak tworzyć zanikające animacje (Fade)
- Jak tworzyć efekty przesuwania (Slide)
- Jak tworzyć niestandardowe animacje
- Jak sekwencjonować animacje
- Jak używać callbacków i opóźnień

**Kolejna lekcja:** Filtrowanie i nawigacja po DOM - nauczymy się dokładnie wyszukiwać i poruszać się po elementach!
