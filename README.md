# IPO (Input-Production-Output) Protocol 0.1

*Link to web: []()  *

This is a project folder template pretty much based on the **TIER** protocol (Teaching Integrity in Empirical Research). TIER "promotes the integration of principles and practices related to transparency and replicability in the research training of social scientists." (more information in [https://www.projecttier.org/](https://www.projecttier.org/)).

The implementation of reproducibility in this kinds of protocols is based on generating a self-contained set of files that can be shared and executed by anyone. In other words, it must have all you need to run and re-run the analysis.

TIER proposes a standardized way to organize a research project in one single folder (the `project` folder) which at the same time organizes files in a structured set of folders, called TIER protocol. Its 4th version is available in the Open Science Framework, link [here](https://osf.io/4cxed/).

The **IPO** protocol follows the rationale of TIER, with some minor innovations:

- attempts a model easy to memorize and related with the analysis workflow (Input-Production-Output), where production refers to processing and analyzing data.

- adds an "Input" folder, which is has a broader scope containing the original "Data" folder but also other possible inputs, such as external images and bibliography files.

- The Data folder is also simplified, including now only an "Original" and "Processed" structure.

- it is more specifically oriented for working with open software & collaboration tools, such as R/Rmarkdown and Git/Github:

  - it modifies the files to .Rmd (Rmarkdown) instead of .txt, which after being rendered in R (vía knitr) generates the corresponding html files

  - in the root the original paper.pdf becomes paper.Rmd and the corresponding publication file paper.html

  - in the root there is a project.Rproj file for working with the project feature in Rstudio (more information [here](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects)).

## Files & Folder Structure

```
├── input: external information such as images, documents, bib files
|   ├── data:
│     ├── proc     : processed data files
│     ├── original : original data files & metadata when available
│   ├── images
│   ├── bib: bilbliography files
|
├── production:
│   - preparation.Rmd
│   - analysis.Rmd
│
├── output: tables, graphs, logs, anything produced by the code
│   ├── graphs
│   ├── tables
|
- README.md : the general introductory file
- paper.Rmd / paper.html: the paper

```
## Download

- To download a zip file with the folders & files click [here]()
- you might also fork this project from Github, which is a better option in order to keep track of the use of this protocol.

## Notes

- as the R/Rmarkdown environment allows combining text, analysis & outputs, the corresponding folders (production & output) could sound redundant. This is probably the case for brief analysis and short reports. Nevertheless, when working on a paper/thesis/group project it is certainly advisable to separate inputs, analysis and outputs for the sake of order and reproducibility despite working with Rmarkdown.

- for making the work easier in Rstudio you might want to make the `project` folder a Rproject folder. This will make that the working directory automatically will be referred to the root, besides activating other functions within Rstudio. For this, just go to File->New project->Existing directory, and point to the project folder. This will create a file with .Rproj extension that when clicked it will open Rstudio and the project folder as a root. In this way it avoids generating local individual working directories (the R command `setwd`), which do not facilitates reproducibility.

- besides having one project folder where all information is contained, the technical key for working within this structure is to save and load files located in different places through **relative paths** (RP), which allows connecting different files within the same project folder. For instance, for loading a data file from the `original` folder from the `preparation.Rmd` script:

```
load("../input/data/original/data.csv")
```
  The `../` characters means "one level up" in the folder structure. In this case, taking as a reference a script within the `production` folder, we need to go up to the `project` or root folder, and from there go down to  `input/data/original/data.csv`

- for saving tables and any output produced in R use the function `sink`. For instance, for a `stargazer` descriptive table from `data`:

```
sink("output/tables/table1.txt")
stargazer(data, )
sink()
```
  The rationale is to tell in which file to save or sink what comes next, and stop saving with `sink()`

  Then, to call the output from the paper.Rmd file:
`<div><object data="output/tables/table1.txt"></object></div>`

- for saving graphs, after producing and viewing the graph:

```
dev.copy(png,"output/graphs/graph1.png",width=600,
      	height=600); dev.off()
```
  Then, to call the graph from the paper.Rmd file:

```
![](output/graphs/graph1.png)
```
