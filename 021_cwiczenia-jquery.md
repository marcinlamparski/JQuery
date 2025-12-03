# Ćwiczenia podsumowujące: jQuery Moduł 1 i 2

## Wprowadzenie
Poniższe ćwiczenia sprawdzają wiedzę z **Lekcji 1 (Wprowadzenie do jQuery)** oraz **Lekcji 2 (Selektory jQuery)**. Każde ćwiczenie zawiera polecenie, szablon HTML do uzupełnienia oraz wskazówkę naprowadzającą na rozwiązanie.

---

## Ćwiczenie 1: Przełącznik widoczności

### Polecenie
Stwórz stronę z trzema elementami `<div>` o różnych ID (`box1`, `box2`, `box3`) oraz trzema przyciskami. Kliknięcie na przycisk powinno ukryć odpowiadający mu element div. Dodatkowo dodaj jeden przycisk "Pokaż wszystko", który wyświetli wszystkie ukryte elementy.

### Szablon do uzupełnienia

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie 1 - Przełącznik widoczności</title>
    <!-- DODAJ TU LINK DO jQuery -->
</head>
<body>

<h1>Przełącznik widoczności</h1>

<!-- DODAJ TU TRZY DIVY Z ID: box1, box2, box3 -->
<!-- Każdy div powinien mieć jakąś zawartość tekstową -->

<!-- DODAJ TU CZTERY PRZYCISKI -->
<!-- Trzy przyciski do ukrywania poszczególnych boxów -->
<!-- Jeden przycisk "Pokaż wszystko" -->

<script>
$(function() {
    // TUTAJ NAPISZ KOD
    // 1. Obsłuż kliknięcie każdego przycisku ukrywającego
    // 2. Obsłuż kliknięcie przycisku "Pokaż wszystko"
});
</script>

</body>
</html>
```

### Wskazówka
Zastanów się nad metodami `.hide()` i `.show()`. Aby wybrać wszystkie trzy elementy jednocześnie, możesz użyć **selektora wielokrotnego** z przecinkiem lub wspólnej klasy dla wszystkich boxów.

---

## Ćwiczenie 2: Kolorowanie tabeli

### Polecenie
Masz tabelę z listą produktów. Napisz kod jQuery, który:
1. Pokoloruje wiersze parzyste na jasnoszary (#f2f2f2)
2. Pokoloruje wiersze nieparzyste na biały (#ffffff)
3. Nagłówek tabeli (`<th>`) powinien mieć ciemnoniebieskie tło (#2c3e50) i biały tekst
4. Po najechaniu myszką na wiersz (nie nagłówek), wiersz powinien zmienić kolor tła na jasnożółty

### Szablon do uzupełnienia

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie 2 - Kolorowanie tabeli</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        table { border-collapse: collapse; width: 100%; }
        td, th { border: 1px solid #ddd; padding: 8px; }
    </style>
</head>
<body>

<h1>Lista produktów</h1>

<table id="products">
    <tr>
        <th>Nazwa</th>
        <th>Cena</th>
        <th>Ilość</th>
    </tr>
    <tr>
        <td>Laptop</td>
        <td>3500 zł</td>
        <td>10</td>
    </tr>
    <tr>
        <td>Monitor</td>
        <td>800 zł</td>
        <td>25</td>
    </tr>
    <tr>
        <td>Klawiatura</td>
        <td>150 zł</td>
        <td>50</td>
    </tr>
    <tr>
        <td>Mysz</td>
        <td>80 zł</td>
        <td>100</td>
    </tr>
</table>

<script>
$(function() {
    // TUTAJ NAPISZ KOD
    // 1. Pokoloruj wiersze parzyste/nieparzyste
    // 2. Styluj nagłówek
    // 3. Dodaj efekt hover na wiersze (oprócz nagłówka)
});
</script>

</body>
</html>
```

### Wskazówka
Użyj pseudo-selektorów `:even` i `:odd` dla wierszy. Pamiętaj, że indeksowanie zaczyna się od 0 (pierwszy wiersz to nagłówek). Do obsługi najechania myszką użyj metod `.on("mouseenter", ...)` i `.on("mouseleave", ...)`. Rozważ użycie selektora `tr:gt(0)`, który wybiera wiersze z indeksem większym niż 0.

Korzystaj z dokumentacji np na stronie jquery z metodą mouseleave: https://api.jquery.com/mouseleave-shorthand/

---

## Ćwiczenie 3: Wyszukiwanie na liście

### Polecenie
Stwórz pole tekstowe do wyszukiwania oraz listę elementów. Po kliknięciu przycisku "Szukaj", ukryj wszystkie elementy listy, które NIE zawierają wpisanej frazy, a pokaż te, które ją zawierają.

### Szablon do uzupełnienia

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie 3 - Wyszukiwarka</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<h1>Wyszukiwarka owoców</h1>

<input type="text" id="searchInput" placeholder="Wpisz nazwę owocu...">
<button id="searchBtn">Szukaj</button>
<button id="resetBtn">Reset</button>

<ul id="fruitList">
    <li>Jabłko</li>
    <li>Banan</li>
    <li>Pomarańcza</li>
    <li>Gruszka</li>
    <li>Winogrono</li>
    <li>Arbuz</li>
    <li>Truskawka</li>
    <li>Malina</li>
</ul>

<script>
$(function() {
    // TUTAJ NAPISZ KOD
    // 1. Pobierz wartość z pola tekstowego po kliknięciu "Szukaj"
    // 2. Ukryj elementy, które nie zawierają szukanej frazy
    // 3. Pokaż elementy, które zawierają szukaną frazę
    // 4. Przycisk "Reset" powinien pokazać wszystkie elementy
});
</script>

</body>
</html>
```

### Wskazówka
Do pobrania wartości z pola tekstowego użyj metody `.val()`. Do filtrowania elementów zawierających tekst użyj pseudo-selektora `:contains()`. Pamiętaj, że możesz użyć zaprzeczenia - najpierw ukryj wszystkie, potem pokaż pasujące, lub użyj kombinacji selektorów.

---

## Ćwiczenie 4: Formularz rejestracji

### Polecenie
Stwórz prosty formularz rejestracji z polami: nazwa użytkownika, email i hasło. Po kliknięciu przycisku "Sprawdź":
1. Zaznacz na czerwono obramowanie wszystkich pustych pól
2. Zaznacz na zielono obramowanie pól, które są wypełnione
3. Wyświetl komunikat pod formularzem informujący, ile pól wymaga uzupełnienia

### Szablon do uzupełnienia

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie 4 - Formularz</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        input { display: block; margin: 10px 0; padding: 8px; width: 200px; }
        .error { border: 2px solid red; }
        .valid { border: 2px solid green; }
    </style>
</head>
<body>

<h1>Formularz rejestracji</h1>

<form id="registerForm">
    <input type="text" name="username" placeholder="Nazwa użytkownika">
    <input type="email" name="email" placeholder="Email">
    <input type="password" name="password" placeholder="Hasło">
    <button type="button" id="checkBtn">Sprawdź</button>
</form>

<p id="message"></p>

<script>
$(function() {
    // TUTAJ NAPISZ KOD
    // 1. Pobierz wszystkie pola input w formularzu
    // 2. Sprawdź, które są puste
    // 3. Dodaj odpowiednią klasę CSS
    // 4. Wyświetl komunikat
});
</script>

</body>
</html>
```

### Wskazówka
Do iteracji po elementach możesz użyć metody `.each()`. Sprawdzenie, czy pole jest puste, można zrobić przez `$(this).val() === ""`. Do dodawania i usuwania klas użyj metod `.addClass()` i `.removeClass()`. Możesz też wykorzystać selektor `:text`, `:password` oraz selektor atrybutu `[type='email']`.

---

## Ćwiczenie 5: Menu nawigacyjne

### Polecenie
Stwórz menu nawigacyjne z kilkoma pozycjami. Kliknięcie na pozycję menu powinno:
1. Podświetlić wybraną pozycję (dodać klasę "active" z żółtym tłem)
2. Usunąć podświetlenie z poprzednio wybranej pozycji
3. Wyświetlić poniżej tekst "Wybrano: [nazwa pozycji]"

### Szablon do uzupełnienia

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie 5 - Menu nawigacyjne</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        #menu { list-style: none; padding: 0; }
        #menu li { 
            padding: 10px 20px; 
            background: #3498db; 
            color: white; 
            margin: 2px 0;
            cursor: pointer;
        }
        #menu li:hover { background: #2980b9; }
        #menu li.active { background: #f1c40f; color: black; }
    </style>
</head>
<body>

<h1>Menu nawigacyjne</h1>

<ul id="menu">
    <li>Strona główna</li>
    <li>O nas</li>
    <li>Usługi</li>
    <li>Portfolio</li>
    <li>Kontakt</li>
</ul>

<p id="selected">Wybrano: brak</p>

<script>
$(function() {
    // TUTAJ NAPISZ KOD
    // 1. Obsłuż kliknięcie na każdy element <li> w menu
    // 2. Usuń klasę "active" ze wszystkich elementów
    // 3. Dodaj klasę "active" do klikniętego elementu
    // 4. Wyświetl tekst klikniętego elementu w paragrafie
});
</script>

</body>
</html>
```

### Wskazówka
Aby obsłużyć kliknięcie na wszystkie elementy `<li>` jednocześnie, użyj selektora `#menu li`. Wewnątrz funkcji obsługi zdarzenia, `$(this)` odnosi się do klikniętego elementu. Metoda `.text()` bez argumentów zwraca tekst elementu.

---

## Ćwiczenie 6: Dynamiczna galeria

### Polecenie
Stwórz prostą galerię z miniaturami (4 małe divy reprezentujące obrazki). Po kliknięciu na miniaturę:
1. Duży div "podgląd" powinien zmienić swój kolor tła na kolor miniatury
2. Pod podglądem powinien wyświetlić się tekst z numerem wybranej miniatury (np. "Obrazek 3")
3. Wybrana miniatura powinna otrzymać obramowanie

### Szablon do uzupełnienia

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ćwiczenie 6 - Galeria</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        .thumbnail { 
            width: 50px; 
            height: 50px; 
            display: inline-block; 
            margin: 5px; 
            cursor: pointer;
        }
        .thumbnail.selected { border: 3px solid black; }
        #preview { 
            width: 200px; 
            height: 200px; 
            background: #ccc; 
            margin: 20px 0;
        }
    </style>
</head>
<body>

<h1>Galeria</h1>

<div id="thumbnails">
    <div class="thumbnail" data-color="#e74c3c" data-number="1" style="background: #e74c3c;"></div>
    <div class="thumbnail" data-color="#3498db" data-number="2" style="background: #3498db;"></div>
    <div class="thumbnail" data-color="#2ecc71" data-number="3" style="background: #2ecc71;"></div>
    <div class="thumbnail" data-color="#9b59b6" data-number="4" style="background: #9b59b6;"></div>
</div>

<div id="preview"></div>
<p id="imageInfo">Wybierz obrazek</p>

<script>
$(function() {
    // TUTAJ NAPISZ KOD
    // 1. Obsłuż kliknięcie na miniaturę
    // 2. Pobierz kolor z atrybutu data-color
    // 3. Pobierz numer z atrybutu data-number
    // 4. Zmień tło podglądu
    // 5. Wyświetl informację o wybranym obrazku
    // 6. Zaznacz wybraną miniaturę
});
</script>

</body>
</html>
```

### Wskazówka
Do pobierania wartości atrybutów `data-*` użyj metody `.data()` lub `.attr()`. Na przykład `$(this).data("color")` zwróci wartość atrybutu `data-color`. Aby zmienić tło elementu, użyj `.css("background-color", kolor)`. Pamiętaj o usunięciu klasy "selected" z innych miniatur przed dodaniem jej do aktualnie klikniętej.

---

## Podsumowanie

Te ćwiczenia sprawdzają umiejętności z zakresu:
- ✅ Podstawowej składni jQuery i `$(document).ready()`
- ✅ Selektorów ID, klas i tagów
- ✅ Selektorów hierarchicznych (potomków, dzieci)
- ✅ Pseudo-selektorów (`:even`, `:odd`, `:first`, `:last`, `:contains()`)
- ✅ Selektorów atrybutów
- ✅ Obsługi zdarzeń (`.on("click", ...)`)
- ✅ Manipulacji stylami CSS (`.css()`)
- ✅ Manipulacji klasami (`.addClass()`, `.removeClass()`)
- ✅ Pobierania i ustawiania wartości (`.text()`, `.val()`)
- ✅ Pokazywania i ukrywania elementów (`.show()`, `.hide()`)

**Powodzenia!** 🚀

Miejsce na wysłanie plików: 

https://www.dropbox.com/request/MywwO8yCocsHWLCB2Rns
