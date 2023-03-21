Uporaba načrta razlage (Explain Plan) v Oracleu je močno orodje, ki vam pomaga razumeti izbrani načrt izvajanja za določeno SQL poizvedbo s strani optimizatorja Oracle. Z analizo rezultatov načrta razlage lahko prepoznate morebitne ozke grla pri zmogljivosti in optimizirate svoje SQL poizvedbe. Tu so koraki za pravilno uporabo načrta razlage:

Ustvari načrt razlage:
Načrt razlage lahko ustvarite z eno od naslednjih metod:
Z uporabo ukaza EXPLAIN PLAN FOR:

```
EXPLAIN PLAN FOR
SELECT * FROM zaposleni WHERE id_oddelek = 10;
```
Z uporabo paketa DBMS_XPLAN s SQL_ID:

```
SELECT * FROM table(DBMS_XPLAN.DISPLAY_CURSOR('<SQL_ID>', NULL, 'TYPICAL'));
```
Z uporabo funkcije SQL*Plus AUTOTRACE:

```
SET AUTOTRACE ON EXPLAIN
SELECT * FROM zaposleni WHERE id_oddelek = 10;
```
Analiziraj rezultate načrta razlage:
Rezultati načrta razlage vsebujejo več stolpcev, kot so Operacija, Možnosti, Ime objekta, Stroški, Bajti in Kardinalnost. Poiščite naslednje kazalnike za prepoznavanje morebitnih ozkih grl:
Visoki stroški: Stroški predstavljajo ocenjeni čas za izvedbo določene operacije. Visokocenovne operacije lahko kažejo na težave z zmogljivostjo.

Popolno pregledovanje tabel: Popolno pregledovanje tabel je lahko drago, še posebej pri velikih tabelah. Razmislite o uporabi indeksov ali delitve za izboljšanje zmogljivosti poizvedb.

Gnezdeni ciklični spoji: Gnezdeni ciklični spoji so lahko neučinkoviti pri velikih naborih podatkov. Razmislite o uporabi hash spojev ali sortirno-združevalnih spojev.

Visoka kardinalnost: Kardinalnost je ocenjeno število vrstic, obdelanih v operaciji. Visoka kardinalnost lahko pomeni, da optimizator dela z netočnimi statistikami ali slabo zasnovanimi poizvedbami.

Neoptimalne poti dostopa: Če načrt razlage pokaže, da Oracle ne uporablja najučinkovitejše poti dostopa (npr. dostop z indeksom), boste morda morali posodobiti statistiko, ustvariti ali spremeniti indekse ali uporabiti namige za usmerjanje optimizatorja
