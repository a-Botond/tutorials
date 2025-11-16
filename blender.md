[< Főmenü](./readme.md)

Hasznos blender tippek 3D játék készítéséhez
============



Kör alakú (zárt) kijelölésnél a körbezárt rész kijelölése
------------

> Szerkesztésnél érdemes "Edge" módba váltani (shortcut: 2) <br>
> A kijelölés egyszerűbb, ha az egyik élre való kattintást Alt billentyűvel végezzük. Elm. kijelöli az egész élt.

1. **Felső menüsor**: `Select` (Kijelölés)
2. **Navigálj ide**: `Select Loops` (Hurkok kijelölése)
3. **Kattints erre**: Select Loop `Inner-Region` (Belső hurok-régió kijelölése)
4. **Törlés**: `X` vagy `Delete`



X-Ray Mód
------------

Edit mode-ban szerkesztés/törlés esetén ha nem csak a látható részeket szeretnénk szerkeszteni vagy törölni, akkor az `Alt + Z` shortcut megnyomásával a kijelölés alatt lévő összes rész kijelölésre kerül



Lyukak betöltése (Fill)
------------

Több lehetőség is van, itt a bevált módszert mutatom írom le, amely egyszerre az összes lyukat betölti
<br>
Itt is **Edit Mode**-ban vagyunk

1. **Jelölj ki mindent** az `A` billentyűvel. (Igen, az egész modellt. A funkció így is megtalálja a lyukat).
2. Menj a **Felső menüsor**ba: `Mesh`
3. **Navigálj ide**: `Clean up` (Tisztítás)
4. **Válaszd ki**: `Fill Holes` (Lyukak kitöltése)
5. **Bal alsó sarok "Options" panel**. `Sides -> 1000` 



Fölösleges részek törlése
------------

> **Első lehetőség**: "Delete Loose" <br>
> Ez a parancs kifejezetten a "gazdátlan" geometria (pontok, élek) eltávolítására való. Ez a parancs azonnal megkeres és töröl minden olyan pontot, ami nincs élhez kötve, és minden olyan élt, ami nincs laphoz kötve. Általában ez megoldja a "lebegő pontok" problémáját.

1. Lépj **Edit Mode**-ba (Szerkesztő Mód).
2. Nyomj `A`-t, hogy mindent kijelölj (ez nem mindig szükséges, de biztosra megy).
3. Menj a felső menüsorba: `Mesh`
4. Navigálj ide: `Clean up` (Tisztítás)
5. Válaszd ki: `Delete Loose` (Gazdátlan elemek törlése)

> **Második lehetőség**: "Select Linked" + Invert (A leghatékonyabb) <br>
> Ez a módszer akkor a legjobb, ha nemcsak magányos pontok maradtak, hanem apró, különálló "szigetek" is (pár háromszögből álló darabkák), amik már nem kapcsolódnak a fő modeledhez.

1. Lépj **Edit Mode**-ba.
2. Győződj meg róla, hogy semmi nincs kijelölve (nyomj `Alt + A`-t).
3. Vidd az egeret a **fő, nagy modelled** fölé (az a rész, amit meg akarsz tartani).
4. Nyomd meg az `L` billentyűt (a "Select Linked" - Összefüggő kijelölése rövidítése).
5. A Blender kijelöli az egész összefüggő geometriát az egered alatt.
6. Most fordítsd meg a kijelölést: Nyomd meg a `Ctrl + I` billentyűkombinációt (az "Invert" rövidítése).
7. Most minden ki van jelölve, kivéve a fő modelledet. Ezek a lebegő pontok és az apró, levált "szigetek".
8. Nyomd meg az `X` billentyűt, és válaszd a `Vertices` (Pontok) opciót. (Fontos, hogy a Vertices-t válaszd, mert az törli a pontokkal együtt a rajtuk lévő éleket és lapokat is).



Közel lévő, de nem kapcsoló felületek összekapcsolása
------------
> Pl. vágás miatt nem kapcsolódtak össze, de nem látszik
1. **Edit Mode**-ban jelölj ki mindent (`A`).
2. Nyomd meg az `M` billentyűt (a "Merge" rövidítése).
3. Válaszd a `By Distance` (Távolság szerint) opciót.
4. A bal alsó sarokban megjelenő panelen állíthatsz egy pici értéket (pl. `0.001m`).



Exportálás .fbx textúrával együtt
------------
1. 
2. 
3. 
4. 


Bake nagy felbontású elemről low poly-ra
------------
1. 
2. 
3. 
4. 



Hibák megoldással
------------

 1. Nem látszik egy oldal:

      * `Viewport Overlays` menüben a `Face Orientation`t be kell kapcsolni. 
      * A piros oldalak ki vannak fordítva. Legtöbb megjelenítő csak az objektumot külső oldalát rendereli, így átlászó lesz az kifordult oldal.
      * **Megoldás**: **`Edit Mode > Mesh > Normals > Flip Normals`**

 2. Nem látszik a face Orientation színe:

      * **Megoldás**: `Edit(fenti menüszalag) > Preferences > Themes > 3D Viewport`: Face orientation Back, Face Orientation Front színt beállítani (opacity-t is.)

 3. Export után nincs ott/átlátszó a fillelt Face:

      * 
        > Amikor a Fill Holes (Lyukak kitöltése) paranccsal betömöd a lyukat, az gyakran egyetlen óriási, több száz pontból álló lapot hoz létre. Ezt a Blender N-gon-nak nevezi.<br>
        > **A Blender kezeli**: A Blender modern szoftver, meg tudja jeleníteni ezeket az N-gonokat. Számára ez a felület "kék" (kifelé néző) és tömör.<br>
        > **Más programok nem**: A legtöbb program (mint a Windows 3D Nézegető, játékmotorok, más régi szoftverek) kizárólag háromszögekkel (tris) vagy négyszögekkel (quads) tud dolgozni.<br>
        > **A hiba pillanata**: Amikor megnyitod az .obj fájlt a 3D Nézegetőben, az megpróbálja saját maga, valós időben felbontani (szabdalni) a te óriási N-gonodat háromszögekre.

      * **Megoldás**: Háromszögelés (Triangulation) exportálás előtt
      1. `Select > Select All by Trait > Faces by Sides`
      2. A bal alsó panelen állítsd a "`Type`"-ot "`Greater Than`"-re (Nagyobb mint), és a "Vertices"-t (Pontok) `4-re (vagy nagyobbra)`. Ez kijelöli az összes N-gonodat.
      3. Jelöld ki a hibás N-gon lapo(ka)t (vagy biztonság kedvéért az egész modellt az `A` billentyűvel).
      4. Menj a felső menübe: `Face > Triangulate Faces (Ctrl + T)`
