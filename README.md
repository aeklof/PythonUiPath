# Installera python 3.6 för integrering med UiPath

## Installera python 3.6 via anaconda prompt
Börja med att öppna annaconda command prompt.

Kör följande kommando för att installera en virtuell miljö för python 3.6. Byt ut yourenvname till något bra namn t.ex. python36

```bash
conda create -n yourenvname python=3.6 anaconda

```

Aktivera miljön genom att köra kommandot

```bash
conda activate yourenvname

```
Notera att terminalen har bytt prefix från (base) till (yourenvname). Detta betyder att du nu kan installera paket till din nya virtuella miljö.

För att installera paket använd kommandot pip för att installera nödvändiga paket. t.ex: (OBS använd inte conda install för då kommer inte UiPath att känna igen dina importerade paket.)

```bash
pip install pandas
pip install numpy
pip install sklearn

```

## UiPath
### Installera Python activities
1. Starta ett nytt projekt
2. Klicka på Manage packages
3. Klicka på fliken Official och sök på Python
4. Klicka install och sedan save.

### Använd Python activities
Nu kan du hitta alla Python activities där du hittar alla andra activities.
För att importera ett Python script så tar du följande steg:

1. Dra in ett Python scope på arbetsytan.
2. Propertien Path ska sättas till den virtuella miljön som du skapade tidigare. För att hitta den så kan du öppna anaconda prompten och skriva:

```bash
conda info
```

Utifrån följande information kan du kopiera sökvägen "active env location" och klistra in i Path under Python scope properties i UiPath.

```bash
     active environment : testenv
    active env location : C:\Users\aeklof\Documents\anaconda64\envs\testenv
            shell level : 2
       user config file : C:\Users\aeklof\.condarc
 populated config files :
          conda version : 4.7.12
    conda-build version : 3.18.9
         python version : 3.7.4.final.0

```

3. Sedan måste ni välja property Target till x64 om ni kör 64-bit Python eller x86 om ni kör 32-bit Python. För att kolla vilken version av python ni kör så kan ni skriva följande i  anacondaterminalen:
```bash
Python
```


4. För propertien Version, välj Python_36 (Eftersom Python 3.6 installerades tidigare)

5. Dra in en ny aktivitet, Load Python Script och lägg det i Python scope.
6. Ge filsökvägen till den python-fil som ni vill använda. I properties klicka på Result och skapa en ny variabel (ctrl+k) och döp den till något passande.
7. Dra in en Invoke Python Method aktivitet till. I properties under fliken Input skriv in variabeln som skapades i förra steget i fältet Instance.
8. I fältet name, skriv funktionsnamnet till den funktion som ska anropas. (t.ex. "FunctionName").
9. Klicka på Result under Output och skapa en ny variabel (ctrl+k) och döp den till något passande.

10. Dra in en Get Python Object aktivitet, under properties och fyll i fältet Python object under Input med den variabel som skapades i steg 9.
11. Klicka på Result under Output och skapa en ny variabel(ctrl+k) och döp den till något passande. Här måste Propertien TypeArgument matcha den datatyp som Pythonfunktionen spottar ut. Oftast fungerar Object bra. 

# Det ska vara allt för att köra ett Python-script i UiPath :)
