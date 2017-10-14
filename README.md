# Pitanje 1:
Nakon dodavanja reference na ClassLibrary1 projekt u soluciji, kopiraju nam se sljedeće datoteke u output direktorij:
- ClassLibrary1.dll (shared library ili dynamic-link library projekta ClassLibrary1) 
- ClassLibrary1.pdb (informacije debuggeru, nama nebitno)

Razlog njenog kopiranja u output direktorij jest CopyLocal property u IDE-u koji je automatski postavljen na True nakon
dodavanja reference. S obzirom da naša izvršna datoteka (KonzolnaAplikacija.exe) ovisi o ClassLibrary1.dll (poziva statičku
funkciju unutar classa MyConsole), ona mora biti prisutna na mjestu poznatom izvršnoj datoteci. Jedno od tih mjesta na kojima
izvršna datoteka traži referirane libraryje jest direktorij u kojem se trenutno nalazi. Izradom 'app.config' datoteke se može
dati informacija izvrsnoj datoteci gdje traziti referirane librarije.

Micanjem ClassLibrary1.dll datoteke i onda pokretanjem izvrsne KonzolnaAplikacija.exe datoteke izaziva se
System.IO.FileNotFoundException iznimka, jer izvrsna aplikacija ne moze pronaci library gdje se nalazi metoda
ClassLibrary1.MyConsole.PrintHelloWorld. Dakle, aplikacija se crash-a.

Da vam trebam poslati izgrađenu aplikaciju, poslat ću vam (iz bin/Release foldera nakon izrade Release builda):
- ClassLibrary1.dll
- KonzolnaAplikacija.exe

# Pitanje 2:
Izmjenom stringa statičke funkcije PrintHelloWorld i onda kompilacije i pokretanja KonzolnaAplikacija će uzrokovati
ponovnu izgradnju libraryja ClassLibrary1 koji se onda stavlja u output direktorij. Dakle, ispis je od novog stringa
radije nego staroga (nova verzija librarija je korištena). Razlog tomu je što dodavanjem reference na neki library
projekt unutar solucije uzrokuje da taj projekt ovisi o tom library projektu (on postaje njegov build dependency).

Da promijenimo to, u Solution Exploreru kliknemo desnim klikom na Solution, te odaberemo Properties -> Common Properties ->
Project Dependencies, te u Project ListBox-u odaberemo 'KonzolnaAplikacija' i uncheckamo/untickamo ClassLibrary1.

# Pitanje 3:
Brisanjem packagea NodaTime i izgradnjom projekta, NodeTime package se automatski ponovno skida iz repozitorija i dodaje u folder
packages. To je zahvaljujući 'packages.config' datoteci, koji u sebi sadrži informaciju o NodaTime packageu i potrebnoj verziji za
izgradnju projekta. Dalke, projekt se izgrađuje bez problema jer se package ponovno skinuo.

# Odgovorio na pitanja
Antonio Junaković
0036500097