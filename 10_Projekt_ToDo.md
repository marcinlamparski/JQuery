# Lekcja 10: Projekt - Aplikacja ToDo

## Cele lekcji
Po ukończeniu tej lekcji będziesz potrafić:
- Tworzyć złożoną aplikację web
- Łączyć wiele funkcjonalności jQuery
- Pracować z danymi w localStorage
- Budować responsywny interfejs

---

## Opis projektu

Stworzymy **aplikację zadań (ToDo List)** z funkcjami:
- ✅ Dodawanie nowych zadań
- ✅ Zaznaczanie zadań jako ukończone
- ✅ Usuwanie zadań
- ✅ Filtrowanie zadań (wszystkie, aktywne, ukończone)
- ✅ Zapisywanie danych w localStorage
- ✅ Licznik zadań

---

## Struktura HTML

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikacja ToDo</title>
    <link rel="stylesheet" href="style.css">
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>

<div class="container">
    <h1>Moja Lista Zadań</h1>
    
    <!-- Formularz dodawania zadania -->
    <form id="addForm">
        <input type="text" id="taskInput" placeholder="Dodaj nowe zadanie..." required>
        <button type="submit" id="addBtn">Dodaj</button>
    </form>
    
    <!-- Filtry -->
    <div id="filters">
        <button class="filter active" data-filter="all">Wszystkie (<span id="countAll">0</span>)</button>
        <button class="filter" data-filter="active">Aktywne (<span id="countActive">0</span>)</button>
        <button class="filter" data-filter="completed">Ukończone (<span id="countCompleted">0</span>)</button>
    </div>
    
    <!-- Lista zadań -->
    <ul id="taskList"></ul>
    
    <!-- Przycisk wyczyść -->
    <button id="clearCompleted" class="btn-secondary">Wyczyść ukończone</button>
</div>

<script src="script.js"></script>

</body>
</html>
```

---

## Strukturа CSS

```css
/* style.css */

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: 0 auto;
    background-color: white;
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

h1 {
    color: #333;
    margin-bottom: 20px;
    text-align: center;
}

/* Formularz */
#addForm {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

#taskInput {
    flex: 1;
    padding: 10px;
    border: 2px solid #ddd;
    border-radius: 4px;
    font-size: 16px;
}

#taskInput:focus {
    outline: none;
    border-color: #4CAF50;
    background-color: #f9fff9;
}

#addBtn {
    padding: 10px 20px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
}

#addBtn:hover {
    background-color: #45a049;
}

/* Filtry */
#filters {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
    justify-content: center;
    flex-wrap: wrap;
}

.filter {
    padding: 8px 15px;
    border: 2px solid #ddd;
    background-color: white;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s;
}

.filter:hover {
    border-color: #4CAF50;
}

.filter.active {
    background-color: #4CAF50;
    color: white;
    border-color: #4CAF50;
}

/* Lista zadań */
#taskList {
    list-style: none;
    margin-bottom: 20px;
}

.task-item {
    display: flex;
    align-items: center;
    padding: 12px;
    background-color: #f9f9f9;
    border: 1px solid #eee;
    border-radius: 4px;
    margin-bottom: 10px;
    gap: 10px;
    animation: slideIn 0.3s ease-in;
}

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateY(-10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.task-item.completed {
    opacity: 0.6;
}

.task-item.completed .task-text {
    text-decoration: line-through;
    color: #999;
}

.task-checkbox {
    width: 20px;
    height: 20px;
    cursor: pointer;
}

.task-text {
    flex: 1;
    color: #333;
    font-size: 16px;
}

.task-delete {
    padding: 5px 10px;
    background-color: #f44336;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 12px;
}

.task-delete:hover {
    background-color: #da190b;
}

.btn-secondary {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #666;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
}

.btn-secondary:hover {
    background-color: #555;
}

.empty-message {
    text-align: center;
    color: #999;
    padding: 20px;
    font-style: italic;
}

.hidden {
    display: none;
}
```

---

## Logika JavaScript

```javascript
// script.js

$(function() {
    // === ZMIENNE ===
    var tasks = [];
    var currentFilter = 'all';
    var STORAGE_KEY = 'todoTasks';
    
    // === INICJALIZACJA ===
    loadTasks();
    renderTasks();
    updateCounts();
    
    // === EVENT LISTENERY ===
    
    // Dodaj nowe zadanie
    $("#addForm").on("submit", function(e) {
        e.preventDefault();
        var taskText = $("#taskInput").val().trim();
        
        if (taskText === "") return;
        
        var newTask = {
            id: Date.now(),
            text: taskText,
            completed: false,
            createdAt: new Date().toLocaleString()
        };
        
        tasks.push(newTask);
        saveTasks();
        renderTasks();
        updateCounts();
        
        $("#taskInput").val("");
        $("#taskInput").focus();
    });
    
    // Zaznacz/Odznacz zadanie
    $("#taskList").on("change", ".task-checkbox", function() {
        var taskId = $(this).closest(".task-item").data("id");
        toggleTask(taskId);
    });
    
    // Usuń zadanie
    $("#taskList").on("click", ".task-delete", function() {
        var taskId = $(this).closest(".task-item").data("id");
        deleteTask(taskId);
    });
    
    // Filtry
    $(".filter").on("click", function() {
        $(".filter").removeClass("active");
        $(this).addClass("active");
        
        currentFilter = $(this).data("filter");
        renderTasks();
    });
    
    // Wyczyść ukończone
    $("#clearCompleted").on("click", function() {
        if (confirm("Czy na pewno chcesz usunąć wszystkie ukończone zadania?")) {
            tasks = tasks.filter(function(task) {
                return !task.completed;
            });
            saveTasks();
            renderTasks();
            updateCounts();
        }
    });
    
    // === FUNKCJE ===
    
    function loadTasks() {
        var stored = localStorage.getItem(STORAGE_KEY);
        if (stored) {
            tasks = JSON.parse(stored);
        }
    }
    
    function saveTasks() {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(tasks));
    }
    
    function toggleTask(id) {
        var task = tasks.find(function(t) {
            return t.id === id;
        });
        if (task) {
            task.completed = !task.completed;
            saveTasks();
            renderTasks();
            updateCounts();
        }
    }
    
    function deleteTask(id) {
        tasks = tasks.filter(function(t) {
            return t.id !== id;
        });
        saveTasks();
        renderTasks();
        updateCounts();
    }
    
    function renderTasks() {
        var filteredTasks = getFilteredTasks();
        var html = "";
        
        if (filteredTasks.length === 0) {
            html = '<li class="empty-message">Brak zadań do wyświetlenia</li>';
        } else {
            $.each(filteredTasks, function(index, task) {
                var completedClass = task.completed ? "completed" : "";
                var checkedAttr = task.completed ? "checked" : "";
                
                html += '<li class="task-item ' + completedClass + '" data-id="' + task.id + '">';
                html += '  <input type="checkbox" class="task-checkbox" ' + checkedAttr + '>';
                html += '  <span class="task-text">' + escapeHtml(task.text) + '</span>';
                html += '  <button class="task-delete">Usuń</button>';
                html += '</li>';
            });
        }
        
        $("#taskList").html(html);
    }
    
    function getFilteredTasks() {
        switch(currentFilter) {
            case 'active':
                return tasks.filter(function(t) {
                    return !t.completed;
                });
            case 'completed':
                return tasks.filter(function(t) {
                    return t.completed;
                });
            default:
                return tasks;
        }
    }
    
    function updateCounts() {
        var allCount = tasks.length;
        var activeCount = tasks.filter(function(t) {
            return !t.completed;
        }).length;
        var completedCount = tasks.filter(function(t) {
            return t.completed;
        }).length;
        
        $("#countAll").text(allCount);
        $("#countActive").text(activeCount);
        $("#countCompleted").text(completedCount);
    }
    
    function escapeHtml(text) {
        return $("<div>").text(text).html();
    }
});
```

---

## Rozszerzenie funkcjonalności - Wersja zaawansowana

### Dodaj edytowanie zadań

```javascript
// Dodaj pole do HTML na kliknięcie
$("#taskList").on("dblclick", ".task-text", function() {
    var taskId = $(this).closest(".task-item").data("id");
    var task = tasks.find(function(t) {
        return t.id === taskId;
    });
    
    if (task) {
        var newText = prompt("Edytuj zadanie:", task.text);
        if (newText && newText.trim() !== "") {
            task.text = newText.trim();
            saveTasks();
            renderTasks();
        }
    }
});
```

### Sortowanie zadań

```javascript
// Dodaj do filtrów
var sortOptions = {
    newest: function(a, b) {
        return b.id - a.id;  // Najnowsze na górze
    },
    oldest: function(a, b) {
        return a.id - b.id;  // Najstarsze na górze
    },
    alphabetical: function(a, b) {
        return a.text.localeCompare(b.text);
    }
};
```

---

## Ćwiczenie - Samodzielnie implementuj

### Polecenie

Stwórz pełną aplikację ToDo z funkcjami:
1. Dodawanie i usuwanie zadań
2. Zaznaczanie jako ukończone
3. Filtrowanie
4. Zapisywanie w localStorage
5. Liczniki zadań

### Wskazówka
- Zacznij od HTML i CSS
- Później napisz funkcje JavaScript
- Testuj każdą funkcję osobno
- Używaj console.log() do debugowania

### Punkty kontrolne

- [ ] Formularz działa - można dodać zadanie
- [ ] Zadania wyświetlają się na liście
- [ ] Checkbox zaznacza zadanie
- [ ] Przycisk Usuń działa
- [ ] Filtry działają
- [ ] Liczniki się aktualizują
- [ ] Dane zapisują się w localStorage
- [ ] Po przeładowaniu strony zadania zostają

---

## Testowanie aplikacji

1. Dodaj kilka zadań
2. Zaznacz jedno jako ukończone
3. Przełączaj się między filtrami
4. Przeładuj stronę - dane powinny zostać
5. Usuń wszystkie ukończone
6. Sprawdź konsolę (F12) czy nie ma błędów

---

## Podsumowanie kursu

🎉 **Gratulacje! Ukończyłeś kurs jQuery!**

### Co nauczyłeś się:

✅ Instalacja i konfiguracja jQuery
✅ Selektory i DOM manipulation
✅ Obsługa zdarzeń
✅ Efekty i animacje
✅ Filtrowanie i nawigacja
✅ Walidacja formularzy
✅ AJAX i komunikacja z serwerem
✅ jQuery UI i komponenty
✅ Tworzenie złożonych aplikacji

### Kolejne kroki:

1. **Ćwicz** - Stwórz własne projekty
2. **Eksperymentuj** - Dodawaj nowe funkcje
3. **Ucz się** - Przejdź do React/Vue/Angular
4. **Praktykuj** - Rób projekty dla portfolio

### Zasoby dodatkowe:

- [jQuery API Documentation](https://api.jquery.com/)
- [jQuery Learning Center](https://learn.jquery.com/)
- [W3Schools jQuery](https://www.w3schools.com/jquery/)
- [jQuery Fundamentals](https://jqfundamentals.com/)

---

## Powodzenia! 🚀
