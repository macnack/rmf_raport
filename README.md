# rmf_raport



# Tworzenie wlasnej mapy

## Toolbar

![toolbar](https://github.com/macnack/rmf_raport/blob/main/resources/toolbar.png)

1. Wybor elementu
2. Move
3. Obroc
4. Dodac punkta
5. x
6. x
7. Dodawanie punktow referencyjnych dla map `fiducials`
8. Dodawanie sciezek 
9. Dodawnie scian
10. x
11. Dodawanie drzwi
12. Dodawanie modelu
13. Dodawanie podlogi
14. x
15. x
16. x

x - nie testowane podczas, brak zastosowanie
## Dodawanie wymiaru mapy

W celu zwymiarowania mapy nalezy dodac `measurement`, w ich definicji nadaje sie rzeczywiste miary ( odcinki zaznaczone kolorem fioletowym )
![measurement](https://github.com/macnack/rmf_raport/blob/main/resources/rozmiar.png)

## Dodanie podlogi 

Nalezy zdefiniowac obszar na ktorym zostanie wygenerowana podloga
![floor](https://github.com/macnack/rmf_raport/blob/main/resources/podloga.png)


## Dodawnie scian i punktow

Dodawanie scian i punktow:
![sciana](https://github.com/macnack/rmf_raport/blob/main/resources/sciana_punkt.png)

Po zaznaczeniu scian (niebieskie odcinki) zostaje tam wygenerowany ich model.
Puntky sluza za punkty informacyjne dla robotow, np. ladowarka, nazwa pomieszczenia

## Dodawanie sciezek

Sciezki sluza jako strefa ruchu dla robotow mobilny
![sciezki](https://github.com/macnack/rmf_raport/blob/main/resources/sciezki.png)

## Dodawanie punktow `fiducials`

W celu konstruowania wielowarstwowej mapy nalezy nalozyc punkty ktore beda, laczyc pietra 
![punkty](https://github.com/macnack/rmf_raport/blob/main/resources/punkty_laczace.png)

## Generowanie mapy

[generator mapy](https://github.com/open-rmf/rmf_demos/tree/main/rmf_demos_maps)
W celu wygenerowania wlasnej mapy plik `xml` nalezy umiescic w folderze `maps`, a nastepnie zbudowac za pomoca komend:

```
mkdir build
cd build
cmake ..
```

Za pomoca skonfigurowanego przez producenta `CMakeLists.txt` otrzymuje sie wygenerowane modele, sciezki, oraz plik z punktami i sciazkami typu `yaml`


## Plik uruchomieniowy

W celu uruchomienia mapy nalezy skonfigurowac [plik](https://github.com/macnack/rmf_raport/blob/main/map_home2.launch.xml) `launch`, ktory umieszcza sie w [folderze](https://github.com/open-rmf/rmf_demos/tree/main/rmf_demos_gz/launch).