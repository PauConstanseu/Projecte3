# Introducció Documentació servidor DNS

Aquesta tasca consisteix a extreure la configuració d’un servidor DNS creat en una màquina virtual Ubuntu Server i preparar-la per ser publicada a GitHub com a prova de concepte per al client Digicore. L’objectiu és permetre que aquesta configuració es pugui replicar fàcilment en qualsevol altre servidor Linux simplement descarregant els fitxers i reiniciant el servei.

# Objectius Principals

- Assegurar la connectivitat entre la màquina virtual i la màquina física mitjançant una interfície Host-Only.
- Extreure els fitxers de configuració del servidor DNS utilitzant SCP.
- Organitzar aquesta configuració en un repositori GitHub dins la carpeta producte04/.
- Crear un README.md explicatiu i pujar els fitxers necessaris, incloent la carpeta zones/ amb els fitxers de zona.

# Fitxers a Publicar

- named.conf.options
- named.conf.local
- Fitxers de zona dins zones/
