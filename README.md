#!/bin/bash

# Obsługa opcji
if [[ "$1" == "--help" ]] || [[ "$1" == "-h" ]]; then
    # Wyświetlanie dostępnych opcji
    echo "Dostępne opcje:"
    echo "--help, -h: Wyświetla pomoc i dostępne opcje."
    echo "--logs, -l: Tworzy pliki log. Domyślnie 100 plików."
    echo "--date, -d: Wyświetla dzisiejszą datę."
    echo "--init: Klonuje całe repozytorium do katalogu w którym został uruchomiony oraz ustawia ścieżkę w zmiennej środowiskowej PATH."
    echo "--error, -e [liczba]: Tworzy pliki error. Domyślnie 100 plików, lub podana liczba."
    exit 0
elif [[ "$1" == "--logs" ]] || [[ "$1" == "-l" ]]; then
    if [[ "$2" =~ ^[0-9]+$ ]]; then
        # Tworzenie określonej liczby plików log
        liczba_plikow=$2
    else
        # Tworzenie 100 plików log
        liczba_plikow=100
    fi

    for ((i=1; i<=$liczba_plikow; i++)); do
        nazwa_pliku="log$i.txt"
        echo "Nazwa pliku: $nazwa_pliku" > "$nazwa_pliku"
        echo "Nazwa skryptu: skrypt.sh" >> "$nazwa_pliku"
        echo "Data utworzenia: $(date +%Y-%m-%d)" >> "$nazwa_pliku"
    done
elif [[ "$1" == "--date" ]] || [[ "$1" == "-d" ]]; then
    # Wyświetlanie dzisiejszej daty
    echo "Dzisiejsza data: $(date +%Y-%m-%d)"
elif [[ "$1" == "--init" ]]; then
    # Klonowanie repozytorium i ustawianie zmiennej PATH
    git clone https://github.com/axushd/cwiczenia.git
    export PATH=$PATH:$(pwd)/cwiczenia
elif [[ "$1" == "--error" ]] || [[ "$1" == "-e" ]]; then
    if [[ "$2" =~ ^[0-9]+$ ]]; then
        # Tworzenie określonej liczby plików error
        liczba_plikow=$2
    else
        # Tworzenie 100 plików error
        liczba_plikow=100
    fi

    for ((i=1; i<=$liczba_plikow; i++)); do
        nazwa_pliku="error$i.txt"
        echo "Nazwa pliku: $nazwa_pliku" > "$nazwa_pliku"
        echo "Nazwa skryptu: skrypt.sh" >> "$nazwa_pliku"
        echo "Data utworzenia: $(date +%Y-%m-%d)" >> "$nazwa_pliku"
    done
else
    # Obsługa nieznanej opcji
    echo "Błąd: Nieznana opcja."
    exit 1
fi
