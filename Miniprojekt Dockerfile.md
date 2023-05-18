# Docker Miniprojekt
### Maurin Inauen
# 1. Files erstellen

In dieses Dateien werden alle Dateien zur Organisation für den Docker und die Webseite abgelget.
Mit  ```mkdir``` werden die Dateien erstellt und mit ```cd``` in das jeweilige Verzeichnis gewechselt.

Code Terminal:
```
mkdir my-webserver

cd my-webserver

mkdir website

cd website
```
<p>&nbsp;</p>

# 2. Dateien für Webseite

Im ```index.html```  sind die Formatierungsinformationen abglelegt. Mit ```touch``` wird die Datei erstellt und mit ```nano``` wird der untenstehende Code eingefügt. Im ```style.css``` sind die Grafischen Informationen gespeichert, welche für das Design der Website wichtig sind.

Code Terminal: 
``` 
touch index.html
nano index.html

touch style.css
nano style.css
```

Code .HTML Datei:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <link rel="stylesheet" type="text/css" href="style.css">
    
    <title>Document Miniprojekt</title>
</head>
<body>

    <h1>Hello World</h1>
    <button>Click here! (nothing will happen...)</button>
    <a href="https://www.gbssg.ch/">Visit Us</a>

</body>
</html>
```

Code .CSS Datei:
```css
h1{
    font-family: Arial, Helvetica, sans-serif;
    font-weight: bolder;
}
```
<p>&nbsp;</p>

# 3. Docker File erstellen

Der Docker wird erstellt. In dieser separaten Datei wird das verwendete Apache-Image als Basis mit ```FROM``` angegeben und die Webseite wird mit ```COPY``` ins Image kopiert. Die ```EXPOSE```-Anweisung legt den Port fest, auf dem Ihre Anwendung läuft, wenn sie ausgeführt wird.

Code Terminal:
``` 
touch dockerfile
nano dockerfile
```

Code im dockerfile:
``` 
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
COPY style.css /usr/share/nginx/html/style.css
EXPOSE 8080
```
<p>&nbsp;</p>

# 4. Docker Image

Aus der HTML Datei und mit den Informationen vom Dockerfile wird ein Image erstellt. 

Code Terminal:
``` 
docker build -t my-webserver-image .
```

## 4.1 Kontrolle

Mit ```image ls``` kann man überprüfen ob das Image erstellt wurde.

Code Terminal:
``` 
docker image ls
```

Falls das Image erstellt wurde und vorhanden ist, wird die Ausgabe etwa so aussehen: 
``` 
vmadmin@lp-22-04:~/Desktop/Miniproket/my-webserver/website$ docker image ls
REPOSITORY               TAG        IMAGE ID       CREATED          SIZE
my-webserver-image       latest     a9989dcd6f18   14 seconds ago   142MB
```
<p>&nbsp;</p>

# 5. Container Starten

Aus dem Image kann nun ein Container gestartet werden. Das dockerfile wird ausgeführt und muss  laufen gelassen werden. Mit ```Crtl + C``` kann der Prozess abgebrochen werden und der Container wird gestoppt. Danach funktioniert auch die Webseite nicht mehr.

Code Terminal:
``` 
docker run -p 8080:80 my-webserver-image
```

## 5.1. Webseite erreichen

Das angezeigte HTML Dokument kann im Browser mit der untenstehenden Internetadresse aufgerufen werden.

Internetadresse Browser:
``` 
http://localhost:8080
```
