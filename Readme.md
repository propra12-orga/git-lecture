Git Lecture
===========
LATEX-Quellen für die Präsentation zur Einführung in GIT

Build
-----
Es sind folgende Abhängigkeiten erforderlich:

1. rvm
2. pygments
3. latexmk
4. evince

- Für Gentoo: `emerge pygments latexmk evince`
- Für Ubuntu: `apt-get install latexmk evince python-pygments` (siehe auch http://wiki.ubuntuusers.de/Pygments)

Folgender Inhalt muss in die Datei `~/.latexmkrc`:

    $pdflatex = 'pdflatex -shell-escape %O %S';
    $pdf_previewer = "start evince";
    $pdf_update_method = 0;

Danach rvm installieren:

    bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
    source ~/.bash_profile # oder ~/.profile
    rvm requirements
    #.
    #.
    #.
    #Additional Dependencies:
    ## For Ruby / Ruby HEAD (MRI, Rubinius, & REE), install the following:
    #  ruby|ruby-head: emerge libiconv readline zlib openssl curl git libyaml sqlite libxslt libtool gcc autoconf automake bison m4 # unter Ubuntu steht das ganze hier mit apt
    #.
    #.
    #.
    rvm get head
    rvm reload
    rvm install 1.9.3

Dann ins Verzeichnis wechseln und bundler ausführen:

    git clone http://github.com/ohcibi/git-lecture.git
    cd git-lecture
    # Warnung über .rvmrc-Datei mit y beantworten
    bundle install

Schließlich Dokument kompilieren:

    mkdir build # falls nicht vorhanden
    rake clean && rake


Readme.md bearbeiten
--------------------
Zur Arbeit an der Readme.md gibt es einen kleinen Rake-Task, der die Datei in HTML kompiliert, nach /tmp speichert und mit Opera öffnet sowie einen Guard, der die Readme.md auf Änderungen überwacht und den Rake-Task automatisch startet.

    rake readme # rake task manuell starten
    bundle exec guard # guard starten

Für die Arbeit mit VIM empfehlen sich folgende Plugins:

* https://github.com/tpope/vim-markdown (Syntax-Highlight)
* https://github.com/suan/vim-instant-markdown (Live während des Bearbeitens im Browser laden. Abhängigkeiten im Gemfile enthalten. Nodejs und npm muss manuell nachinstalliert werden (siehe Readme im Projekt))
