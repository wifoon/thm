# Cloud Shell & gcloud CLI: Resource Management

Zarządzanie zasobami Google Cloud z poziomu terminala. Notatka na podstawie labu **Getting Started with Cloud Shell and gcloud**.

---

### Environment Configuration
Narzędzie `gcloud` przechowuje właściwości (properties), które determinują domyślne zachowanie komend.

 **Identification**:
    ```bash
    gcloud auth list               # Listowanie aktywnych kont [cite: 4]
    gcloud config list project     # Sprawdzenie aktualnie ustawionego projektu [cite: 4]
    ```
* **Regions & Zones**:
    Ustawienie domyślnej lokalizacji geograficznej dla zasobów (zonal/regional).
    ```bash
    gcloud config set compute/region europe-west1      # Ustawienie regionu [cite: 6]
    gcloud config set compute/zone europe-west1-b       # Ustawienie strefy [cite: 7]
    ```
* **Environment Variables**:
    Przechowywanie ID projektu i strefy w zmiennych powłoki dla automatyzacji skryptów.
    ```bash
    export PROJECT_ID=$(gcloud config get-value project)       # Pobranie ID projektu [cite: 12]
    export ZONE=$(gcloud config get-value compute/zone)        # Pobranie strefy [cite: 12]
    echo -e "PROJECT_ID: $PROJECT_ID\nZONE: $ZONE"             # Weryfikacja zmiennych [cite: 13]
    ```

---

### Compute Instances
Zarządzanie instancjami maszyn wirtualnych (VM).

* **Create VM**:
    Tworzenie instancji o określonym typie maszyny i strefie.
    ```bash
    gcloud compute instances create gcelab2 --machine-type e2-medium --zone $ZONE  # Utworzenie VM [cite: 14]
    ```
* **SSH Connection**:
    Zautomatyzowane połączenie SSH z generowaniem kluczy.
    ```bash
    gcloud compute ssh gcelab2 --zone $ZONE  # Połączenie i autoryzacja [cite: 38, 42]
    # Przykład po zalogowaniu:
    sudo apt update && sudo apt install -y nginx  # Instalacja serwera WWW [cite: 52]
    ```

---

### Networking & Firewall
Zastosowanie tagów sieciowych do kontroli ruchu przez firewall.

* **Apply Tags**:
    Etykietowanie instancji w celu dopasowania reguł firewalla.
    ```bash
    gcloud compute instances add-tags gcelab2 --tags http-server,https-server  # Nadanie tagów [cite: 61]
    ```
* **Firewall Rules**:
    Zezwolenie na ruch przychodzący (ingress) na porcie 80 dla instancji z tagiem `http-server`.
    ```bash
    gcloud compute firewall-rules create default-allow-http \
        --direction=INGRESS --priority=1000 --network=default \
        --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 \
        --target-tags=http-server  # Utworzenie reguły [cite: 62]
    ```
* **Verification**:
    Testowanie dostępności serwera nginx przez zewnętrzny IP.
    ```bash
    curl http://$(gcloud compute instances list --filter=name:gcelab2 --format='value(EXTERNAL_IP)') # [cite: 65]
    ```

---

### Filtering & Logging
Wyciąganie precyzyjnych informacji z dużej ilości danych.

* **Filtering**:
    Użycie flagi `--filter` do wyszukiwania zasobów.
    ```bash
    gcloud compute instances list --filter="name=('gcelab2')"  # Filtrowanie po nazwie [cite: 35]
    gcloud compute firewall-rules list --filter="NETWORK:'default' AND ALLOW:'icmp'" # [cite: 37]
    ```
* **Cloud Logging**:
    Odczytywanie logów systemowych i audytowych.
    ```bash
    gcloud logging logs list --filter="compute"              # Filtrowanie list logów [cite: 67]
    gcloud logging read "resource.type=gce_instance" --limit 5  # Odczyt logów instancji [cite: 68]
    gcloud logging read "resource.type=gce_instance AND labels.instance_name='gcelab2'" --limit 5 # [cite: 75]
    ```

---

### SDK Components
Zarządzanie komponentami CLI.
```bash
gcloud components list      # Wyświetlenie zainstalowanych narzędzi (np. bq, gsutil) [cite: 32]
gcloud components update    # Aktualizacja CLI do najnowszej wersji [cite: 34]