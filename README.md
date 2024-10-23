# OOP Python (Czyli python obiektowo)

## 1. Podstawowe pojęcia obiektowości

### Klasa
Klasa to szablon do tworzenia obiektów. Definiuje atrybuty (zmienne) oraz metody (funkcje), które będą dostępne dla obiektów tej klasy.
```python
class MyClass:
    def __init__(self, name, age):
        # Konstruktor inicjalizujący atrybuty
        self.name = name
        self.age = age

    def greet(self):
        # Przykładowa metoda
        return f"Cześć, jestem {self.name} i mam {self.age} lat."
```
### Obiekt
Obiekt to instancja klasy. Poniżej przykład tworzenia obiektu i używania jego metod.
```python
# Tworzenie obiektu klasy
person = MyClass("Jan", 30)

# Wywołanie metody obiektu
print(person.greet())  # Output: Cześć, jestem Jan i mam 30 lat.
```
## 2. Dziedziczenie

Dziedziczenie pozwala tworzyć nowe klasy, które dziedziczą właściwości i metody z istniejących klas.
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} wydaje dźwięk."

# Dziedziczenie po klasie Animal
class Dog(Animal):
    def speak(self):
        return f"{self.name} szczeka."

# Tworzenie obiektu klasy Dog
dog = Dog("Burek")
print(dog.speak())  # Output: Burek szczeka.
```
## 3. Polimorfizm (Jak tego nie ogarniecie to wyjebane)

Polimorfizm oznacza możliwość używania tych samych metod przez różne klasy.
```python
class Cat(Animal):
    def speak(self):
        return f"{self.name} miauczy."

def animal_sound(animal):
    print(animal.speak())

dog = Dog("Burek")
cat = Cat("Mruczek")

animal_sound(dog)  # Output: Burek szczeka.
animal_sound(cat)  # Output: Mruczek miauczy.
```
## 4. Enkapsulacja

Enkapsulacja oznacza ukrywanie danych wewnątrz obiektu. W Pythonie możemy oznaczać atrybuty jako "prywatne" za pomocą podkreślenia `_` lub podwójnego podkreślenia `__`.
```python
class Person:
    def __init__(self, name, age):
        self.__age = age  # Atrybut prywatny

    def get_age(self):
        return self.__age

    def set_age(self, age):
        if age > 0:
            self.__age = age

person = Person("Adam", 25)
print(person.get_age())  # Output: 25
person.set_age(30)
print(person.get_age())  # Output: 30
```
## 5. Klasy abstrakcyjne i metody abstrakcyjne

Klasy abstrakcyjne zawierają metody, które muszą być zdefiniowane w klasach dziedziczących. W Pythonie używamy modułu `abc`.
```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def move(self):
        pass

class Car(Vehicle):
    def move(self):
        print("Samochód jedzie.")

class Bike(Vehicle):
    def move(self):
        print("Rower jedzie.")

car = Car()
car.move()  # Output: Samochód jedzie.

bike = Bike()
bike.move()  # Output: Rower jedzie.
```
## 6. Metody i atrybuty klasowe vs instancyjne

Atrybuty i metody klasowe dotyczą klasy jako całości, a nie konkretnego obiektu. Możemy je zdefiniować za pomocą dekoratora `@classmethod` lub po prostu przypisując je do samej klasy.

### Atrybuty klasowe
```python
class Car:
    wheels = 4  # Atrybut klasowy

    def __init__(self, color):
        self.color = color  # Atrybut instancyjny

car1 = Car("czerwony")
car2 = Car("niebieski")

print(car1.wheels)  # Output: 4
print(car2.wheels)  # Output: 4
```
### Metody klasowe
```python
class Car:
    wheels = 4

    @classmethod
    def change_wheels(cls, wheels):
        cls.wheels = wheels

Car.change_wheels(6)
print(Car.wheels)  # Output: 6
```

## 7. Dziedziczenie wielokrotne

W Pythonie można dziedziczyć po więcej niż jednej klasie.
```python
class A:
    def method_a(self):
        print("Metoda z klasy A")

class B:
    def method_b(self):
        print("Metoda z klasy B")

class C(A, B):
    pass

c = C()
c.method_a()  # Output: Metoda z klasy A
c.method_b()  # Output: Metoda z klasy B
```
## 8. Metody specjalne (Dunder Methods)

W Pythonie istnieją specjalne metody (tzw. "dunder methods"), które definiują zachowanie obiektów w różnych sytuacjach.

### Przykład metody `__str__` (reprezentacja tekstowa obiektu):
```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    def __str__(self):
        return f"{self.title} napisana przez {self.author}"

book = Book("Python 101", "Jan Kowalski")
print(book)  # Output: Python 101 napisana przez Jan Kowalski
```
### Przykład przeciążenia operatorów:
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"({self.x}, {self.y})"

v1 = Vector(2, 3)
v2 = Vector(1, 5)
result = v1 + v2
print(result)  # Output: (3, 8)
```
## Podsumowanie

1. **Klasy i obiekty**: Klasy definiują strukturę, a obiekty są ich instancjami.
2. **Dziedziczenie**: Pozwala rozszerzać funkcjonalność klas.
3. **Polimorfizm**: Różne klasy mogą mieć metody o tych samych nazwach, ale różnych zachowaniach.
4. **Enkapsulacja**: Ukrywanie danych wewnątrz klasy.


# PyQt5 Cheat Sheet

## 1. Tworzenie podstawowej aplikacji

### Minimalna aplikacja w PyQt5
Każda aplikacja w PyQt5 wymaga kilku podstawowych elementów: 
1. Import bibliotek PyQt5
2. Inicjalizacja aplikacji
3. Tworzenie okna głównego
4. Uruchomienie głównej pętli aplikacji

```python
from PyQt5.QtWidgets import QApplication, QWidget

class MyApp(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('Moja aplikacja PyQt5')
        self.setGeometry(100, 100, 300, 200)  # x, y, szerokość, wysokość
        self.show()

if __name__ == '__main__':
    app = QApplication([])  # Tworzymy instancję aplikacji
    window = MyApp()  # Tworzymy okno
    app.exec_()  # Uruchamiamy główną pętlę aplikacji
```
**Wyjaśnienie:**

- **QApplication**: Klasa odpowiedzialna za uruchomienie aplikacji.
- **QWidget**: Bazowa klasa dla interfejsu graficznego (GUI).
- **setWindowTitle()**: Ustawia tytuł okna.
- **setGeometry()**: Ustawia pozycję i wymiary okna.
- **show()**: Wyświetla okno.
- **exec_()**: Uruchamia pętlę aplikacji, oczekującą na interakcje użytkownika.

## 2. Kontrolki w PyQt5
PyQt5 oferuje wiele wbudowanych kontrolek. Poniżej znajduje się opis kilku z nich oraz przykładowy kod.

### 2.1. QPushButton - Przycisk
```python
from PyQt5.QtWidgets import QPushButton

btn = QPushButton('Kliknij mnie', window)
btn.move(100, 50)  # Pozycjonowanie przycisku w oknie
btn.clicked.connect(lambda: print('Przycisk kliknięty!'))
```

### 2.2. QLabel - Etykieta

```python
from PyQt5.QtWidgets import QLabel

label = QLabel('To jest etykieta', window)
label.move(100, 100)
```

### 2.3. QLineEdit - Pole tekstowe

```python
from PyQt5.QtWidgets import QLineEdit

textbox = QLineEdit(window)
textbox.move(100, 150)
```

### 2.4. QComboBox - Lista rozwijana

```python

from PyQt5.QtWidgets import QComboBox

combo = QComboBox(window)
combo.addItem("Opcja 1")
combo.addItem("Opcja 2")
combo.move(100, 200)
```

### 2.5. QCheckBox - Pole wyboru

```python
from PyQt5.QtWidgets import QCheckBox

checkbox = QCheckBox('Zgadzam się', window)
checkbox.move(100, 250)
```

### 2.6. QRadioButton - Przyciski radiowe

```python
from PyQt5.QtWidgets import QRadioButton

radio1 = QRadioButton('Opcja 1', window)
radio1.move(100, 300)

radio2 = QRadioButton('Opcja 2', window)
radio2.move(100, 350)
```

### 2.7. QSlider - Suwak

```python
from PyQt5.QtWidgets import QSlider
from PyQt5.QtCore import Qt

slider = QSlider(Qt.Horizontal, window)
slider.move(100, 400)
```

## Przykładowy program z wszystkimi kontrolkami

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QLabel, QLineEdit, QComboBox, QCheckBox, QRadioButton, QSlider
from PyQt5.QtCore import Qt

class MyApp(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('Przykład z kontrolkami')
        self.setGeometry(100, 100, 400, 500)

        # Przycisk
        self.btn = QPushButton('Kliknij mnie', self)
        self.btn.move(100, 50)
        self.btn.clicked.connect(self.button_clicked)

        # Etykieta
        self.label = QLabel('To jest etykieta', self)
        self.label.move(100, 100)

        # Pole tekstowe
        self.textbox = QLineEdit(self)
        self.textbox.move(100, 150)

        # Lista rozwijana
        self.combo = QComboBox(self)
        self.combo.addItem("Opcja 1")
        self.combo.addItem("Opcja 2")
        self.combo.move(100, 200)

        # Checkbox
        self.checkbox = QCheckBox('Zgadzam się', self)
        self.checkbox.move(100, 250)

        # RadioButton
        self.radio1 = QRadioButton('Opcja 1', self)
        self.radio1.move(100, 300)

        self.radio2 = QRadioButton('Opcja 2', self)
        self.radio2.move(100, 350)

        # Suwak
        self.slider = QSlider(Qt.Horizontal, self)
        self.slider.move(100, 400)

        self.show()

    # Funkcja obsługująca kliknięcie przycisku
    def button_clicked(self):
        print("Przycisk został kliknięty!")

app = QApplication(sys.argv)
window = MyApp()
sys.exit(app.exec_())

```
## 3. Łączenie sygnałów z funkcjami

W PyQt5, aby połączyć akcję (np. kliknięcie przycisku) z funkcją, używamy metody `connect()`.

#### Przykład połączenia przycisku z funkcją:
```python
class MyApp(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('Przykład z funkcją')
        self.setGeometry(100, 100, 300, 200)

        self.button = QPushButton('Kliknij mnie', self)
        self.button.setGeometry(100, 100, 100, 30)
        self.button.clicked.connect(self.button_clicked)

        self.show()

    def button_clicked(self):
        print("Przycisk został kliknięty!")
```
## 4. Korzystanie z QtDesigner

QtDesigner to narzędzie graficzne, które pozwala tworzyć interfejsy użytkownika w sposób wizualny, bez pisania kodu. Plik zapisany z QtDesigner ma format `.ui`.

### Ładowanie pliku .ui bez konwersji:
Zamiast konwertować plik `.ui`, można go załadować bezpośrednio w kodzie PyQt5.

```python
from PyQt5 import uic
from PyQt5.QtWidgets import QApplication, QMainWindow

class MyApp(QMainWindow):
    def __init__(self):
        super().__init__()
        uic.loadUi('design.ui', self)  # Ładowanie pliku .ui

if __name__ == '__main__':
    app = QApplication([])
    window = MyApp()
    window.show()
    app.exec_()
```
## 5. Układy (Layouts)

W PyQt5 można ustawiać układy (layouty), aby lepiej kontrolować rozmieszczenie widgetów w oknie. Poniżej przykład użycia `QVBoxLayout`.

```python
from PyQt5.QtWidgets import QVBoxLayout, QPushButton

class MyApp(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('Przykład z układem')

        layout = QVBoxLayout()

        button1 = QPushButton('Przycisk 1', self)
        button2 = QPushButton('Przycisk 2', self)

        layout.addWidget(button1)
        layout.addWidget(button2)

        self.setLayout(layout)
        self.show()
```
## Podsumowanie

- **QPushButton**: Tworzenie przycisków.
- **QLabel**: Tworzenie etykiet.
- **QLineEdit**: Pole tekstowe.
- **QCheckBox**: Pole wyboru.
- **QRadioButton**: Przycisk radiowy.
- **QComboBox**: Lista rozwijana.
- **Layouts**: Używanie układów do rozmieszczania widgetów.
- **QtDesigner**: Tworzenie interfejsu użytkownika wizualnie i integracja z PyQt5.
