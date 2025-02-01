# Maskowanie i zgadywanie liter – Projekt ASM

## Autor
**[Twoje imię i nazwisko]**

## Opis projektu
Program napisany w asemblerze dla symulatora SMS32. Umożliwia:
- Wprowadzanie tekstu przez użytkownika
- Maskowanie wybranych liter gwiazdkami (`*`)
- Zgadywanie ukrytych liter

## Struktura programu

### 1. Wprowadzanie tekstu
Program pobiera znaki wpisywane przez użytkownika i zapisuje je w pamięci.

```assembly
WPROWADZANIE_TEKSTU:
IN 00
MOV [BL],AL
ADD BL,70
MOV [BL],AL
SUB BL,70
INC BL
CMP BL,56
JNZ WPROWADZANIE_TEKSTU
```

### 2. Wybór liter do ukrycia
Użytkownik wybiera numery liter, które mają być zamaskowane (`*`).

```assembly
UKRYWANIE_LITER:
IN 00
SUB AL,31
MOV [BL],AL
INC BL
CMP BL,63
JNZ UKRYWANIE_LITER
```

### 3. Maskowanie liter
Program zamienia wybrane litery na `*`.

```assembly
MASKOWANIE_LITER:
MOV AL,[60]
ADD AL,C0
MOV BL,2A
MOV [AL],BL
MOV AL,[61]
ADD AL,C0
MOV [AL],BL
MOV AL,[62]
ADD AL,C0
MOV [AL],BL
```

### 4. Zgadywanie liter
Jeśli użytkownik poda poprawną literę, zostanie ona odsłonięta.

```assembly
ZGADYWANIE:
MOV CL,C0
MOV DL,50

SPRAWDZANIE_LITER:
MOV BL,[CL]
CMP BL,2A
JZ WPISYWANIE_ZGADNIECIA
INC DL
INC CL
CMP CL,C6
JNZ SPRAWDZANIE_LITER
JZ KONIEC
```

### 5. Odkrywanie poprawnie odgadniętych liter

```assembly
POPRAWNA_ODPOWIEDZ:
MOV AL,[DL]
MOV [CL],AL
INC DL
INC CL
CMP CL,C6
JNZ SPRAWDZANIE_LITER
```

## Podsumowanie
- Program działa w **symulatorze SMS32**
- **Język:** Asembler
- Można go rozwijać np. dodając licznik prób

## Jak uruchomić?
1. Pobierz **symulator SMS32**
2. Załaduj plik `projekt.asm`
3. Uruchom i testuj

