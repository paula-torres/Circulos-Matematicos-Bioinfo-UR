# Circulos Matemáticos-Bioinformatica

## 1. El Caso:
La madrugada del viernes, el Dr. Elías Navarro, un reconocido investigador genético, fue hallado sin vida en el cuarto frío del Instituto de Ciencias Biológicas. La escena mostraba signos claros de forcejeo: equipos volcados, gradillas en el suelo y marcas defensivas en los brazos de la víctima.

Durante la autopsia, el médico forense encontró un elemento crucial: tejido epitelial (piel) debajo de las uñas de la víctima. El Dr. Navarro luchó contra su asesino y logró arrancar una pequeña muestra de ADN antes de morir.

La policía cerró el edificio e interrogó al personal. Se ha restringido la lista a tres sospechosos principales. Dado que la muestra de piel es minúscula y ha comenzado a degradarse por las condiciones del cuarto frío, el equipo forense secuenció la Región Hipervariable 1 (HVR1) del ADN mitocondrial, ideal para rastrear linajes e identificar individuos en casos extremos.

Tu Misión: Eres el bioinformático de la división de homicidios. Recibirás las secuencias digitales extraídas de la escena. Tu deber es filtrar los contaminantes, comparar las secuencias humanas e identificar el asesino.

**Misión: Determinar si alguno de los sospechosos coincide con la evidencia utilizando herramientas de de biología molecular y bioinformática!!**

## 2. Cadena de Custodia: Las Muestras
En este [archivo]() encontrarás las secuencias de ADN recuperadas. Conoce su procedencia antes de analizarlas:

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

## FASE 2: Alineamiento Múltiple

Una vez aisladas las secuencias puramente humanas, debes buscar Polimorfismos de Nucleótido Único (SNPs). Las diferencias de una sola letra (mutaciones) pueden exculpar a un sospechoso.

1. Vamos a entrar a [Benchling](https://www.benchling.com/) y vamos a crear una cuenta.

2. Seleccionamos `Create > New DNA/RNA Aligment`

3. Subimos nuestro archivo fasta y escogemos la secuencia de la evidencia como Template.

![Ben1](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/benchlin1.png)

5. Escogemos Clustal como programa, quitamos las secuencias que no son de humanos y corremos el alineamiento!!

![Ben3](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/benchlin3.png)

![Ben4](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/benchlin4.png)

7. Una vez organizadas nuestras secuencias le damos en  `export > FASTA `.

![Bn2](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/benchlin2.png)

## FASE 3: Análisis Filogenético (El Clado del Asesino)
El árbol filogenético agrupará las muestras por cercanía evolutiva y similitud directa.

1. Con nuestro alineamiento vamos a ir a [phylogeny](https://www.ebi.ac.uk/jdispatcher/phylogeny/simple_phylogeny)
2. Subimos nuestro archivo alineado y le damos click en submit.

![sub1](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/phylogeny1.png)

4. Esto nos va a generar un arhivo con los nombres de nuestras secuencias en paréntesis, ese es nuestro árbol!! Pero ¿Como lo vemos? Copiemos el texto y lo llevamos a [iTol](https://itol.embl.de/)

5. Seleccionamos la opción upload tree y en el cuadro te texto pegamos nuestro árbol.

![itol1](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/itol1.png)
![itol2](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/itol3.png)
3. Listo tenemos nuestro árbol!! ¿Qué podemos interpretar? Observemos qué sospechoso comparte la misma rama evolutiva con el ADN recuperado de las uñas de la víctima.

![itol3](https://github.com/paula-torres/Circulos-Matematicos-Bioinfo-UR/blob/main/files/itol2.png)

Veredicto: Según el árbol filogenético y el alineamiento múltiple, ¿quién asesinó al Dr. Elías Navarro?
