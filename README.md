# LCA-Script V1.0 

Scriptet vil i høj grad kunne bruges i de tidlige designfaser, alt afhængeligt af sit bygningsdelsinput (LCAbyg). 

Det er bygget op omkring åbenhed, og at det skal være overkommeligt at få sit resultat ud. Helt lav praktisk er det bygget op af følgende: 
-	Grasshopper
-	Rhino.Inside.Revit (bruges til at trække mængder ud af sin revit model)
-	LCAbyg: Bruges til at tilføje yderligere bygningsdele. På denne måde, kan man blive ved med at udvide sit biblioteket. Jeg har vedlagt den fil jeg har arbejdet med for at få scriptet til at fungere, så bare følg navngivningss ytemet i den, også skal resten nok løbe flydende (eller lav om i sorteringskoden i grasshopper)
-	Excel: Der er 2 excel ark hvoraf
o	1. LCAByg - Export - Resultatliste: Det ark du skal bruge til at importere dine nye LCAbyg filer 
o	2. Resultat ark: Et ark hvori grasshopper (hvis du har arket åbent)

## Dansk Guide
For at dette script skal fungerer er det vigtigt at have Rhino.Inside.Revit [RIR] til at køre, og scriptet skal åbnes igennem sit grasshopper vindue i Revit. Hvis man åbner scriptet igennem Rhino -> Grasshopper, vil alle RIR komponenter ikke vises. RIR er et gratis plugin til Revit.

Download link til Rhino.Inside.Revit:
https://www.rhino3d.com/inside/revit/1.0/ 

Udover RIR er det vigtigt at du har en aktiv Autodesk Revit Licens, Rhino Licens, samt et LCAbyg data udtræk med en sammenlignelig navngivning som uploadet. Du kan se eksempler på navngivningen i LCAbyg filen eller Excel udtrækket. Bygningsdelsnavngivningen tager udgangspunkt i BIM7AA typekodning. 

BIM7AA Typekodning: 
http://bim7aa.dk/ 

![Overordnet](https://github.com/LHFriis/LCA-Script/assets/166735139/575ff84f-4c8d-4f1f-b986-2f5e21b9047f)

#### 1. input data
Her defineres stien af dit LCAbyg excel udtræk. Denne sti skal være det uploadede Excel ark ’LCAByg – Export – Resultatliste. Denne Excel fil indeholder den struktur resten af scriptet er bygget op om. Hvor de forskellige bygningsdele osv. bliver sorteret. Det er derfor vigtigt, at denne fil bevarer sin struktur, samt navngivning af bygningsdele fra LCAbyg udtrækket. Hvis dette ændres, skal du huske at ændre til i sorteringen igennem scriptet. 
Her skal også defineres hvilken typologi der bygges, mængde gulvareal (m<sup>2</sup>), analyseperiode (I Danmark vil dette typisk være 50 år) og din ønskede usikkerhedsfaktor (se evt. nedenstående link for inspiration). 

Inspiration / reference til mulige usikkerhedsfaktorer på dit LCA projekt:
https://bygherrepartner.com/bygherrepartner-usikkerhedsmatrix/ 

![image](https://github.com/LHFriis/LCA-Script/assets/166735139/dd83dcde-f318-4363-b407-df8666085087)


#### 2. Beregning & Oversigt af resultat
GWP resultatet i enheden CO<sub>2</sub>-eq./m<sup>2</sup>/år. Resultatet kan ses både med og uden usikkerhedsfaktor. Derudover vises resultatet for bygningsdrift, bygningsdele (med og uden usikkerhedsfaktor), de forskellige bygningsdels kategorier fordelt op i Yder- & Indervægge, Tage, Dæk, Terrændæk, Fundamenter og Vinduer, Døre og Glasfacader.

![image](https://github.com/LHFriis/LCA-Script/assets/166735139/4853497b-2368-43b9-b544-91ae73087813)


#### 3. Standard værdier for teknisk data
Standardværdier for henholdsvis vand, afløb og ventilation og køl. Disse værdier ændrer sig alt afhængig af den valgte typologi. Standardværdierne er hentet fra: Social- og Bolig styrelsen - Oplæg til Defaultværdier for Installationer.
Hent standardværdierne for installationer, i bunden af denne side:
https://www.sbst.dk/byggeri/baeredygtigt-byggeri/national-strategi-for-baeredygtigt-byggeri/klimakrav-lca-i-bygningsreglementet 

![3](https://github.com/LHFriis/LCA-Script/assets/166735139/43443e11-046a-4553-94a1-34c1f54f7fe1)


#### 4. Tjek om de er overskydende elementer 
Test / overblik over om der er geometri fra Revit modellen som ikke er tildelt en bygningsdel. Det er delt op på: Yder- og Indervægge, Døre, Tage og Lofter, Dæk og Terrændæk. 

![4](https://github.com/LHFriis/LCA-Script/assets/166735139/70dfb7f5-d96e-448f-a2eb-540cd58dd254)


#### 5. Visning af model
Her kan man tænde / slukke for den udvalgte bygningsgeometri. Der kan tændes / slukkes for følgende grupper: Yder- & Indervægge, Tage & Lofter, Terrændæk, Fundamenter, Dæk og Vinduer, Døre og Glasfacader. 

![5](https://github.com/LHFriis/LCA-Script/assets/166735139/7295c708-dc36-4d2b-9207-fd6c57de49e8)


#### 6. Grafer
Ved hjælp af Grasshopper plugin ’LunchBox’ kan man ved at højreklikke på ”Chart” ud fra de forskellige grupperinger, få vist en graf af over de udvalgte elementer. Man kan få vist en graf for henholdsvis: Yder- & Indervægge, Tage & Lofter, Dæk, Terrændæk, Fundament, Vinduer & Døre og Glasfacader og en samlet for diverse bygningsdele i modellen.  

![6](https://github.com/LHFriis/LCA-Script/assets/166735139/0eb16839-e445-427b-a36b-cec14736c151)


#### 7. Print / forbindelse til excel 'Resultat Ark'
Ved hjælp af Grasshopper plugin ’LunchBox’ kan man få en live visning + grafer i Excel filen ved navn ’Resultat ark’. Det er dog vigtigt, at du har Excel filen åben, ellers vil dette ikke virke. Den første del af scriptet under punkt 7, udskriver bygningsdelsresultatet til hver sit Worksheet, og henter data herfra til at lave grafer i Excel arket. 2. del af scriptet under punkt 7, udskriver hovedbygningsdata som areal, samlet resultatet osv. til Excel arkets hovedside, på det 1. Worksheet. 

OBS! Vigtigt, at du husker at gemme, samt ikke har andre Excel filer åbne, da denne funktion vil overskrive din åbne Excel fil. 

Se evt. nedenstående video via. LinkedIn for live opdatering i Excel ark:
https://www.linkedin.com/posts/lassehfriis_vidensdeling-opensource-grasshopper-activity-7184452905637187584-iZmw?utm_source=share&utm_medium=member_desktop 

![7](https://github.com/LHFriis/LCA-Script/assets/166735139/92c75a03-4655-4233-8296-53a167959e80)


#### 8. Forbindelse til tevit / Oversættelse af revit geoemtri til grasshopper
Denne del af scriptet udvælger de specifikke kategorier fra Revit og omdanner disse til Grasshopper data. Det er vigtigt at have Rhino.Inside.Revit til at køre, for at denne del fungerer. Det er denne del som gør, at vi har mulighed for at forbinde grasshopper til Revit modellen.  

![8](https://github.com/LHFriis/LCA-Script/assets/166735139/e387f36e-eb02-45d7-831a-75ab5e9d0197)


#### 9. Udvælgelse af geometri
Denne del er hvor der udvælges hvilken type Revit geometri der skal tildeles hvilken type bygningsdel fra dit LCAbyg udtræk ’LCAbyg - Export – Resultatliste’. For Yder- & Indervægge er det vigtigt at indstille ’Value list’ til om det er en indervæg eller ydervæg. Dette skal gøres for at være sikker på at du får mulighed for at vælge den rigtige bygningsdelstype. Det samme gælder for fundamenter. Her skal du sætte din ’Value list’ til enten m (meter) eller Antal. Dette skyldes at bygningsdelene enten kommer i løbende meter (f.eks. linjefundament) eller antal (f.eks. skruefundament).  
For at tilføje flere bygningsdele skal du blot tænde for ’Typen’ til højre for den ’Type’ du sidst udvalgte elementer i. 

![9](https://github.com/LHFriis/LCA-Script/assets/166735139/7d20e35e-d5b8-4637-9ba1-32eecd069898)


#### 10. beregning af GWP af udvakgte bygningsdele
Denne del beregner GWP for dine udvalgte typer. Her har du også mulighed for at få et overblik over dine udvalgte typer. Her kan du aflæse type, mængde og klimabelastning i enheden (kg. CO<sub>2</sub>-eq.). Årsagen til denne enhed er, at her aflæses kun GWP for bygningsdelen, hvor i punkt 2 ganges bygningens kvadratmeter samt analyseperiode (årstal) på resultatet.

![10](https://github.com/LHFriis/LCA-Script/assets/166735139/2b5fdab2-3883-4def-95d9-352ee3f5b8e1)


## English Guide

To make this script work, it's important to have Rhino.Inside.Revit [RIR] running, and the script should be opened through its Grasshopper window in Revit. If you open the script through Rhino -> Grasshopper, the  RIR components will not be visible. RIR is a free plugin for Revit.

Download link for Rhino.Inside.Revit: 
https://www.rhino3d.com/inside/revit/1.0/ 

In addition to RIR, it's important to have an active Autodesk Revit License, Rhino License, and an LCA building data export with a comparable naming convention as uploaded. You can see examples of the naming convention in the LCAbyg file or Excel export. The building component naming is based on BIM7AA type coding.

BIM7AA Type Coding: 
http://bim7aa.dk/ 

Furthermore you can see the pictures, which belongs to the respective parts under the Danish translation above. 

#### 1. Input data
You need to define the path of your LCA building Excel export. This path should be the uploaded Excel file named 'LCAByg - Export - Result List'. This Excel file contains the structure on which the rest of the script is built. Various building components, etc., are sorted based on this. It's therefore important that this file maintains its structure, as well as the naming of building components from the LCA building extraction. If this changes, remember to update it in the sorting throughout the script or the script will fail.
Here, you should also define which typology is being tested, quantity of floor area (m<sup>2</sup>), analysis period (typically 50 years in Denmark), and your desired uncertainty factor (see the link below for inspiration).

Inspiration/reference for possible uncertainty factors in your LCA project:
https://bygherrepartner.com/bygherrepartner-usikkerhedsmatrix/ 

#### 2. Calculation & Overview of Results
The GWP result in the unit CO<sub>2</sub>-eq./m<sup>2</sup>/year. The result can be viewed both with and without the uncertainty factor. Additionally, the result for building operation, building components (with and without the uncertainty factor), the various building component categories distributed into External & Internal Walls, Roofs, Slabs, Ground Slabs, Foundations, and Windows, Doors, and Glass Facades are shown.

#### 3. Generic Technical Data
Standard values for water, drainage, ventilation, and cooling. These values vary depending on the chosen typology. The standard values are retrieved from: Social- and Housing Board - Presentation of Default Values for Installations. 

Get the standard values for installations at the bottom of this page: 
https://www.sbst.dk/byggeri/baeredygtigt-byggeri/national-strategi-for-baeredygtigt-byggeri/klimakrav-lca-i-bygningsreglementet

#### 4. Check for Excess Elements
Test/overview of whether there is geometry from the Revit model that is not assigned to a building component. It is divided into: External and Internal Walls, Doors, Roofs and Ceilings, Slabs and Ground Slabs.

#### 5. Display model
Here, you can toggle on/off the selected building geometry. You can toggle on/off the following groups: External & Internal Walls, Roofs & Ceilings, Ground Slabs, Foundations, Slabs and Windows, Doors, and Glass Facades.

#### 6. Graphs
Using the Grasshopper plugin 'LunchBox', by right-clicking on "Chart" based on the different groupings, a graph of the selected elements can be displayed. A graph can be displayed for: External & Internal Walls, Roofs & Ceilings, Slabs, Ground Slabs, Foundation, Windows & Doors, and Glass Facades, and a total for various building components in the model.

#### 7. Print / Link to Excel 'Result Sheet'
Using the Grasshopper plugin 'LunchBox', live viewing + graphs in the Excel file named 'Result sheet' can be obtained. However, it's important to have the Excel file open, otherwise, this won't work. The first part of the script under point 7, prints the building component result to each of its worksheets and retrieves data from here to create graphs in the Excel sheet. The second part of the script under point 7 prints main building data such as area, total result, etc., to the main page of the Excel sheet, on the 1st worksheet.

NOTE! It's important to remember to save, and not to have other Excel files open, as this function will overwrite your open Excel file.

Refer to the video below via LinkedIn for live updates in the Excel sheet:
https://www.linkedin.com/posts/lassehfriis_vidensdeling-opensource-grasshopper-activity-7184452905637187584-iZmw?utm_source=share&utm_medium=member_desktop 

#### 8. Link to Revit / Translation of Revit geometry to Grasshopper
This part of the script selects specific categories from Revit and converts them to Grasshopper data. It's important to have Rhino.Inside.Revit running for this part to work. This is the part that allows you to connect Grasshopper to the Revit model.

#### 9. Geometry Selection
This part is where the type of Revit geometry to be assigned to the type of building component from your LCA building export 'LCAbyg - Export - Result List' is selected. For External & Internal Walls, it's important to set the 'Value list' to whether it's an internal wall or an external wall. This should be done to ensure that you have the option to choose the correct building component type. The same goes for foundations. Here, you need to set your 'Value list' to either m (meter) or Quantity. This is because the building components either come in meters (e.g., line foundation) or quantity (e.g., screw foundation).
To add more building components, simply turn on the 'Type' to the right of the 'Type' you last selected elements in.

#### 10. Calculation of GWP of selected building components
This part calculates GWP for your selected types. Here, you also have the option to get an overview of your selected types. Here, you can read type, quantity, and climate load in the unit (kg CO<sub>2</sub>-eq.). The reason for this unit, is that its only GWP for the building component which is calculated in this part. Where in point 2 the building's square meters and analysis period (year) are multiplied by the result.
