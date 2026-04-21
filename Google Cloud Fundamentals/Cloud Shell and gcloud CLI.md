
Google Cloud Resource Management via Terminal, basic uses of gcloud cli.

---
### Environment Configuration

The `gcloud` tool stores properties that determine the default behavior of commands.

List the active account name and project ID:

```bash
gcloud auth list
gcloud config list project
```


Setting the default projects region and zone:

```bash
gcloud config set compute/region europe-west1
gcloud config set compute/zone europe-west1-b
```

```bash
# To view the project region and zone setting
gcloud config get-value compute/region
gcloud config get-value compute/zone
```


**Environment Variables**:
Przechowywanie ID projektu i strefy w zmiennych powłoki dla automatyzacji skryptów.
```bash
export PROJECT_ID=$(gcloud config get-value project)
export ZONE=$(gcloud config get-value compute/zone)
echo -e "PROJECT_ID: $PROJECT_ID\nZONE: $ZONE"
```

---

### Compute Instances
Zarządzanie instancjami maszyn wirtualnych (VM).

**Create VM**:
Tworzenie instancji o określonym typie maszyny i strefie.
```bash
gcloud compute instances create gcelab2 --machine-type e2-medium --zone $ZONE
```

**SSH Connection**:
Zautomatyzowane połączenie SSH z generowaniem kluczy.
```bash
gcloud compute ssh gcelab2 --zone $ZONE  # Połączenie i autoryzacja [cite: 38, 42]
# Przykład po zalogowaniu:
sudo apt update && sudo apt install -y nginx
```

---

### Networking & Firewall
Zastosowanie tagów sieciowych do kontroli ruchu przez firewall.

**Apply Tags**:
```bash
gcloud compute instances add-tags gcelab2 --tags http-server,https-server
# Nadanie tagów
```
**Firewall Rules**:
Zezwolenie na ruch przychodzący (ingress) na porcie 80 dla instancji z tagiem `http-server`.

```bash
gcloud compute firewall-rules create default-allow-http \
        --direction=INGRESS --priority=1000 --network=default \
        --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 \
        --target-tags=http-server  # Utworzenie reguły [cite: 62]
```

**Verification**:
Testowanie dostępności serwera nginx przez zewnętrzny IP.
```bash
curl http://$(gcloud compute instances list --filter=name:gcelab2 --format='value(EXTERNAL_IP)')
```


---

### Filtering & Logging
Wyciąganie precyzyjnych informacji z dużej ilości danych.

**Filtering**:
Użycie flagi `--filter` do wyszukiwania zasobów.
```bash
gcloud compute instances list --filter="name=('gcelab2')"  # Filtrowanie po nazwie 
gcloud compute firewall-rules list --filter="NETWORK:'default' AND ALLOW:'icmp'" 
```

**Cloud Logging**:
Odczytywanie logów systemowych i audytowych.

```bash
gcloud logging logs list --filter="compute"              # Filtrowanie list logów 
gcloud logging read "resource.type=gce_instance" --limit 5  # Odczyt logów instancji
gcloud logging read "resource.type=gce_instance AND labels.instance_name='gcelab2'" --limit 5 #
```
 
---

### SDK Components
Zarządzanie komponentami CLI.

```bash
gcloud components list      # Wyświetlenie zainstalowanych narzędzi (np. bq, gsutil) [cite: 32]
gcloud components update    # Aktualizacja CLI do najnowszej wersji [cite: 34]
```