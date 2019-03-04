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

