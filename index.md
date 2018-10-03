# Spis treści

* * *

1. [CEL I ZAKRES PRACY](#cel-i-zakres-pracy)
2. [WSTĘP](#wstep)
3. [WPROWADZENIE DO NORMY STEP](#wprowadzanie-do-normy-step)
    1. [NORMA STEP](#norma-step)
    2. [JĘZYK EXPRESS ORAZ EXPRESS-G](#jezyk-express-oraz-express-g)
    3. [STEP-NC](#step-nc)
    4. [NORMA ISO 14649](#norma-iso-14649)
    5. [NORMA ISO 14649 – CZĘŚĆ 201](#norma-iso-14649-czesc-201)
4. [PROJEKTOWANIE ARCHITEKTURY SYSTEMU APLIKACJI](#projektowanie-architektury-systemu-aplikacji)
    1. [OMÓWIENIE STRUKTURY TYPU KLIENT - SERWER](#omownie-struktury-typu-klient-serwer)
    2. [OMÓWIENIE PROTOKOŁU KOMUNIKACJI POMIĘDZY PRZEGLĄDARKĄ A SERWEREM - POŁĄCZENIE HTTP](#omowienie-protokulu-komunikacji-pomiedzy-przegladarka-a-serwerem-polaczenie-http)
    3. [RODZAJE STRON INTERNETOWYCH](#rodzaje-stron-internetowych)
    4. [KOMUNIKACJA MIĘDZY APLIKACJAMI - API](#komunikacja-miedzy-aplikacjami-api)
    5. [ARCHITEKTURA API - REST](#architektura-api-rest)
    6. [PLANOWANIE API ZGODNIE Z ZASADAMI REST](#planowanie-api-zgodnie-z-zasadami-rest)
    7. [PROJEKTOWANIE API DLA SERWISU INTERNETOWEGO](#projektowanie-api-dla-serwisu-internetowego)
    8. [PROXY](#proxy)
    9. [BAZA DANYCH](#baza-danych)
5. IMPLEMENTACJA SERWISU INTERNETOWEGO
    1. OMÓWIENIE ŚRODOWISKA NODE.JS ORAZ FRAMEWORK'A EXPRESS.JS 
    2. OMÓWIENIE MENEDŻERA PAKIETÓW JS – NPM
    3. ZAPROJEKTOWANIE ARCHITEKTURY SERWISU 
    4. PLIK KONFIGURACYJNY
    5. MONGOOSE – BIBLIOTEKA DO ZARZĄDZANIE BAZĄ DANYCH M ONGO DB
    6. TWORZENIE SERWISÓW
    7. TWORZENIE KONTROLERÓW
    8. UWIERZYTELNIENIE UŻYTKOWNIKA
    9. MODUŁ GŁÓWNY APLIKACJI 
    10. URUCHOMIENIE APLIKACJI
6. IMPLEMENTACJA APLIKACJI PRZEGLĄDARKOWEJ 
    1. OMÓWIENIE FRAMEWORK'A A NGULAR 
    2. OMÓWIENIE WYKORZYSTANYCH NARZĘDZI FRONT - END'OWYCH
    3. KOMUNIKACJA Z SERWEREM
    4. PROCES UWIERZYTELNIANIA 
    5. PROJEKTOWANIE FORMULARZA "MACHINE TOOL SPECIFICATION"
    6. PROJEKTOWANIE FUNKCJONALNOŚCI DO TWORZENIA FORMULARZY 
    7. PROJEKTOWANIE PANELU GŁÓWNEGO STRONY
    8. UTWORZENIE MODUŁU GŁÓWNEGO
    9. PRZYGOTOWANIE APLIKACJI DO URUCHOMIENIA
    10. OGRANICZENIA
7. KONFIGUROWANIE SERWISU PROXY 
    1. OMÓWIENIE SERWISU N GINX
    2. KONFIGURACJA N GINX 
8. PRZYGOTOWANIE SYSTEMU APLIKACJI DO URUCHOMIENIA 
    1. DOCKER
    2. PLIK KONFIGURACYJNY DO BUDOWANIA OBRAZÓW D OCKER'OWYCH 
    3. AUTOMATYCZNE BUDOWANIE ORAZ UDOSTĘPNIANIE OBRAZÓW 
    4. COMPOSE – ZDEFINIOWANE PLIKU KONFIGURACYJNEGO
    5. ZARZĄDZANIE SERWISAMI 
9. TESTOWANIE APLIKACJI
    1. ZALOGOWANIE SIĘ DO APLIKACJI 
    2. UTWORZENIE NOWEGO FOLDERU GŁÓWNEGO 
    3. UTWORZENIE FORMULARZA "MACHINE TOOL SPECIFICATION"
    4. DODANIE NOWYCH REKORDÓW DO FORMULARZA
    5. GENEROWANIE PLIKU XML 
    6. TWORZENIE WŁASNEGO FORMULARZA 
    7. PODGLĄD ZAWARTOŚCI BAZY DANYCH 
10. STATYSTYKI ORAZ WYKORZYSTANE NARZĘDZIA 
11. PODSUMOWANIE 
12. DYSKUSJA 
13. SUMMARY
14. LITERATURA
15. SPIS ILUSTRACJI
16. SPIS TABEL 
17. ANEKS 

# <a name="cel-i-zakres-pracy"></a> Cel i zakres pracy

* * *

Celem niniejszej pracy dyplomowej jest utworzenie aplikacji internetowej, z możliwością
jej uruchomienia z dowolnej, najnowszej przeglądarki internetowej na komputerze osobistym,
która ma umożliwić użytkownikowi wprowadzenie oraz zapisywanie danych technicznych
obrabiarek zgodnie z normą ISO 14649-201 (opisy obrabiarek objęte tym schematem to frezarki,
centra obróbcze, tokarki i wielozadaniowe maszyny). Aplikacja ma udostępniać również
funkcjonalność do generowania pliku XML na podstawie wprowadzonych danych. Oprócz tego,
aplikacja ma umożliwiać tworzenia własnych, prostych formularzy. Aby aplikacja była łatwa w
obsłudze zostanie również zaimplementowana funkcjonalność do tworzenia katalogów oraz
podkatalogów w celu umożliwienia segregowania formularzy według upodobań użytkownika.
Aplikacja ma być łatwa do instalacji oraz intuicyjna. W tym celu należy wykonać następujące
kroki:
1. Sformułowanie koncepcji budowy systemu aplikacji
2. Wybór sposobu komunikacji pomiędzy poszczególnymi komponentami systemu
3. Wybór odpowiednich technologii oraz narzędzi
4. Implementacja poszczególnych komponentów systemu
5. Uruchomienie systemu aplikacji
6. Testowanie systemu


# <a name="wstep"></a> Wstęp

* * *

Nowoczesne zakłady produkcyjne są budowane na całym świecie, które zawierają sprzęt
oraz oprogramowanie od różnych producentów. Ogromne ilości informacji o produktach muszą
być przesyłane między różnymi urządzeniami i maszynami. Przez to, że każdy system posiada
własne formaty danych, te same informacje muszą być wprowadzane wielokrotnie, prowadząc do
nadmiarowości i błędów [1]. W celu rozwiązania opisanego problemu powstała Międzynarodowa
Organizacja Normalizacyjna (ISO), której celem jest ułatwienie międzynarodowej koordynacji i
unifikacji standardów przemysłowych.

Jedną z norm zdefiniowaną przez ISO jest norma oznaczona numerem 14649-201, będącą
częścią normy STEP oraz STEP-NC. Norma ta definiuje obiektową strukturę danych, która
jednoznacznie charakteryzuje dostępne obrabiarki (frezarki, centra obróbcze, tokarki i
wielozadaniowe maszyny). Dzięki takiemu standardowi dowolny producent obrabiarek może
przekazywać dane do dowolnego systemu CAD/CAM, a producenci systemów CAD/CAM mogą
wymieniać między sobą dane bez konieczności integracji z każdym z dostępnych systemów
osobno.

Niniejsza praca inżynierska ma na celu stworzenie aplikacji, za pomocą której
użytkownik będzie mógł wprowadzić, zapisać a następnie wyeksportować wprowadzone dane
techniczne obrabiarki do formatu XML. Wszystko to zgodnie z normą ISO 14649-201.


# <a name="wprowadzanie-do-normy-step"></a> Wprowadzenie do normy STEP

* * *

## <a name="norma-step"></a> Norma STEP

Nazwa STEP (Standard for the Exchange of Product Model Data) jest to powszechne
określenie normy ISO 10303. STEP zajmuje się danymi o produktach z projektowania
mechanicznego i elektrycznego, wymiarowaniem geometrycznym i tolerancją, analizą i
produkcją, a także dodatkowymi informacjami specyficznymi dla różnych branż, takich jak
motoryzacja, przemysł lotniczy, budownictwo, przemysł stoczniowy, ropa i gaz, przetwarzanie
roślinnych surowców i wiele inne. Zakres ten stale się powiększa, gdyż wydawane są nowe części
normy. Części te są nazywane ISO 10303-xxx, gdzie xxx jest numerem części, a każda jest
standardem samym w sobie, mimo że jest składnikiem większej całości i współzależna od innych
części [2]. Na rys. 3-1 został przedstawiony schemat ideowy normy STEP.

![Wymiana danych pomiędzy różnymi systemami](assets/images/wymiana-danych-pomiedzy-roznymi-systemami.png)
*rys. 3-1 Wymiana danych pomiędzy różnymi systemami [źródło własne]*

Podobnie jak inne normy ISO, STEP jest chroniony prawami autorskimi ISO i nie jest
swobodnie dostępny. Jednak schematy 10303 EXPRESS są udostępniane bezpłatnie, podobnie jak
zalecane praktyki dla wdrażających normę [3]


## <a name="jezyk-express-oraz-express-g"></a> Język EXPRESS oraz EXPRESS-G

EXPRESS to bogaty i dojrzały język służący do definiowania obiektowych schematów
danych. Jest on częścią standardu STEP (ISO 10303) i jest szeroko stosowany w modelowaniu
danych dla zastosowań przemysłowych na dużą skalę, w tym do produkcji, inżynierii, platform
wiertniczych, zakładów przetwórczych itp. Jest wykorzystywany wszędzie tam, gdzie
projektowanie jest wspomagane komputerowo (systemy CAD). Jest on używany do opisania i
konfiguracji trójwymiarowej geometrii części stałych oraz i zespołów tych części w różnego 
rodzaju maszynach, począwszy od samochodów, po samoloty, skończywszy na platformach
wiertniczych, statkach i elektrowniach. Jego celem jest uwolnienie danych CAD od zależności
zastrzeżonych systemów komputerowych i formatów, a tym samym umożliwienie wymiany
danych opisujących wytwarzane produkty między systemami podczas projektowania procesu
produkcyjnego [4].

Użyteczność tego języka sprawiła, że musiał sprostać wyzwaniom wykraczającym poza
pierwotne przewidywania. Oprócz kształtu i konfiguracji produktu, jego wymagań projektowych
oraz instrukcji obsługi, należało również opisać historię obsługi i użytkowania w firmie. W
przypadku dużego lub kosztownego produktu informacje o cyklu życia mogą być co najmniej tak
samo ważne jak opis jego fizycznej konfiguracji. Informacje mogą być potrzebne w czasie
rzeczywistym pomiędzy wieloma użytkownikami w środowisku sieciowym, a nie tylko
wymieniane okresowo, co było pierwotną intencją STEP.

EXPRESS jest językiem leksykalnym o charakterze obiektowym, jest podobny do
języków programowania takich jak Pascal, czy C. Na rys. 3-2 został przedstawiony przykładowy
zapis schematu „Family” w języku EXPRESS.

```
SCHEMA Family;

ENTITY Human
    ABSTRACT SUPERTYPE OF (ONEOF (Man, Woman));
    name: STRING;
    mother: OPTIONAL Woman;
    father: OPTIONAL Man;
END_ENTITY;

ENTITY Man
    SUBTYPE OF (Human);
END_ENTITY;

ENTITY Woman
    SUBTYPE of (Human);
END_ENTITY;

END_SCHEMA;
```
*rys. 3-2 Model schematu "Family" zapisany w języku EXPRESS*

Schemat „Family” zawiera encję („ENTITY”) o nazwie „Human”. Encja ta została
oznaczona jako abstrakcyjna („ASBSTRACT”). Powoduje to, że nie może być tworzona
samodzielnie, ale może być podtypem innej encji. W tym schemacie encja „Human” jest podtypem
encji „Woman” oraz „Man”. Każda encja „Human” lub jej podtyp zawiera pole: „name” oraz
opcjonalnie „mother” oraz „father”, które wskazują na inny obiekt („Man” lub „Woman”).

Instrukcja obsługi języka EXPRESS w ISO 10303-11 definiuje także graficzny
podzestaw języka leksykalnego o nazwie EXPRESS-G. Jest to standardowa notacja graficzna dla
modeli informacyjnych. Uważa się go powszechnie za przydatny dodatek do języka EXPRESS,
który służy do wyświetlania definicji encji i typów, relacji i liczności. Ta notacja graficzna
obsługuje podzbiór języka EXPRESS. Jedną z zalet używania EXPRESS-G nad EXPRESS jest
to, że struktura modelu danych może być przedstawiona w bardziej zrozumiały sposób, a wadą,
że nie można formalnie określić ograniczeń złożonych [5].

rys. 3-3 przedstawia schemat danych zapisany za pomocą języka EXPRESS-G. Definicje
typów danych i schematów na diagramie są oznaczone ramkami, które zawierają nazwę
definiowanego elementu. Relacje między elementami są oznaczone liniami łączącymi te pola.
Odmienne style linii dostarczają informacji na temat rodzaju definicji lub relacji.

![Model "Family" zapisany za pomocą języka EXPRESS-G wraz z objaśnieniem poszczególnych relacji](assets/images/model-family-express-g.png)
*rys. 3-3 Model "Family" zapisany za pomocą języka EXPRESS-G wraz z objaśnieniem poszczególnych relacji [ISO 10303-11]*


## <a name="step-nc"></a> STEP-NC

STEP-NC jest językiem sterowania obrabiarek, który rozszerza normę ISO 10303 o
modele obróbki, które są zawarte w ISO 14649. Dodaje również wymiary geometryczne i dane
tolerancji oraz model STEP PDM do integracji z większymi przedsiębiorstwami. Wynik tych
działań został znormalizowany i zapisany jako ISO 10303-238 (znany również jako AP238) [6].

Obrabiarki ewoluowały od prostych maszyn z kontrolerami, które nie posiadały pamięci,
napędzane przez perforowaną taśmę do dzisiejszych, wysoce automatyzowanych systemów
sterowanych numerycznie, znanych jako obrabiarki CNC. Możliwości obrabiarek zmieniły się
radykalnie, ale język programowania zasadniczo pozostał taki sam. Wprowadzanie danych do
systemu CNC za pomocą G-code’ów (opisanych przez normę ISO 6983, również znaną pod nazwą RS-274)
jest często specyficzne dla maszyny i ograniczone do poleceń ruchu osi. Przez to
obrabiarka nie posiada żadnych użytecznych informacji o produkcie, takich jak dane o wymiarach
geometrycznych półfabrykatu, tolerancjach, właściwościach materiału, ustawieniu urządzenia i
innych informacjach wytworzonych podczas projektowania i planowania technologii produkcji .
Wszystkie te informacje znikną podczas konwersji ścieżki narzędzia w G-Code, przez co przepływ
informacji staje się jednokierunkowy [7]. Uproszczony schemat przepływu danych został
przedstawiony na rys. 3-4.

![Sposób programowania obrabiarek CNC za pomocą G-code'ów](assets/images/programowanie-cnc-g-codami.png)
*rys. 3-4 Sposób programowania obrabiarek CNC za pomocą G-code'ów [źródło własne]*

STEP-NC został zaprojektowany w celu zastąpienia kodów G nowoczesnym protokołem
komunikacyjnym, który łączy dane procesowe sterowane komputerowo (CNC) z opisem produktu
obrabianej części. Program STEP-NC może wykorzystywać pełny zakres konstrukcji
geometrycznych ze standardu STEP do przekazywania ścieżek narzędzi niezależnych od
urządzenia CNC. Dostarcza również opis operacyjny CAM i geometrię STEP CAD do obrabiarki
CNC, dzięki czemu przedmioty obrabiane, uchwyty i kształty narzędzi skrawających mogą być
wizualizowane i analizowane w kontekście ścieżek narzędziowych. Dzięki takiej wizualizacji
możliwe jest pokazanie ścieżki narzędzia w kontekście maszyny i przedmiotu obrabianego,
symulacji na maszynie, w celu sprawdzenia, czy nie występują zakłócenia i inne niepożądane
zachowania, a dzięki wspólnemu protokołowi wymiany danych możliwe jest wysłanie informacji
zwrotnej z produkcji do projektu [8]. Uproszczony schemat przepływu danych pomiędzy
systemem CAD/CAM a obrabiarką CNC został przedstawiony na rys. 3-5.

![Sposób programowania obrabiarek CNC z wykorzystaniem STEP-NC](./assets/images/programowanie-cnc-g-norma.png)
*rys. 3-5 Sposób programowania obrabiarek CNC z wykorzystaniem STEP-NC [źródło własne]*


## <a name="norma-iso-14649"></a> Norma ISO 14649

ISO 14649 to model transferu danych pomiędzy systemami CAD/CAM i maszynami
CNC, który zastępuje normę ISO 6983 poprzez usunięcie wad precyzując procesy obróbki
wykorzystując koncepcję obiektową. CNC jest odpowiedzialny za tłumaczenie kroków roboczych
na ruch osi i pracę narzędzia. Główną zaletą ISO 14649 jest wykorzystanie istniejących modeli
danych z ISO 10303. Jako że ISO 14649 zapewnia kompleksowy model procesu produkcyjnego,
może być również wykorzystany jako podstawa dwu- i wielokierunkowej wymiany danych
między innymi systemami informatycznymi [9].

ISO 14649 reprezentuje zorientowane obiektowo, informacyjno-kontekstowe podejście
do programowania sterowanego numerycznego (NC), które zastępuje redukcję danych do prostych
instrukcji przełączania lub ruchów liniowych i kołowych. Ponieważ jest zorientowany na obiekty
i funkcje oraz opisuje operacje obróbki wykonywane na obrabianym przedmiocie, a nie ruchy osi
zależne od maszyny, będzie on działał na różnych obrabiarkach lub sterownikach [9].

Formularz informacji w ISO 14649 pozwala na znaczne ulepszenia w stosunku do
istniejących metod, ale w celu wsparcia jeszcze bardziej wydajnej produkcji, oprócz informacji o
produkcji potrzebny jest opis środowiska produkcyjnego. W związku z tym, ta część ISO 14649
jest pierwszym krokiem umożliwiającym opis obrabiarek jako zasobów produkcyjnych. Opis
umożliwia projektantom procesów klasyfikowanie ich potrzeb maszynowych w ramach planu
mikro procesowego (plik ISO 14649), określanego jako model wymagań. Model umożliwia także
opisanie istniejących obrabiarek jako zasobów do produkcji, określanych jako modele katalogowe
[9].

Ta część normy ISO 14649 ma na celu zapewnienie podstaw do planowania i symulacji
procesów, na przykład dla twórców kontrolerów i programistów obrabiarek do opisywania ich
produktów, a także do badań. Norma ta określa również elementy danych opisu maszyn
specyficzne dla obrabiarek, potrzebne jako dane procesowe dla produkcji i charakterystyk maszyn.
Opisy obrabiarek objęte tym schematem to frezarki, centra obróbcze, tokarki i wielozadaniowe
maszyny. Ta część ISO 14649 nie ma na celu zastąpienia istniejących standardów opisu
obrabiarek, ale obejmuje konkretne potrzeby opisu zasobów produkcyjnych dla potrzeb
produkcyjnych w technologiach opisanych w ISO 14649.


## <a name="norma-iso-14649-czesc-201"></a> Norma ISO 14649 – część 201

Część 201 normy ISO 14649 jest odpowiedzialna za określenie danych technicznych
obrabiarek wykorzystywanych w procesach skrawania. Norma ta składa się z:
* opisu modelów poszczególnych encji składających się na daną normę
* przedstawionych zależności poszczególnych encji w języku EXPRESS
* przedstawionych zależności poszczególnych encji w języku EXPRESS-G
* przykładów danych technicznych obrabiarek i danych dotyczących wymagań
* obrabiarek dla różnych zastosowań

Rdzeniem całego modelu owej normy jest encja „machine_tool”, która składa się z pola
„description” typu „text”. Jednostki takie jak „machine_tool_requirements” oraz
„machine_tool_specification” dziedziczą po jednostce „machine_tool”. Opisany powyżej
fragment normy został przedstawiony w sposób graficzny na rys. 3-6 za pomocą języka
EXPRESS-G, który obrazuje występujące relacje.

![Fragment normy ISO 14649-201 przedstawiający rdzeń schematu „machine_tool” za pomocą języka EXPRESS-G](./assets/images/fragment-normy-iso-14649-201-express-g.png)
*rys. 3-6 Fragment normy ISO 14649-201 przedstawiający rdzeń schematu „machine_tool” za pomocą języka EXPRESS-G [10]*

Cała norma składa się z pięćdziesięciu dziewięciu encji połączonych między sobą
odpowiednimi relacjami oraz z siedemnastu zdefiniowanych typów, z czego dwanaście jest typem
wyliczeniowym. Każda encja jest dokładnie opisana: zawiera zastosowanie danej encji wraz z
objaśnieniem każdego z pól. Na rys. 3-7 został przedstawiony fragment normy ISO 14649-201
objaśniający encję „machine_tool_specification” za pomocą języka EXPRESS wraz z opisem
poszczególnych pól.

Fragment normy ISO 14649-201 przedstawiający encję „machine_tool_specification” w języku EXPRESS wraz z opisem poszczególnych pól [10]

![Fragment normy ISO 14649-201 przedstawiający encję „machine_tool_specification” w języku EXPRESS wraz z opisem poszczególnych pól](./assets/images/fragment-normy-iso-14649-201-encja-machine-tool-specification-express-g.png)
*rys. 3-7 Fragment normy ISO 14649-201 przedstawiający encję „machine_tool_specification” w języku EXPRESS wraz z opisem poszczególnych pól [10]*

Zgodnie z wymaganiami postawionymi aplikacji, nie wszystkie encje zostały
zaimplementowane. Wynika to z tego, że niektóre dane są bardzo specyficzne i przeznaczone dla
bardzo wąskiej grupy przypadków. W tab. 3-1 zostały przedstawione, wraz z opisem, wszystkie
encje, które zostały zaimplementowane w napisanej aplikacji.

*tab. 3-1 Spis encji, które zostały zaimplementowane w napisanej aplikacji [10]*
// ToDo: Paste table content


# <a name="projektowanie-architektury-systemu-aplikacji"></a> Projektowanie architektury systemu aplikacji

* * *

Przed przystąpieniem do pisania aplikacji należy najpierw zaplanować architekturę
całego systemu, który zostanie utworzony. W związku tym, że aplikacja ma zostać utworzona dla
„sieci”, muszą zostać zaprojektowane co najmniej dwa komponenty: aplikacja kliencka, która
będzie wykorzystywana przez przeglądarkę oraz aplikacja działającej po stronie serwera (aplikacja
serwerowa [11]), która będzie obsługiwać żądania wysyłane przez klienta (przeglądarkę). Jest to
klasyczny przykład architektury typu klient-serwer [12]. Obecnie zaprojektowany system został
przedstawiony na rys. 4-1.

![Schemat zaprojektowanego systemu składającego się z dwóch komponentów: klienta (przeglądarki) oraz serwisu internetowego](./assets/images/schemat-zaprojektowanego-systemu-1.png)
*rys. 4-1 Schemat zaprojektowanego systemu składającego się z dwóch komponentów: klienta (przeglądarki) oraz serwisu internetowego [źródło własne]*

Aplikacja ma za zadanie zapisywać dane dostarczone przez użytkownika (przeglądarkę),
dlatego w tym celu będzie potrzebny system do zarządzania danymi (baza danych). Baza danych
to system, który służy do przechowywania informacji oraz umożliwia sprawne manipulowanie
nimi, dzięki czemu zarządzanie dużą ilością danych jest względnie łatwe oraz efektywne [13]. W
Internecie jest dostępnych mnóstwo darmowych systemów bazodanowych, które umożliwiają
wydajne manipulowanie danymi, w związku z tym nie ma potrzeby pisania własnej implementacji
[14]. W związku z powyższym, do zaprojektowanego wcześniej systemu zostanie dołączony
serwer bazodanowy. Aktualny schemat systemu został przedstawiony na rys. 4-2.


![Schemat zaprojektowanego systemu składającego się z trzech komponentów: klienta (przeglądarki), serwisu internetowego oraz serwisu bazy danych](./assets/images/schemat-zaprojektowanego-systemu-2.png)
*rys. 4-2 Schemat zaprojektowanego systemu składającego się z trzech komponentów: klienta (przeglądarki), serwisu internetowego oraz serwisu bazy danych [źródło własne]*

Projektowana aplikacja ma oferować klientowi (osobie korzystającej z oprogramowania)
bogatą paletę operacji oraz wysoką dynamikę. Aby sprostać tym wymaganiom strona internetowa
powinna być „aplikacją”, a więc idealnie sprawdzą się w tym przypadku aplikacje jednostronicowe - SPA. Dobrze napisana strona typu SPA nie wymaga udziału serwera do generowania podstron,
dlatego wystarczy tylko zwykły serwer plików, którego zadaniem będzie przechowywanie danych
niezbędnych do uruchomienia aplikacji przez klienta (przeglądarkę) z możliwością ich pobrania.
W związku z powyższym do zaprojektowanego systemu zostanie dołączony serwis
przechowywujący pliki źródłowe aplikacji klienckiej. Aktualnie zaprojektowany system został
przedstawiony na rys. 4-3.

![Zaprojektowany system składający się z czterech komponentów: klienta (przeglądarki), serwisu internetowego, serwisu bazy danych oraz serwisu przechowywującego pliki źródłowe aplikacji klienckiej](./assets/images/schemat-zaprojektowanego-systemu-3.png)
*rys. 4-3 Zaprojektowany system składający się z czterech komponentów: klienta (przeglądarki), serwisu internetowego, serwisu bazy danych oraz serwisu przechowywującego pliki źródłowe aplikacji klienckiej [źródło własne]*

Klient (przeglądarka), aby móc korzystać z systemu aplikacji, musi mieć dostęp do dwóch
komponentów: serwisu z plikami źródłowymi (w celu pobrania i uruchomienia aplikacji przez
przeglądarkę) oraz serwisu z logiką biznesową (serwis internetowy). W takim wypadku, system
musi udostępniać na „zewnątrz” dwa porty. Dlatego, że na danym komputerze, na jednym porcie,
może być uruchomiona tylko jedna aplikacja jednocześnie, nie ma możliwości udostępnienia
całego systemu pod jednym IP lub jedną domeną na jednym porcie. Stanowi to problem w
szczególności w sieciach firmowych, w których administratorzy sieci bardzo często blokują porty,
które nie są ustandaryzowane, przez co klient może mieć problem z nawiązaniem połączenia z
aplikacjami. Jeżeli serwis z logiką biznesową zostanie uruchomiony na standardowym porcie, np.:
porcie 80 (przeznaczonym dla połączeń http), to serwis z plikami źródłowymi aplikacji klienckiej
musi zostać uruchomiony na innym porcie, który może być blokowany przez administratora sieci,
w której aplikacja jest uruchomiona. W celu poradzenia sobie z tym problemem należy
wykorzystać serwer proxy. Zadaniem serwera proxy będzie przekierowywanie żądań na
odpowiednie aplikacje w zależności od dostarczonego URL’a. Dzięki takiemu zabiegowi jest
możliwość skomunikowania się z odpowiednim serwerem bez bezpośredniej interakcji z nim, a 
co za tym idzie ominięcie blokady portów. W związku z powyższym do zaprojektowanego
wcześniej systemu zostanie dołączony serwis proxy. Ostateczna faza zaprojektowanego systemu
została przedstawiona na rys. 4-4.

![Zaprojektowany system składający się z pięciu aplikacji: klienta (przeglądarki), serwisu internetowego, serwisu bazy danych, serwisu przechowywującego pliki źródłowe aplikacji klienckiej oraz serwisu proxy](./assets/images/schemat-zaprojektowanego-systemu-4.png)
*rys. 4-4 Zaprojektowany system składający się z pięciu aplikacji: klienta (przeglądarki), serwisu internetowego, serwisu bazy danych, serwisu przechowywującego pliki źródłowe aplikacji klienckiej oraz serwisu proxy [źródło własne]*


## <a name="omownie-struktury-typu-klient-serwer"></a> Omówienie struktury typu klient-serwer

Model klient-serwer jest to wzór architektury oprogramowania, który dzieli zadania
między dostawców zasobów i usług, zwanych serwerami oraz wyzwalaczami usług, nazywanymi
klientami. Często klienci i serwery komunikują się za pośrednictwem sieci komputerowej na
oddzielnym sprzęcie, ale zarówno klient, jak i serwer mogą znajdować się w tym samym systemie.
Host serwera uruchamia jeden lub więcej programów serwera, które udostępniają swoje zasoby
klientom. Klient nie udostępnia żadnych zasobów, ale żąda funkcji lub usługi serwera . Klienci
inicjują zatem sesje komunikacyjne z serwerami oczekującymi na przychodzące żądania [12].

Architektura klient-serwer stała się jednym z podstawowych modeli obliczeniowych w
sieci. Wiele typów aplikacji zostało napisanych przy użyciu modelu klient-serwer. Standardowe
funkcje sieciowe, takie jak wymiana poczty e-mail, dostęp do sieci i dostęp do bazy danych, są
oparte na modelu klient-serwer. Na przykład przeglądarka internetowa to program klienta na
komputerze użytkownika, który może uzyskać dostęp do informacji na dowolnym serwerze
WWW na świecie. Na rys. 4-5 został przedstawiony schemat sieci komputerowej, w której klienci
komunikują się z serwerem za pośrednictwem Internetu.


![Schemat sieci komputerowej klientów komunikujących się z serwerem za pośrednictwem Internetu w architekturze klient-serwer](./assets/images/schemat-klient-serwer.png)
*rys. 4-5 Schemat sieci komputerowej klientów komunikujących się z serwerem za pośrednictwem Internetu w architekturze klient-serwer [źródło własne]*

## <a name="omowienie-protokulu-komunikacji-pomiedzy-przegladarka-a-serwerem-polaczenie-http"></a> Omówienie protokołu komunikacji pomiędzy przeglądarką a serwerem - połączenie HTTP

Żądanie-odpowiedź to wzorzec wymiany komunikatów, w którym jeden komputer
wysyła komunikat żądania do systemu, który odbiera i przetwarza żądanie, ostatecznie zwracając
wiadomość. Jest to prosty, ale potężny wzorzec przesyłania wiadomości, który pozwala dwóm 
aplikacjom prowadzić dwukierunkową rozmowę ze sobą przez kanał komunikacyjny. Ten
wzorzec jest szczególnie powszechny w architekturach klient-serwer.

Dla przykładu, kiedy klient banku uzyskuje dostęp do usług bankowości internetowej za
pomocą przeglądarki internetowej, jako klient inicjuje żądanie na serwer internetowy banku. Dane
logowania klienta są przechowywane w bazie danych, więc serwer sieciowy uzyskuje dostęp do
serwera bazy danych jako klient. Serwer aplikacji interpretuje zwrócone dane z bazy danych
poprzez zastosowanie logiki biznesowej, po czym wreszcie serwer WWW zwraca wynik do
przeglądarki klienta, w celu wyświetlenia danych. Na każdym etapie tej sekwencji wymiany
komunikatów pomiędzy klientem a serwer komputer przetwarza żądanie i zwraca dane. Przepływ
danych w wyżej podanym przykładzie został zobrazowany na rys. 4-6.

![Schemat komunikacji typu żądanie-odpowiedź pomiędzy klientem, serwerem oraz bazą danych](./assets/images/komunikacja-zadanie-odpowiedz.png)
*rys. 4-6 Schemat komunikacji typu żądanie-odpowiedź pomiędzy klientem, serwerem oraz bazą danych [źródło własne]*

Dla uproszczenia wzorzec ten jest zwykle implementowany w sposób całkowicie
synchroniczny, tak samo dzieje się w przypadku wywołań usług internetowych za pośrednictwem
protokołu HTTP, który utrzymuje połączenie otwarte i czeka, aż odpowiedź zostanie dostarczona
lub zawiesza działanie, gdy upłynie limit maksymalnego czasu oczekiwania na odpowiedź. Jednak
komunikacja typu żądanie-odpowiedź może być również zaimplementowana asynchronicznie, a
odpowiedź jest zwracana w nieznanym czasie.

## <a name="rodzaje-stron-internetowych"></a> Rodzaje stron internetowych

Strona internetowa jest do dokument, który został utworzony dla „sieci”, najczęściej o
rozszerzeniu HTML. Oznacza to, że owy dokument może zostać „otworzony” za pomocą
przeglądarki internetowej, której zadaniem jest odpowiednie wyświetlenie jego zawartości,
zgodnie ze zdefiniowanymi przez programistę regułami, zawartymi w dokumencie. Dokument ten
jest najczęściej przechowywany na komputerze podłączonym do Internetu (serwerze), z którym
łączą się przeglądarki internetowe (najczęściej poprzez protokół http) w celu jego pobrania a
następnie wyświetlenia jego zawartości. Proces ten został przedstawiony na rys. 4-7

![Proces komunikacji z serwerem przez przeglądarkę internetową](./assets/images/komunikacja-serwer-przegladarka.png)
*rys. 4-7 Proces komunikacji z serwerem przez przeglądarkę internetową [źródło własne]*

Po wpisaniu nazwy domeny, w przeglądarce internetowej, przeglądarka wysyła żądanie
do serwera na którym znajdują się pliki witryny. Przeglądarka pobiera te pliki, zwykle dokumenty
HTML, i towarzyszące im obrazy lub filmy, po czym wyświetla je na ekranie. HTML i inne języki
(CSS, JavaScript) używane do wyświetlania danych przez przeglądarkę internetową są zwykle
określane jako technologie Front-End’owe [15].

### <a name="tradycyjna-strona-internetowa"></a> Tradycyjna strona internetowa – MPA

„Multiple Page Application” (MPA) jest to termin, który odnosi się do stron
internetowych tworzonych w sposób „tradycyjny” [16]. Każde żądanie, wyświetlenie nowych
danych lub wysłanie danych na serwer w celu ich przetworzenia lub zapisania, wiąże się z potrzebą
wygenerowania a następnie wyświetlenia całej strony od nowa, co wiąże się z względnie długim
czasem oczekiwania. Proces ten został przedstawiony na rys. 4-8.

![Proces wyświetlania kolejnych podstrony witryny internetowej](./assets/images/proces-wyswietlania-strony-internetowej.png)
*rys. 4-8 Proces wyświetlania kolejnych podstrony witryny internetowej [źródło własne]*

Ze względu na to, że logika generowania dokumentów HTML jest umiejscowiona na
serwerze, serwer ten oprócz docelowej logiki musi również mieć zaimplementowane
funkcjonalności umożliwiające generowanie dokumentów HTML, co wiąże się z zużyciem
dodatkowych zasobów serwera. Uproszczony proces przetwarzania żądania przez serwer w tego
typu stronach internetowych został przedstawiony na rys. 4-9.

![Uproszczony schemat przetwarzania żądania przez serwer w stronach internetowych typu MPA](schemat-przetwarzania-zadania.png)
*rys. 4-9 Uproszczony schemat przetwarzania żądania przez serwer w stronach internetowych typu MPA [źródło własne]*

### <a name="aplikacja-internetowa-spa"></a> Aplikacja internetowa - SPA

Termin „Single Page Application” (SPA) jest zwykle używany do opisywania aplikacji,
które zostały zbudowane dla „sieci”. Aplikacje te są dostępne za pośrednictwem przeglądarki
internetowej, podobnie jak „tradycyjne” witryny internetowe, ale oferują bardziej dynamiczne
interakcje przypominające natywne aplikacje mobilne i stacjonarne. Najbardziej zauważalną
różnicą między witryną tradycyjną, a SPA jest zmniejszona ilość pełnych przeładowań strony.
SPA mają większe wykorzystanie zapytań AJAX (Asynchronous JavaScript And XML), czyli
sposobu na komunikację z serwerem bez konieczności pełnego odświeżania strony w celu
pobrania danych oraz aktualizacji widoku w aplikacji [17]. rys. 4-10 przedstawia uproszczony
schemat komunikacji pomiędzy przeglądarką a serwerem, gdy dostarczona strona internetowa jest
aplikacją internetową.


![Sposób komunikacji pomiędzy SPA a serwerem](./assets/images/komunikacja-spa-serwer.png)
*rys. 4-10 Sposób komunikacji pomiędzy SPA a serwerem [źródło własne]*

Po pobraniu całej przesłanej aplikacji internetowej i uruchomieniu jej przez przeglądarkę
(kroki 1-5), aplikacja wysyła żądanie na serwer w celu pobrania odpowiednich danych. Gdy dane
zostaną już dostarczone, aplikacja wygeneruje odpowiednie podstrony (kroki 6-10). Jeżeli dane
ulegną zmianie, nie ma potrzeby pobierania całej aplikacji od nowa (tak jak ma to miejsce w
MPA), wystarczy, że zostanie ponownie zainicjowane żądanie pobrania danych z serwera (kroki
6-10).

Ze względu na to, że cała logika generowania podstron witryny została przeniesiona na
aplikację (przeglądarkę), nie ma potrzeby implementowania warstwy logiki odpowiedzialnej za
generowanie dokumentów HTML na serwerze. W związku z tym proces przetwarzania żądania
przez serwer przechowywujący dane zostanie znacznie uproszczony (rys. 4-11).

![Uproszczony schemat przetwarzania żądania przez serwer bez warstwy logiki odpowiedzialnej za generowanie dokumentów HTML](./assets/images/schemat-przetwarzania-zadania-w-spa.png)
*rys. 4-11 Uproszczony schemat przetwarzania żądania przez serwer bez warstwy logiki odpowiedzialnej za generowanie dokumentów HTML [źródło własne]*

Budowanie stron internetowych typu SPA stało się w ostatnim czasie bardzo popularne i
obecnie jest uważane za nowoczesną praktykę rozwojową. Jednak każde rozwiązanie posiada
wady, które zawsze należy uwzględnić podczas podejmowania decyzji na budowanie aplikacji
tego typu. Z powodu, że przeglądarka wykonuje większość operacji, takich jak na przykład
dynamiczne generowanie widoków, powoduje to, że w urządzeniach o małej mocy obliczeniowej,
wydajność takich aplikacji może stanowić poważny problem. Dodatkowo, takie strony są bardzo
ciężkie do analizy przez boty internetowe, przez co wyszukiwarki internetowe mogą niewłaściwie
interpretować treści znajdujące się na stronie [17].

Aplikacje typu SPA powinny być przede wszystkim wykorzystywane podczas tworzenia
zaawansowanych aplikacji, w których ważniejsze jest zapewnienie dużej ilości funkcji i logiki niż
statycznych stron z dużą ilością tekstu. Stąd SPA doskonale sprawdzą się w sytuacjach takich jak
aplikacje bankowe, panele administracyjne, zaawansowane kalkulatory i aplikacje przetwarzające
rozbudowane formularze HTML. Natomiast totalnie nie sprawdzą się na blogach, serwisach
informacyjnych i innych stronach z dużą ilością tekstu i artykułów [18].

Im więcej interaktywności ma miejsce po stronie klienta, tym więcej kodu JavaScript jest
potrzebne, aby te interaktywne elementy obsłużyć. Im więcej kodu jest napisane, tym ważniejsze
jest posiadanie czystej i dobrze zaprojektowanej bazy kodu, przez co programiści nieustanie
pracują nad tworzeniem i ulepszaniem narzędzi, dzięki którym tworzenie SPA staje się szybsze i
przyjemniejsze [17]. Istnieje wiele szkieletów aplikacji JavaScript o otwartym kodzie źródłowym,
które pomagają w budowaniu tego typu aplikacji, jakich jak np.: Angular, React, Vue.js, Backbone
[19].

## <a name="komunikacja-miedzy-aplikacjami-api"></a> Komunikacja między aplikacjami - API

Aby się komunikować, komputery muszą korzystać ze wspólnego języka i przestrzegać
reguł, aby zarówno klient, jak i serwer wiedzieli, czego się spodziewać. Język i zasady
komunikacji są zdefiniowane w protokole komunikacyjnym. Wszystkie protokoły klient-serwer
działają w warstwie aplikacji. Protokół warstwy aplikacji określa podstawowe wzorce dialogu.
Aby jeszcze bardziej sformalizować wymianę danych, serwer może zaimplementować interfejs
aplikacji (API). API jest warstwą abstrakcji do uzyskiwania dostępu do usługi. Ograniczając
komunikację do określonego formatu zawartości, ułatwia to przetwarzanie.

W programowaniu komputerowym, API (Application Programming Interface) jest
zbiorem podprogramów, definicji, protokołów i narzędzi do tworzenia oprogramowania. Jest to
zbiór jasno określonych metod komunikacji między różnymi komponentami oprogramowania.
Dobre API ułatwia tworzenie programów komputerowych poprzez dostarczanie wszystkich
elementów składowych, które następnie są zestawiane przez programistę. API może zostać
napisane dla systemu internetowego, systemu operacyjnego, systemu baz danych, sprzętu
komputerowego lub bibliotek oprogramowania. Na przykład jeśli firma programistyczna
zamierza utworzyć edytor tekstu działający w systemie Microsoft Windows, twórcy tego edytora
tekstu wykorzystają różne funkcje wbudowane w system Windows, zamiast próbować napisać te
funkcje od nowa. W tym kontekście Microsoft zapewnił API jako środek dostępu do usługi
okienkowania w systemie operacyjnym Windows, a twórcy tysięcy aplikacji działających w tym
systemie „skonsumowali” tę usługę za pośrednictwem interfejsu API. Deweloperzy nie musieli
pisać kodu, aby narysować pasek tytułu okna, ani nie musieli pisać funkcji do zmiany rozmiaru
okna, zamiast tego, funkcje te zostały odziedziczone przez każde okno utworzone za pomocą
interfejsu API znajdującego się w samym systemie Microsoft Windows [20].

API nie są ograniczone jedynie do systemu Windows, ani też nie są ograniczone do
systemu, który jest obecnie używany na urządzeniu. API, na przykład, może zostać stworzone na
serwerach www, które umożliwi dostęp do konkretnych informacji z witryny.

## <a name="architektura-api-rest"></a> Architektura API - REST

REST jest to akronim od słów REpresentational State Transfer. REST to styl
architektoniczny zapewniający standardy między systemami komputerowymi w sieci, w celu
ułatwienia systemom komunikowanie się między sobą [21]. Aby daną architekturę można było
nazwać architekturą REST’ową musi ona spełniać pięć następujących ograniczeń [22]:

* Architektura jest typu klient-serwer

W architekturze REST zawsze jest klient i serwer, gdzie komunikacja jest zawsze
inicjowana przez klienta. Klient i serwer są oddzielone od siebie jednolitym interfejsem, dzięki
czemu zarówno klient, jak i serwer rozwijają się niezależnie.

* System jest bezstanowy

Każde żądanie od dowolnego klienta zawiera wszystkie informacje niezbędne do obsługi
żądania, a stan sesji jest przechowywany w kliencie. Stan sesji może być przeniesiony przez serwer
do innej usługi, takiej jak baza danych, w celu utrzymania trwałego stanu przez pewien okres i
umożliwienia uwierzytelnienia. Klient rozpoczyna wysyłanie żądań, gdy jest gotowy do przejścia
do nowego stanu.

* Wykorzystywanie pamięci podręcznej

Klienci i pośrednicy mogą buforować odpowiedzi, odpowiedzi zatem muszą, pośrednio
lub bezpośrednio, określać się jako buforowane lub nie, aby uniemożliwić klientom ponowne
wykorzystanie nieaktualnych lub niewłaściwych danych w odpowiedzi na kolejne żądania. Dobrze
zarządzane buforowanie częściowo lub całkowicie eliminuje niektóre interakcje klient-serwer,
dodatkowo poprawiając skalowalność i wydajność.

* System jest systemem warstwowym

System warstwowy jest systemem, w którym komponenty są grupowane (warstwowane)
w układzie hierarchicznym tak, że niższe warstwy zapewniają funkcje i usługi, które obsługują
wyższe warstwy. Systemy o coraz większej złożoności i możliwościach można rozbudować,
dodając lub zmieniając warstwy, aby poprawić ogólne możliwości systemu.

* Jednolity interfejs

Interfejs jest jednolity dla wszystkich aplikacji. Oznacza to, że informacje przesyłane są
w ustandaryzowanej formie, a nie w zależności od potrzeb konkretnej aplikacji. Interfejs REST
został opracowany z myślą o wydajnym transferze danych o dużej ziarnistości, optymalizując go
pod kątem wspólnego przypadku w sieci, w wyniku czego interfejs nie jest optymalny dla innych
form interakcji architektonicznych.

## <a name="planowanie-api-zgodnie-z-zasadami-rest"></a> Planowanie API zgodnie z zasadami REST

API serwisu internetowego jest to interfejs, który składa się z co najmniej z jednego
„punktu końcowego” (URI), który jest ukierunkowany na system wiadomości typu żądanie-
odpowiedź. Dane zwykle są wyrażone w formacie JSON lub XML, który jest przesyłany za
pośrednictwem Internetu, najczęściej za pomocą HTTP (REST API może zostać również
zaimplementowane dla innych protokołów) [23].

Punkty końcowe są ważnymi aspektami interakcji z internetowymi API po stronie
serwera, ponieważ określają, gdzie znajdują się zasoby dostępne dla oprogramowania stron
trzecich (klientów). Dostęp odbywa się za pośrednictwem identyfikatora URI, do którego są
wysyłane żądania HTTP i od którego oczekuje się odpowiedzi. Punkty końcowe muszą być
statyczne, w przeciwnym razie nie można zagwarantować prawidłowego działania
oprogramowania, które z nimi współdziała. Jeśli lokalizacja zasobu ulegnie zmianie (a wraz z nim
punkt końcowy), wówczas uprzednio napisane oprogramowanie przestanie działać poprawnie,
ponieważ wymagany zasób nie będzie już dostępny pod danym identyfikatorem. tab. 4-1 pokazuje
najczęściej projektowane API z wykorzystaniem metody http zgodne z architekturą REST.

*tab. 4-1 Przykład najczęściej projektowanego API dla HTTP zgodnego z zasadami REST*
// ToDo: Add table with most popular API

## <a name="projektowanie-api-dla-serwisu-internetowego"></a> Projektowanie API dla serwisu internetowego

W zaprojektowanym systemie (opisanym powyżej) będzie następowała komunikacja
pomiędzy aplikacją kliencką oraz serwerem. W związku z tym należy zaprojektować sposób
komunikacji pomiędzy tymi aplikacjami. W tym celu zostało zaprojektowanego API, które
zostanie zaimplementowane przez serwis internetowy. Zaprojektowanie API zostało
przedstawione w tab. 4-2. Jako format danych został wybrany format JSON ze względu na jego
bardzo dużą popularność oraz łatwość implementacji.

*tab. 4-2 Tabela przedstawia zaprojektowane API dla serwisu internetowego*
// ToDo: Add table with designed API 

## <a name="proxy"></a> Proxy

W sieciach komputerowych, serwer proxy jest to serwer pośredniczący, który działa jako
pośrednik pomiędzy różnymi serwerami, przekazując żądania. Klient łączy się z serwerem proxy,
żądając usługi, takiej jak na przykład pobranie pliku, strony internetowej, wykonanie jakieś
operacji lub jakikolwiek inny zasób dostępny z innego serwera. Następnie serwer proxy pyta
serwer docelowy o zasób, po czym zwraca odpowiedź z powrotem do klienta [24].

Wyróżnia się dwa główne podziały serwera proxy ze względu na sposób przekazywania
zasobów: proxy otwarte oraz odwrócone (z ang. „reverse”). Proxy otwarte jest to proxy, do którego
każdy klient połączony z siecią ma dostęp do owego serwera, za pomocą którego może łączyć się
z dowolnym innym serwerem [24]. Na rys. 4-12 został przedstawiony graficzny zapis sposobu
działania otwartego serwera proxy.

![Zasada działania otwartego serwera proxy](./assets/images/otwarte-proxy.png)
*rys. 4-12 Zasada działania otwartego serwera proxy [źródło własne]*

Natomiast odwrotny serwer proxy to serwer, który wydaje się klientom, że jest
„zwykłym” serwerem, ponieważ odpowiedź z serwera proxy jest zwracana tak, jakby pochodziła
bezpośrednio z oryginalnego serwera, pozostawiając klienta bez znajomości serwerów
źródłowych [24]. Na rys. 4-13 został graficznie przedstawiony sposób działania przykładowego
odwróconego serwera proxy.

![Przykład działania odwróconego serwera proxy](./assets/images/odwrocone-proxy.png)
rys. 4-13 Przykład działania odwróconego serwera proxy [źródło własne]

## <a name="baza-danych"></a> Baza danych

Baza danych to abstrakcja systemu plików systemu operacyjnego, która ułatwia
programistom tworzenie aplikacji, które tworzą, odczytują, aktualizują i usuwają trwałe dane.
Bazy danych sprawiają, że zorganizowana pamięć masowa jest niezawodna i szybka [25]. Dwa
najpopularniejsze rodzaje baz danych to bazy relacyjne (SQL) oraz nierelacyjne (NoSQL) [26].

W relacyjnych bazach danych wszystkie dane są przechowywane w relacjach (tabelach),
a każda relacja składa się z wierszy i kolumn. Ważną cechą modelu relacyjnego jest wykorzystanie
kluczy. Są to specjalnie wyznaczone kolumny w relacji, służące do porządkowania danych lub
powiązania danych z innymi relacjami. Jednym z najważniejszych kluczy jest klucz podstawowy,
który służy do jednoznacznej identyfikacji każdego wiersza danych. Klucz obcy jest unikalną
referencją odnoszącą się do danych w jednej relacji z kluczem podstawowym innej relacji [27].

Relacyjne bazy danych wymagają zdefiniowania schematów przed dodaniem danych.
Oznacza to, że w celu przechowania danych, baza danych SQL musi z góry wiedzieć, co będzie
przechowywać. Jeśli baza danych jest duża, jest to bardzo powolny proces, który wymaga
znacznych przestojów. Jeśli często następuje zmiana danych, które przechowuje aplikacja, przestój
ten może być niewskazany. Nie ma również możliwości, za pomocą relacyjnej bazy danych,
efektywnego adresowania danych, które są całkowicie nieuporządkowane lub z góry nieznane.
Oprócz zdefiniowania struktury danych, model relacyjny ustanawia także zestaw zasad
wymuszających integralność danych, znanych jako ograniczenia integralności. Określa również
sposób manipulowania danymi. Ponadto model definiuje specjalną cechę zwaną normalizacją w
celu zapewnienia wydajnego przechowywania danych [27].

Bazy danych NoSQL zostały zbudowane w celu umożliwienia wstawiania danych bez
wstępnie zdefiniowanego schematu. Ułatwia to wprowadzanie istotnych zmian w aplikacji w
czasie rzeczywistym, bez martwienia się o przerwy w świadczeniu usług - co oznacza, że
tworzenie jest szybsze, integracja kodu jest bardziej niezawodna i potrzeba mniej czasu
administratora bazy danych. Programiści zwykle muszą dodać kod po stronie aplikacji, aby
wymusić kontrolę jakości danych, na przykład nakazując obecność określonych pól, typów danych
lub dopuszczalnych wartości. Bardziej wyrafinowane bazy danych NoSQL umożliwiają
stosowanie zasad sprawdzania poprawności w bazie danych, co pozwala użytkownikom
wymuszać zarządzanie danymi, przy jednoczesnym zachowaniu korzyści płynących ze stosowania
dynamicznego schematu [28].

W tab. 4-3 zostały wyszczególnione główne różnice pomiędzy opisywanymi bazami danych.

*tab. 4-3 Porównanie relacyjnych baz danych z bazami nierelacyjnymi [29]*
// ToDo: Add table with differences between SQL and NoSQL

W niniejszej pracy do zapisywania danych została wykorzystana nierelacyjna baza
danych – MongoDB. Baza ta idealnie sprawdzi się w zaprojektowanej aplikacji ze względu na
możliwość zapisu danych w formacie BSON oraz jej dynamiczny schemat. Dzięki temu, że
MongoDB jest popularne wśród programistów, istnieje mnóstwo bibliotek o otwartym kodzie
źródłowym, które znacząco ułatwią wykonywania operacji na niniejszej bazie.

# 5.
