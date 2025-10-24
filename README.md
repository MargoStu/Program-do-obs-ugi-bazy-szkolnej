# Program-do-obs-ugi-bazy-szkolnej
class Uczen:
    def __init__(self,imie, nazwisko, klasa):
        self.imie = imie
        self.nazwisko = nazwisko
        self.klasa = klasa

    def __str__(self):
        return f"Uczen: {self.imie} {self.nazwisko} ({self.klasa})"

class Nauczyciel:
    def __init__(self, imie, nazwisko, przedmiot, klasy):
        self.imie = imie
        self.nazwisko = nazwisko
        self.przedmiot = przedmiot
        self.klasy = klasy

    def __str__(self):
        return f"<Nauczyciel: {self.imie} {self.nazwisko} {self.przedmiot} {self.klasy}>"

class Wychowawca:
    def __init__(self, imie, nazwisko, klasa):
        self.imie = imie
        self.nazwisko = nazwisko
        self.klasa = klasa

    def __str__(self):
        return f"<Wychowawca: {self.imie} {self.nazwisko} {self.klasa}>"

uczniowie = [
    Uczen(imie="Jan", nazwisko="Matejko", klasa="1C")
]
nauczyciele = [
    Nauczyciel(imie="Teresa", nazwisko="Ścibor", przedmiot="Przyroda", klasy="1C")
]

wychowawcy = [
    Wychowawca(imie="Zbigniew",nazwisko="Boniek",klasa="1C")
]

def wczytaj_ucznia():
     imie = input("Podaj imie: ")
     nazwisko = input("Podaj nazwisko: ")
     klasa = input("Podaj klase: ")
     return Uczen(imie, nazwisko, klasa)

def wczytaj_nauczyciela():
    imie = input("Podaj imie: ")
    nazwisko = input("Podaj nazwisko: ")
    przedmiot = input("Podaj przedmiot: ")
    klasy = []
    print("Podaj klasy, które prowadzi nauczyciel (pusta linia kończy): ")
    while True:
        klasa = input(">")
        if klasa == "":
            break
        klasy.append(klasa)
    return Nauczyciel(imie, nazwisko, przedmiot, klasy)

def wczytaj_wychowawce():
    imie = input("Podaj imie: ")
    nazwisko = input("Podaj nazwisko: ")
    klasa = input("Podaj klase: ")
    return Wychowawca(imie, nazwisko, klasa)

while True:
    akcja = input("Co chcesz zrobić? [utwórz, zarządzaj, koniec]: ").lower()

    if akcja == "koniec":
        break

    elif akcja == "utwórz":
        print("utwórz: [klasa, uczeń, nauczyciel, wychowawca]")

        while True:
            akcja_utworz = input("\nCo chcesz zrobić? [klasa, uczeń, nauczyciel, wychowawca, koniec]: ")

            if akcja_utworz == "koniec":
                break

            elif akcja_utworz == "uczeń":
                uczniowie.append(wczytaj_ucznia())
            elif akcja_utworz == "nauczyciel":
                nauczyciele.append(wczytaj_nauczyciela())
            elif akcja_utworz == "wychowawca":
                wychowawcy.append(wczytaj_wychowawce())
            else:
                print("Nieznana komenda.")

    elif akcja == "zarządzaj":

        while True:
            akcja_zarzadzaj = input("\nCo chcesz zrobić? [klasa, uczeń, nauczyciel, wychowawca, koniec]")

            if akcja_zarzadzaj == "koniec":
                  break

            elif akcja_zarzadzaj == "klasa":
                klasa = input("Podaj nazwę klasy:")
                print(f"\nUcznownie klasy {klasa}: ")
                znaleziono = False
                for uczen in uczniowie:
                    if uczen.klasa == klasa:
                        print(f" {uczen.imie} {uczen.nazwisko}")
                        znaleziono = True
                if not znaleziono:
                    print("Brak uczniów w tej klasie.")

                print("\nWychowawca:")
                znaleziono = False
                for wychowawca in wychowawcy:
                    if wychowawca.klasa == klasa:
                        print(f" - {wychowawca.imie} {wychowawca.nazwisko}")
                        znaleziono = True
                if not znaleziono:
                    print("Brak wychowawcy dla tej klasy.")

            elif akcja_zarzadzaj == "uczeń":
                imie = input("Podaj imię ucznia: ")
                nazwisko = input("Podaj nazwisko ucznia: ")
                uczen = None
                for uczen in uczniowie:
                    if uczen.imie == imie and uczen.nazwisko == nazwisko:
                        break
                if uczen:
                    print(f"\nUczeń {uczen.imie} {uczen.nazwisko} ({uczen.klasa}) ma lekcje z:")
                    znaleziono = False
                    for nauczyciel in nauczyciele:
                        for klasa in nauczyciel.klasy:
                            if uczen.klasa == klasa:
                                print(f" - {nauczyciel.przedmiot} ({nauczyciel.imie} {nauczyciel.nazwisko})")
                                znaleziono = True
                    if not znaleziono:
                        print("Brak przypisanych nauczycieli")
                else:
                    print("Nie znaleziono ucznia.")

            elif akcja_zarzadzaj == "nauczyciel":
                imie = input("Podaj imię nauczyciela: ")
                nazwisko = input("Podaj nazwisko nauczyciela: ")
                nauczyciel = None
                for nauczyciel in nauczyciele:
                    if nauczyciel.imie == imie and nauczyciel.nazwisko == nazwisko:
                        break
                if nauczyciel:
                    print(f"{nauczyciel.imie} {nauczyciel.nazwisko} prowadzi klasy:")
                    if nauczyciel.klasy:
                        for klasa in nauczyciel.klasy:
                            print(f" {klasa}")
                    else:
                        print("Brak przypisanych klas")
                else:
                    print("Nie znaleziono nauczyciela")

            elif akcja_zarzadzaj == "wychowawca":
                imie = input("Podaj imię wychowawcy: ")
                nazwisko = input("Podaj nazwisko wychowawcy: ")
                wychowawca = None
                for wychowawca in wychowawcy:
                    if wychowawca.imie == imie and wychowawca.nazwisko == nazwisko:
                        break

                if wychowawca:
                    print(f"\nUczniowie klasy {wychowawca.klasa}:")
                    znaleziono = False
                    for uczen in uczniowie:
                        if uczen.klasa == wychowawca.klasa:
                            print(f" {uczen.imie} {uczen.nazwisko}")
                            znaleziono = True
                    if not znaleziono:
                        print("Brak uczniów w tej klasie")
                else:
                    print("Nie znaleziono wychowawcy")

            else:
                print("Nieprawdiłowa komenda")
