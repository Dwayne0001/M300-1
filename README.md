# M300
Modul 300

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
Vagrant brauchte ich in diesem Mdoul, um meine Virtuellen Maschienen automatisiert aufzusetzen und den gewünschten Service mit zu installieren. Vagrant ist eine Software, welche in BASH läuft. So kann ein Vagrant File aussehen:

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

Als erstes muss man ein Vagrant File erstellen. In diesem werden diverse Sachen festgelegt, wie zum Beispiel RAM grösse, welches Betriebssystem, etc.
Ich habe ein Web Server aufgesetzt. Für diesen hat mein Vagrant File wie folgt ausgesehen:

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
