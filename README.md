# M300
Modul 300

# LB2

## 10 Toolumgebung

**GitHub**
GitHub brauchen wir für die Versionsverwaltung. Bei GitHub kann man Dokumente zentral hochladen und runterladen.

**Vagrant**
Vagrant ist die Software, mit welcher wir unsere Virtuellen Maschinen automatisiert aufsetzen können.

**Virtual Box**
Virtual Box ist unsere Virtualisierungsumgebung. Dort werden unsere Virtuellen Maschinen aufgesetzt und gespeichert.


## Wissensstand

**Linux**
Die Virtuellen Maschienen, welche ich automatisiert erstellt habe, waren Linux Maschienen.
In diesem Modul brauchte ich aber nicht viele Linux Commands. Folgende Befehle musste ich im Vagrant File angeben, damit der gewünschte Service installiert wird:

Mit diesem Befehl werden die Services alle auf den neusten Stand gebracht.
    sudo apt-get update

So kann man gewünschte Pakete installieren.
    sudo apt-get -y install "PAKET"


**Virtualisierung**
Das Ziel dieses Modules ist es, alles automatisiert zu Virtualisieren. Für die Virtualisierung verwenden wir Virtual Box. Man kann auf einem physischen Server, viele virtuelle Server haben, was natürlich sehr viele Ressourcen spart. Ebenfalls ist es sehr platzsparend und kostengünstiger.
Eine weitere sehr verbreitete virtualisierungs Methode ist Cloud Computing. Unter Cloud Computing versteht man, wenn man ein Programm ausführt, welches sich nicht auf dem lokalen Gerät befindet. Von Cloud Computing gibt es verschiedene Arten:

*Infrastructure as a Service (IaaS)*
Es bietet dem Nutzer die typischen Komponenten einer Rechenzentrumsinfrastruktur wie Hardware, Rechenleistung, Speicherplatz oder Netzwerkressourcen aus der Cloud.

*Platform as a Service (PaaS)*
PaaS bezeichnet eine Cloudumgebung, die eine Plattform für die Entwicklung von Anwendungen im Internet bereitstellt.

*Software as a Service (SaaS)*
SaaS bezeichnet ein Distributionsmodell für Anwendungen über den Webbrowser. SaaS wird als Teilbereich des Cloud Computings verstanden, da angeforderte Applikationen nie direkt auf dem Gerät des Nutzers vorhanden sind.


**Vagrant**
Vagrant brauchte ich in diesem Modul, um meine Virtuellen Maschienen automatisiert aufzusetzen und den gewünschten Service mit zu installieren. Vagrant ist eine Software, welche in BASH läuft. So kann ein Vagrant File aussehen:

    Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
    config.vm.synced_folder ".", "/var/www/html"  
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"  
    end
    config.vm.provision "shell", inline: <<-SHELL
    # Packages vom lokalen Server holen
    # sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
    sudo apt-get update
    sudo apt-get -y install apache2 
    SHELL
    end


**Versionsverwaltung**
Die Versionsverwaltung braucht man, um zentral, Dokumente abzulegen und zu bearbeiten. Es ist sehr geeignet, wenn mehrere Benutzer auf einem Dokument oder Skript arbeiten müssen. Wenn man bei GitHub ein Dokument herunterlädt und bearbeitet, muss man beim wieder hochladen immer schreiben, was geändert wurde. So kann jede Veränderung nachgewiesen werden.
Hier sieht man die Help Page von Git:

    clone      Clone a repository into a new directory
    init       Create an empty Git repository or reinitialize an existing one

    add        Add file contents to the index
    mv         Move or rename a file, a directory, or a symlink
    reset      Reset current HEAD to the specified state
    rm         Remove files from the working tree and from the index

    bisect     Use binary search to find the commit that introduced a bug
    grep       Print lines matching a pattern
    log        Show commit logs
    show       Show various types of objects
    status     Show the working tree status

    branch     List, create, or delete branches
    checkout    Switch branches or restore working tree files
    commit     Record changes to the repository
    diff       Show changes between commits, commit and working tree, etc
    merge      Join two or more development histories together
    rebase     Reapply commits on top of another base tip
    tag        Create, list, delete or verify a tag object signed with GPG

    fetch      Download objects and refs from another repository
    pull       Fetch from and integrate with another repository or a local branch
    push       Update remote refs along with associated objects


**Mark Down**
Mark Down ist eine vereinfachte Auszeichnungssprache. Ein Ziel von Mark Down ist, dass schon die Ausgangsform ohne weitere Konvertierung leicht lesbar ist. Diese Dokumentation ist in der Mark Down Sprache geschrieben.


**Systemsicherheit**
Die Systemsicherheit kann man über verschiedene Methoden erhöhen:
- Firewall einrichten und nur die nötigen Ports öffnen
- Reverse-Proxy einrichten, so ist nur dieser vom Internet sichtbar und vom internen Netzwerk nichts.
- Benutzer- und Rechtvergabe ist eingerichtet, sodass nur bestimmte Personen Adminrechte haben.

Die Systemsicherheit ist ein sehr wichtiges Thema. In den grossen Firmen wird sehr viel Zeit und Geld in das investiert.


## Vagrant
Mit Vagrant setzen wir unsere VM automatisiert auf.

Als erste VM habe ich einen einfachen Webserver aufgesetzt. Wenn man eine VM über Vagrant aufsetzt muss man zuerst ein Vagrant File erstellen. In diesem werden diverse Sachen festgelegt, wie zum Beispiel RAM grösse, welches Betriebssystem, etc. Für diesen sieht mein Vagrant File wie folgt aus:

    Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
    config.vm.synced_folder ".", "/var/www/html"  
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"  
    end
    config.vm.provision "shell", inline: <<-SHELL
    # Packages vom lokalen Server holen
    # sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
    sudo apt-get update
    sudo apt-get -y install apache2
    SHELL
    end

Dieser Webserver war nachher über http://127.0.0.1 erreichbar.

Danach habe ich noch eine zweite VM über Vagrant aufgesetzt. Ich habe ein Web Server aufgesetzt und ein MySQL Server aufgesetzt. Für diesen hat mein Vagrant File wie folgt ausgesehen:

    Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
    config.vm.synced_folder ".", "/var/www/html"  
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"  
    end
    config.vm.provision "shell", inline: <<-SHELL
    # Packages vom lokalen Server holen
    # sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
    sudo apt-get update
    sudo apt-get -y install apache2 
    sudo apt-get -y install mysql-server
    sudo apt-get -y install php-mysql
    SHELL
    end

Danach kann man in irgendeiner Bash mit Hilfe von Vagrant eine VM aufsetzen.

    vagrant up

Mit diesem Befehl wird eine VM anhand des Vagrantfile erstellt.


**Vagrant Befehle**
Hier sind noch weitere Vagrant Befehle:

| Befehl                    | Beschreibung                                                      |
| ------------------------- | ----------------------------------------------------------------- | 
| `vagrant init`            | Initialisiert im aktuellen Verzeichnis eine Vagrant-Umgebung und erstellt, falls nicht vorhanden, ein Vagrantfile |
| `vagrant up`              |  Erzeugt und Konfiguriert eine neue Virtuelle Maschine, basierend auf dem Vagrantfile |
| `vagrant ssh`             | Baut eine SSH-Verbindung zur gewünschten VM auf                   |
| `vagrant status`          | Zeigt den aktuellen Status der VM an                              |
| `vagrant port`            | Zeigt die Weitergeleiteten Ports der VM an                        |
| `vagrant halt`            | Stoppt die laufende Virtuelle Maschine                            |
| `vagrant destroy`         | Stoppt die Virtuelle Maschine und zerstört sie.                   |


**Testing**
Wenn die VM richtig erstellt worden ist, sollte man jetzt unter de IP http://127.0.0.1:8080/ die Apache Standard Seite erreichen. Ich kam erfolgreich auf die Seite.


## Sicherheit
Ich habe einen Webserver und einen Datenbankserver aufgesetzt. Diese habe ich anhand eines bestehendem Vagrant File erstellt.
Für die Sicherheit habe ich zum einen eine Host Firewall konfiguriert. In dieser gebe ich definierte Ports an, welche offen sein sollten. Die anderen sind alle geschlossen. Dies aus dem Grund, da offene Ports, Eingänge für Hacker Angriffe sind.
Zusätzlich habe ich noch einen Reverse-Proxy aufgesetzt. Dieser leitet eine URL auf einen bestimmten Server weiter. Dadurch kann man zum Beispiel mit verschiedenen URL's auf einen einzigen Server zugreifen.

**Firewall Rules**
Danach habe ich auf dem Webserver den HTTP Port geöffnet

    sudo ufw allow 80/tcp

Auf dem Datenbankserver habe ich den MySQL Port für den Webserver geöffnet

    sudo ufw allow from 192.168.55.101 to any port 3306

Mit diesem Befehl habe ich dann kontrolliert, ob die Rules richtig erstellt wurden

    sudo ufw status


**Reverse-Proxy**
Für den Reverse-Proxy musste ich zwei Pakete installieren.

    sudo apt-get install lipapache2-mod-proxy-html
    sudo apt-get install libxml2-dev

Danach musste ich die Module in Apache aktivieren.

    sudo a2enmond proxy
    sudo a2enmond proxy_html
    sudo a2enmond proxy_http

Dann musste ich die Apache config (/etc/apache2/apache2.conf) anpassen.

    ServerName localhost

Die Weiterleitung wird in der Datei (etc/apache2/sites-enabled/001-reverseproxy.conf) angegeben.

    # Allgemeine Proxy Einstellungen
    ProxyRequests Off
    <Proxy *>
        Order deny,allow
        Allow from all
    </Proxy>

    # Weiterleitungen master
    ProxyPass /master http://master
    ProxyPassReverse /master http://master


## Abschluss
**Reflexion**
Ich fand es ein sehr spannendes Projekt. Ich habe viele neue Programme kennengelernt, mit welchen ich sicherlich auch in Zukunft arbeiten werde. Automatisierung ist ein sehr grosses Thema in der Informatik und daher fand ich es gut, dass wir die ersten Berührungen mit dem machen konnten. In dieser LB lief bei mir eigenltich alles gut. Also ich hatte keine grossen Probleme. Dies sicherlich auch, weil auf dem GitHub alles sehr gut beschrieben war. Das einzige Problem, was ich hatte, war dass ich nur einen Webserver haben konnte. Sobald ich einen zweiten aufgesetzt habe, sind die beiden Weberver nicht mehr errichbar gewesen.

**Wissenszuwachs**
Ich konnte sehr viel Wissen dazu gewinnen. Vorallem im Thema automatisierung. Mit dem Tool Vagrant ist innerhalb von einer Minute eine ganze virtuelle Maschiene erstellt, dies erleichtert das Ganze sehr.


# LB3

## K1

**GitHub**
GitHub brauchen wir für die Versionsverwaltung. Bei GitHub kann man Dokumente zentral hochladen und runterladen.

**Vagrant**
Vagrant ist die Software, mit welcher wir unsere Virtuellen Maschinen automatisiert aufsetzen können.

**Virtual Box**
Virtual Box ist unsere Virtualisierungsumgebung. Dort werden unsere Virtuellen Maschinen aufgesetzt und gespeichert.

**Visualstudio**
Visualstudio brache ich für meine Markdown Dokumentation. Der Vorteil von Visualstudio ist, dass ich meine Dokumentation direkt auf das GitHub "pushen" kann.


## K2

**Containersierung**
Was ist ein Container?

Ein Linux Container ist ein Satz an Prozessen, die vom Rest des Systems isoliert sind und auf einem eigenen Image ausgeführt werden, das alle benötigten Dateien zur Unterstützung der Prozesse bereitstellt. Durch Bereitstellung eines Image, das alle Abhängigkeiten einer Anwendung enthält, ist er portabel und bleibt konsistent und lässt sich so problemlos von der Entwicklung über die Prüfung und schließlich in die Produktion überführen.

Container vs. Virtualisierung
Container

Container teilen sich den gleichen Betriebssystem-Kernel und isolieren die Anwendungsprozesse vom Rest des Systems. 

Virtualisierung

Die Virtualisierung ermöglicht, dass mehrere Betriebssysteme gleichzeitig auf einem einzigen System laufen.

Was bedeutet das? Erst einmal: Mehrere Betriebssysteme auf einem Hypervisor laufen zu lassen – der Software, die Virtualisierung möglich macht – belastet das System mehr als die Verwendung von Containern. Wenn Sie nur über endliche Ressourcen mit endlichen Fähigkeiten verfügen, benötigen Sie kompakte Apps, die in großer Dichte eingesetzt werden können. Linux-Container arbeiten aus diesem einzelnen Betriebssystem heraus und nutzen es gemeinsam für alle Ihre Container. So bleiben Ihre Apps und Dienste leicht und können zügig parallel laufen.

**Docker**
Docker ist eine Produkt, für die Container Implementierung. Es verpackt den Service mit allen Abhängigkeiten in Container. Diese Container kann man dann individuell starten und stoppen.


## K3

**Besthenden Container kombinieren**
Zu Beginn habe ich einen Container erstellt, welcher einen Webserver beinhaltet.
Ich habe diesen wie folgt erstellt:

Als erstes muss man das Image erstellen.

    docker build -t webserver .

Kontrollieren, ob das Image erstellt worden ist kann man so

    docker images

Danach kann man den Container erstellen. Dafür muss man das Image angeben.

    docker run --rm -d --name webserver webserver

Mit folgendem Befehl kann man kontrollieren, ob der Container läuft.

    docker ps

Der Webserver war unter der URL:http://localhost:8080 erreichbar.


**Volumen einrichten**
So erstellt man ein Volumen.

    docker volume create "Name"

Um zu kontrollieren, ob das Volume richtig erstellt wurde, kann man folgenden Befehl eingeben und alle Volumen werden angezeigt.

    docker volume ls


**Docker Befehle**

| Befehl                               | Beschreibung                                           |
| -------------------------            | ------------------------------------------------------ | 
| `docker build -t "image" .`          | Erstellt ein Image                                     |
| `docker images`                      | Zeigt die Images                                       |
| `docker run --rm -d -- name "image"` | Erstellt einen Container anhand des Image              |
| `docker ps`                          | Zeigt alle Container                                   |
| `docker run --rm -d -P "container"`  | Vergibt den nächsten Port an den angegebenen Container |
| `docker network ls`                  | Listet die Netzwerke auf                               |
| `docker volume create "Name"`        | Erstellt ein Volumen                                   |
| `docker volume ls`                   | Zeigt alle Volumen an                                  |
| `docker search "name"`               | Sucht das gewünschte Image auf Docker Hub              |
| `docker pull "name"`                 | Lädt das gewünschte Image herunter                     |


## K4

**cAdvisor**
Als erste Service-Überwachung habe ich den cAdvisor implementiert.
Diesen habe ich wie folgt heruntergeladen:

    docker run -d --name cadvisor -v /:/rootfs:ro -v /var/run:/var/run:rw -v /sys:/sys:ro -v /var/lib/docker/:/var/lib/docker:ro -p 8080:8080 google/cadvisor:latest

Danach war er über http://localhost:8080 erreichbar.

**Standard-Logging**
Als erstes habe ich einen einfachen Test erstellt. Dieser gibt jede Sekunde ein "Tick" aus.

    docker run -d --name "Test" ubuntu bash -c 'while true; do echo "tick"; sleep 1; done;'

Das Log des laufenden Test kann so angezeigt werden.

    docker logs "Test"

Den Test kann man wie folgt wieder löschen.
    docker rm "Test"

**Syslog**
Zuerst habe ich auch hier einen Test laufen gelassen.

    docker run -d --log-driver=syslog ubuntu bash -c 'i=0; while true; do i=$((i+1)); echo "docker $i"; sleep 1; done;'

Es wurde alles im Syslog(/var/log/syslog) geloggt.

    tail -f /var/log/syslog


## K5

**Vergleich Vorwissen - Wissenszuwachs**
Ich habe im meinem Geschäft schon sehr viel von Container gehört, hatte aber nicht gross eine Ahnung wie das ganze funktioniert. In diesem Modul habe ich einen sehr grossen Einblich in das Thema bekommen. Ich denke ich habe die einfachen Grundlagen von Containern verstanden.

**Reflexion**
Wie schon oben erwähnt konnte ich sehr viel über das Thema Containern mitnehmen. Da Container ein sehr wichtiges Thema ist, was in der Zukunft noch eine viel grössere Rolle spielen wird, finde ich es gut, dass ich jetzt schon einiges darüber weiss. Die LB3 war sehr gut aufgebaut, sodass man viel mitnehmen konnte.


## K6

**Kubernetes**
Zuerst musste ich einen Namespace erstellen

    kubectl create namespace jan

Danach habe ich denn Service erstellt
    
    kubectl run apache --image=httpd --restart=Never --namespace jan

Anschliessend habe ich die YAML Datei mit dem Ergebniss erzeugt

    kubectl get service apache -o yaml --namespace jan

Zusätzlich musste ich noch den richitgen Port öffnen

    kubectl expose pod/apache --type="LoadBalancer" --port 80 --namespace jan

Schlussendlich konnte man kontrollieren, ob der Service auch erstellt wurde

    kubectl get service apache -o yaml --namespace jan
