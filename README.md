# rmf_raport


# RMF-DEMOS
Repozytorium **rmf_demos** zawiera gotowe mapy lokacji oraz zadania, które może wykonywać flota robotów. Aby uruchomić przykładową mapę w narzędziach **rviz2** oraz **gazebo**, należy skorzystać z polecenia:
```
ros2 launch rmf_demos_gz_classic hotel.launch.xml 
```
![](https://github.com/macnack/rmf_raport/blob/main/resources/hotel_world.png)


# RMF-TASK
Biblioteka **rmf_task** zapewnia narzędzia i interfejsy do definiowania i zarządzania sekwencjami zadań dla robotów. Obejmuje między innymi:
- `rmf_task::Task` - interfejs zawierający informacje dotyczące zadania/sekwencji zadań/modelu/akcji
- `rmf_task::TaskPlanner` - interfejs odpowiedzialny za optymalne przydzielenie zadań pomiędzy robotami

Obecnie dostępne są następujące typy zadań:
- Bundle
- DropOff
- GoToPlace
- PerformAction
- PickUp
- Placeholder
- WaitFor

W bibliotece **rmf_demos** mamy dostęp do gotowych sekwencji zadań, które można uruchomić poprzez wykonanie polecenia w terminalu:
```
ros2 run rmf_demos_tasks dispatch_patrol -p coe lounge -n 3 --use_sim_time
```
![](https://github.com/macnack/rmf_raport/blob/main/resources/loop_request.gif)

Przykładowe ciało requestu w formacie JSON może wyglądać następująco:
```
{
  "type": "robot_task_request",
  "robot": "tinyRobot1",
  "fleet": "tinyRobot",
  "request": {
    "category": "patrol",
    "description": {
      "places": ["pantry", "lounge"],
      "rounds": 2
    }
  }
}
```
- ```robot``` - nazwa robota
- ```fleet``` - nazwa floty
- ```category``` - typ zadania
- ```description``` - w tym przypadku lista punktów do odwiedzenia oraz ilość powtórzeń

#### RMF - Panel
Do wysyłania zadań można również wykorzystać aplikację webową:
![https://open-rmf.github.io/rmf-panel-js/](https://github.com/macnack/rmf_raport/blob/main/resources/rmf_panel.png)
Wysyłanie żądań odbywa się poprzez wybór dozwolonych zadań z listy oraz określenie dodatkowych atrybutów zadania, które w ciele requestu znajdują się w polu ```description```.

### Zarządzanie zadaniami
Do przypisywania zadań biblioteka **rmf_open** wykorzystuje dyspozytora (dispatcher), którego sposób działania przedstawiony jest poniżej:
![](https://github.com/macnack/rmf_raport/blob/main/resources/disp.png)
Po inicjalizacji dyspozytor decyduje, na podstawie opisu oraz kosztu (```BidProposals```), do której floty oraz którego robota przypisać zadanie.
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

x - nie testowane podczas pracy, brak zastosowanie
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

W celu konstruowania wielowarstwowej mapy nalezy nalozyc punkty ktore beda, laczyc pietra. Oznaczone jako m1, m2, m3
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

## Film demonstracyjny
[film demonstracyjny](https://drive.google.com/drive/folders/1bS8zznhJ821o93qN4pti-vwEe1Xr9ksD)
