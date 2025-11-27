# Lekcja 9: jQuery UI - Komponenty interfejsu

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Instalować i używać jQuery UI
- Tworzyć interaktywne dialogi
- Używać datepickera
- Tworzyć elementy surowalne (draggable)
- Tworzyć zakresy wartości (slider)

---

## Co to jest jQuery UI?

**jQuery UI** to biblioteka dodatków do jQuery zawierająca gotowe komponenty:
- Dialogi (okna modalne)
- Datepicker (selektor daty)
- Slider (suwak)
- Sortable (sortowanie elementów)
- Draggable (przeciąganie)
- I wiele więcej...

---

## Instalacja jQuery UI

Dodaj w sekcji `<head>`:

```html
<!-- CSS jQuery UI -->
<link rel="stylesheet" href="https://code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">

<!-- jQuery -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<!-- jQuery UI JS -->
<script src="https://code.jquery.com/ui/1.12.1/jquery-ui.min.js"></script>
```

---

## Dialog - Okno modalne

### Podstawowy dialog

```html
<div id="dialog" title="Okno dialogowe">
    <p>Treść dialogu</p>
</div>

<button id="openDialog">Otwórz dialog</button>

<script>
$(function() {
    // Inicjalizacja dialogu
    $("#dialog").dialog({
        autoOpen: false,  // Nie otwieraj automatycznie
        width: 400,
        height: 300
    });
    
    // Otwórz dialog na kliknięcie
    $("#openDialog").on("click", function() {
        $("#dialog").dialog("open");
    });
});
</script>
```

### Opcje dialogu

```javascript
$("#dialog").dialog({
    autoOpen: false,      // Czy otwierać automatycznie
    width: 500,           // Szerokość
    height: 300,          // Wysokość
    modal: true,          // Dialog modalny (nieaktywna reszta strony)
    buttons: {
        "OK": function() {
            $(this).dialog("close");
        },
        "Anuluj": function() {
            $(this).dialog("close");
        }
    }
});
```

---

## Datepicker - Selektor daty

### Podstawowy datepicker

```html
<input type="text" id="datepicker">

<script>
$(function() {
    $("#datepicker").datepicker({
        dateFormat: "dd-mm-yy"  // Format daty
    });
});
</script>
```

### Opcje datepickera

```javascript
$("#datepicker").datepicker({
    dateFormat: "yy-mm-dd",        // Format: YYYY-MM-DD
    minDate: new Date(2024, 0, 1),  // Minimalna data
    maxDate: new Date(2025, 11, 31), // Maksymalna data
    language: "pl"                  // Język (jeśli zainstalowany)
});
```

### Praktyka - Data z datepickera

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="https://code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.min.js"></script>
</head>
<body>

<label>Wybierz datę:</label>
<input type="text" id="datepicker">
<button id="showBtn">Pokaż datę</button>
<div id="result"></div>

<script>
$(function() {
    $("#datepicker").datepicker({
        dateFormat: "yy-mm-dd"
    });
    
    $("#showBtn").on("click", function() {
        var data = $("#datepicker").val();
        $("#result").text("Wybrana data: " + data);
    });
});
</script>

</body>
</html>
```

---

## Slider - Suwak

```html
<div id="slider"></div>
<p>Wartość: <span id="sliderValue">50</span></p>

<script>
$(function() {
    $("#slider").slider({
        min: 0,
        max: 100,
        value: 50,
        slide: function(event, ui) {
            $("#sliderValue").text(ui.value);
        }
    });
});
</script>
```

### Slider zakresu

```html
<div id="rangeSlider"></div>
<p>Min: <span id="min">20</span> Max: <span id="max">80</span></p>

<script>
$(function() {
    $("#rangeSlider").slider({
        range: true,
        min: 0,
        max: 100,
        values: [20, 80],
        slide: function(event, ui) {
            $("#min").text(ui.values[0]);
            $("#max").text(ui.values[1]);
        }
    });
});
</script>
```

---

## Draggable - Przeciąganie

```html
<div id="draggable" style="width:100px; height:100px; background-color:blue; cursor:move;">
    Przeciągnij mnie
</div>

<script>
$(function() {
    $("#draggable").draggable({
        cursor: "move"
    });
});
</script>
```

### Opcje draggable

```javascript
$("#draggable").draggable({
    containment: "#parent",  // Ograniczenie do rodzica
    snap: true,              // Magnetyczne przyleganie
    grid: [10, 10]          // Siatka 10x10 pikseli
});
```

---

## Sortable - Sortowanie

```html
<ul id="sortable">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

<script>
$(function() {
    $("#sortable").sortable({
        update: function() {
            console.log("Kolejność zmieniona");
        }
    });
    
    $("#sortable").disableSelection();  // Zablokuj zaznaczanie
});
</script>
```

---

## Tabs - Karty

```html
<div id="tabs">
    <ul>
        <li><a href="#tab1">Karta 1</a></li>
        <li><a href="#tab2">Karta 2</a></li>
    </ul>
    
    <div id="tab1">
        <p>Zawartość karty 1</p>
    </div>
    
    <div id="tab2">
        <p>Zawartość karty 2</p>
    </div>
</div>

<script>
$(function() {
    $("#tabs").tabs();
});
</script>
```

---

## Accordion - Akordeon

```html
<div id="accordion">
    <h3>Sekcja 1</h3>
    <div>
        <p>Zawartość 1</p>
    </div>
    
    <h3>Sekcja 2</h3>
    <div>
        <p>Zawartość 2</p>
    </div>
</div>

<script>
$(function() {
    $("#accordion").accordion({
        collapsible: true  // Pozwól na zwinięcie wszystkich
    });
});
</script>
```

---

## Ćwiczenie 1: Dialog

### Polecenie

Stwórz dialog z przyciskami:

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="https://code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.min.js"></script>
</head>
<body>

<button id="openBtn">Otwórz dialog</button>

<div id="myDialog" title="Potwierdź akcję">
    <p>Czy na pewno chcesz kontynuować?</p>
</div>

<div id="result"></div>

<script>
$(function() {
    // Zadanie: Inicjalizuj dialog z opcjami:
    // - modal: true
    // - autoOpen: false
    // - Dwa przyciski: "TAK" i "NIE"
    // Po kliknięciu TAK, wyświetl "Potwierdzona" w #result
    // Po kliknięciu NIE, wyświetl "Anulowana" w #result
    // ...
});
</script>

</body>
</html>
```

### Rozwiązanie
```javascript
$(function() {
    $("#myDialog").dialog({
        modal: true,
        autoOpen: false,
        buttons: {
            "TAK": function() {
                $("#result").text("Potwierdzona");
                $(this).dialog("close");
            },
            "NIE": function() {
                $("#result").text("Anulowana");
                $(this).dialog("close");
            }
        }
    });
    
    $("#openBtn").on("click", function() {
        $("#myDialog").dialog("open");
    });
});
```

---

## Podsumowanie lekcji

✅ Wiesz teraz:
- Jak zainstalować jQuery UI
- Jak tworzyć dialogi
- Jak używać datepickera
- Jak tworzyć suwaki
- Jak robić elementy przeciągalne
- Jak sortować elementy

**Ostatnia lekcja:** Projekt całej aplikacji ToDo!
