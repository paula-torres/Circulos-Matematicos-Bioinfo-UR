# Circulos Matemáticos-Bioinformatica

## 1. El Caso:
La madrugada del viernes, el Dr. Elías Navarro, un reconocido investigador genético, fue hallado sin vida en el cuarto frío del Instituto de Ciencias Biológicas. La escena mostraba signos claros de forcejeo: equipos volcados, gradillas en el suelo y marcas defensivas en los brazos de la víctima.

Durante la autopsia, el médico forense encontró un elemento crucial: tejido epitelial (piel) debajo de las uñas de la víctima. El Dr. Navarro luchó contra su asesino y logró arrancar una pequeña muestra de ADN antes de morir.

La policía cerró el edificio e interrogó al personal. Se ha restringido la lista a tres sospechosos principales. Dado que la muestra de piel es minúscula y ha comenzado a degradarse por las condiciones del cuarto frío, el equipo forense secuenció la Región Hipervariable 1 (HVR1) del ADN mitocondrial, ideal para rastrear linajes e identificar individuos en casos extremos.

Tu Misión: Eres el bioinformático de la división de homicidios. Recibirás las secuencias digitales extraídas de la escena. Tu deber es filtrar los contaminantes, comparar las secuencias humanas e identificar el asesino.

**Misión: Determinar si alguno de los sospechosos coincide con la evidencia utilizando herramientas de de biología molecular y bioinformática!!**

## 2. Cadena de Custodia: Las Muestras
En este [archivo](https://raw.githubusercontent.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/refs/heads/main/files/secuencias_finales.fasta) encontrarás las secuencias de ADN recuperadas. Conoce su procedencia antes de analizarlas:

## Muestras de Interés Forense (ADN Mitocondrial HVR1)

* **Evidencia 1:** Células de piel extraídas de la mano derecha de la víctima (bajo las uñas).

* **Evidencia 2:** Pelo negro encontrado junto al cuerpo de la víctima.

* **Evidencia 3:** Hisopado de una biopelícula en el marco de la puerta del cuarto frío, donde la humedad es alta.

* **Sospechoso 01:** Frotis bucal del investigador postdoctoral, a quien el Dr. Navarro le acababa de negar la coautoría en un artículo crucial.

* **Sospechoso 02:** Raíz de un folículo piloso de la administradora del instituto, quien estaba siendo investigada por la víctima por presunto desvío de fondos.

* **Sospechoso 03:** Células epiteliales de un vaso de agua usado por el técnico de laboratorio principal, la última persona en ver a la víctima con vida.

## ¿Que pasó con estas muestras antes de llegar a nosotros?

![Cadena](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/custodia.png)

## 3. Protocolo de Laboratorio Bioinformático
Para resolver el homicidio, debes procesar los datos con rigor científico.

# FASE 1: Filtrado de Contaminantes (BLAST)
El cuarto frío no es un ambiente estéril. Debes descubrir la naturaleza biológica de las muestras de control y descartarlas.

1. Abre la base de datos de genomas: [NCBI BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&PAGE_TYPE=BlastSearch&LINK_LOC=blasthome)

2. Copia y pega la secuencia de las muestras.

3. Asegúrate de seleccionar Standard databases (nr/nt).

4. Haz clic en BLAST.


![Blast](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/Screenshot%20from%202026-05-03%2020-48-50.png)

¿Como interpretamos los resultados? Vamos a ver datos de nombre de la especie a la que pertenece esa secuencia y que tanto se parece a las secuencias de la base de datos.  

![Blast2](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/Screenshot%20from%202026-05-03%2020-52-36.png)

Nota del analista: Si la secuencia pertenece a un microorganismo o un animal de compañía, descártala. El asesino es indudablemente humano.

Vamos a seleccionar solo las secuencias de humanos, para eso vamos a usar el comando `grep`

```
grep -A 1 "Evidencia_1" secuencia > secuencia_final.fasta
grep -A 1 "Sospechoso" secuencias.fasta >> secuencia_final.fasta
```

## FASE 2: Alineamiento Múltiple

Una vez aisladas las secuencias puramente humanas, debes buscar Polimorfismos de Nucleótido Único (SNPs). Las diferencias de una sola letra (mutaciones) pueden exculpar a un sospechoso.

1. Movamos nuestro archivo a un lugar donde podamos usar nuestras secuencias:

```
cp secuencia_final.fasta /mnt/c/Users/../Desktop
```

2. Ingresa a la herramienta de alineamiento MEGA y abre el archivo de nuestras secuencias.

![Mega](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/Captura%20de%20pantalla%202026-05-06%20120525.png)

3. Va a aparecer un recuadro donde nos va a preguntar que queremos hacer con nuestras secuencias, le vamos a dar click en Align.

![Mega2](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/Captura%20de%20pantalla%202026-05-06_mega2.png)

4. Posteriormente vamos a seleccionaer el brazo con musculo (es el software de alineamiento) y damos la opcion Align DNA.

![Mega3](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/Captura%20de%20pantalla%202026-05-06_mega3.png)

Va a empezar a alinear y ya tenemos nuestras secuencias organizadas!! 

## FASE 3: Análisis Filogenético (El Clado del Asesino)
El árbol filogenético agrupará las muestras por cercanía evolutiva y similitud directa.

1. Con nuestro alineamiento vamos a ir a la pestaña Data > Phylogenetic Analysis
   
![Flogenia1](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/Captura%20de%20pantalla%202026-05-06filogenia1.png)

2. Damos ok y seleccionamos Tree > Construct/Test Maximum Likelihood Tree

![Flogenia2](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/Captura%20de%20pantalla%202026-05-06filogenia2.png)

3. Listo tenemos nuestro árbol!! ¿Qué podemos interpretar? Observemos qué sospechoso comparte la misma rama evolutiva con el ADN recuperado de las uñas de la víctima.

![Flogenia3](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/Captura%20de%20pantalla%202026-05-06filogenia3.png)

Veredicto: Según el árbol filogenético y el alineamiento múltiple, ¿quién asesinó al Dr. Elías Navarro?


Veredicto: Según el árbol filogenético y el alineamiento múltiple, ¿quién asesinó al Dr. Elías Navarro?
