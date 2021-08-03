# PDFigCapX
Website:
https://www.eecis.udel.edu/~compbio/PDFigCapX
Our paper at:
https://doi.org/10.1093/bioinformatics/btz228

## Codes 
* Main function:
Command: python /code/FigCap.py
Inputs:
input_path: The folder contains PDF files that need to be parsed.
output_path: The folder where parsing results will be saved.
Outputs:
For each document in the \textit{input\_path}, the main function will generate a corresponding folder with the same name as the original document in the \textit{output\_path}. All extracted figures (in jpg format), captions (in text format) and their coordinate information (in json format) will be saved in the corresponding folder.

* Explainations of submodules called by FigCap.py
\noindent\textbf{Submodule 1:} PDF parsing using xpdf (Lines 51-57 in FigCap.py)\\
\noindent\underline{Inputs: }\\
\noindent\textit{Xpdf\_path:} The path to the xpdf code. In our implementation, the path is set to /usa/pengyuan/Documents/RESEARCH/xpdf-tools-linux-4.00/bin/pdftohtml. This code is also available online at: https://www.xpdfreader.com/pdftohtml-man.html. \\
\noindent\textit{pdf\_path:} The document that needs to be parsed.\\
\noindent\textit{html\_file\_path:} The folder contains all parsing results obtained by using xpdf.\\
\noindent\underline{Outputs:}\\
\noindent{A folder with the same name as the PDF document will be created in the \textit{html\_file\_path}. For each page in the document, an HTML file containing the textual information and an text-striped image will be saved in the newly created folder.}

\noindent\textbf{Submodule 2:} Obtain layout information (/code/pdf\_info.py)\\
\noindent\underline{Inputs: }\\
\noindent\textit{pdf\_path:} The path to the PDF file.\\
\noindent\textit{html\_file\_path:} The path to the folder generated by xpdf in Submodule 1.\\
\noindent\underline{Outputs:}\\
\noindent{A json file containing all layout information and textual information is saved in \textit{html\_file\_path} and this information will be passed to Submodule 3.}

\noindent\textbf{Submodule 3:} Disambiguation of figures and captions (/code/xpdf\_process.py)\\
\noindent\underline{Inputs:}\\
\noindent\textit{pdf\_path:} The path to the PDF file.\\
\noindent\textit{html\_file\_path:} The path to the folder generated by xpdf in Submodule 1.\\
\noindent\underline{Outputs:}\\
\noindent{A python dictionary that contains the coordinate information of all identified figures and captions.}

\noindent\textbf{Submodule 4:} Extract figures and captions as files (Lines 78-120 in FigCap.py)\\
\noindent\underline{Inputs:}\\
\noindent\textit{data[pdf]:} The python dictionary that contains the coordinates of all identified figures and captions. The variable \textit{pdf} is the ID of the PDF file.\\
\noindent\textit{Output\_path\_file:} The path that figures and captions will be saved.\\
\noindent\underline{Outputs:}\\
\noindent{Figures (in jpg format), captions (in text format) and their coordinate information (in a json format) will be saved in the \textit{output\_path\_folder} folder.}

## Datasets
### GXD-200 dataset:
Dataset path: /datasets/GXD200
Description: The GXD-200 dataset contains 200 documents selected from a collection curated by Jackson Lab's Gene Expression Database. There are 1335 figures, 1298 figure-associated captions, and 1298 figure and caption pairs in this dataset. 
Ground-truth annotations: /datasets/GXD200/GT_GXD200.json

### PMD-200 dataset:
Dataset path: /datasets/PMC200
Description: The PMC-200 dataset contains 200 biomedical documents selected from the PubMed Central (PMC) Open Access Subset (2018). There are 1042 figures, 1032 captions, and 1032 figure and caption pairs in this dataset. 
Ground-truth annotations: /datasets/PMC200/GT_PMC200.json
