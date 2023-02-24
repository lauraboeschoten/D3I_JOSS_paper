---
title: 'D3I: A software tool for digital data donation'
tags:
  - data donation
  - digital trace data
  - local processing
  - pyodide
  - elixir
  
authors:
  - name: Laura Boeschoten
    orcid: 0000-0000-0000-0000
    corresponding: true # 
    affiliation: 1
  - name: Niek C. de Schipper
    orcid: 0000-0000-0000-0000
    affiliation: 2
  - name: Adri\"enne M. Mendrik
    orcid: 0000-0000-0000-0000
    affiliation: 3
  - name: Emiel van der Veen
    orcid: 0000-0000-0000-0000
    affiliation: 3
  - name: Bella Struminskaya
    orcid: 0000-0000-0000-0000
    affiliation: 1
  - name: Heleen Janssen
    orcid: 0000-0000-0000-0000
    affiliation: 2
  - name: Theo B. Araujo
    orcid: 0000-0000-0000-0000
    affiliation: 2
    
affiliations:
 - name: Utrecht University, The Netherlands
   index: 1
 - name: University of Amsterdam, The Netherlands
   index: 2
 - name: Eyra.co, the Netherlands
   index: 3
   
date: 8 February 2023
bibliography: paper.bib

---

# Summary

*A summary describing the high-level functionality and purpose of the software for a diverse, non-specialist audience.*

Recently, a new workflow was introduced that allows research participants to donate their digital trace data for research [@boeschoten2022framework]. In this workflow, the digital traces of participants are processed locally on their own devices prior to providing informed consent to share the relevant features with the researchers. 

This *data donation workflow* consists of the following steps: First the participant requests a digital copy of their personal data at the platform of interest. Second, they download it onto their personal device. Third, by means of *local processing*, only the features of interest to the researcher are extracted from that DDP. Fourth, the participant inspects the extracted features after which they can consent to donate. Only after providing this consent, the donated data is sent to a server which can be accessed by the researcher for further analyses. 

In this paper, we introduce D3I. D3I is a software tool that allows researchers to configure the local processing step of the data donation workflow, allowing the researcher to collect exactly the digital traces needed to answer their research question. With D3I, a researcher decides: 

- What is communicated to the participant.
- Which digital platforms are being investigated.
- Which digital traces are collected exactly. 
- How the extracted data is visualized.
- Where to store the extracted data. 


# Statement of need

*A Statement of need section that clearly illustrates the research purpose of the software and places it in the context of related work.*

In our everyday lives, we leave more and more digital traces behind. Whether we like a post on Instagram, or an send a message on WhatsApp. Even when we check-in at public transportation, or when we do a bank transaction we leave behind a digital trace. The promise of digital humanities and computational social science has been that researchers can utilize these digital traces to study humam behavior and interaction at an unprecendented level of detail [@king2011ensuring]. 

However, while the amount of digital trace data increases, most are closed off in proprietary archives of commercial corporations, with only a subset being available to a small set of elite researchers at a platform's discretion, through initiatives such as Social Science One [@king2020new]), or through increasingly restricted and opaque APIs [@bruns2019after; @freelon2018computational; @perriam2020digital].

An alternative approach to gain access to digital traces is enabled thanks to the European Union's General Data Protection Regulations (GDPR) right to data access and data portability [@ausloos2019gdpr]. Thanks to this legislation, all data processing entities are required to provide citizens a digital copy of their personal data upon request, which typically come in the form of .zip files to which we refer as *Data Download Packages* (DDPs).

This allows researchers to invite participants to share their DDPs. A major challenge is however that DDPs potentially contain very sensitive data, and often not all data is needed to answer the specific research question under investigation. To circumvent these challenges, @boeschoten2022framework developed an alternative workflow:  First, the research participant requests their personal DDP at the platform of interest. Second, they download in onto their own personal device. Third, by means of local processing, only the features of interest to the researcher are extracted from that DDP. Fourth, the participant inspects the extracted features after which they can consent (or decline) to donate. Only after providing this consent, the donated data is sent to a server which can be accessed by the researcher for further analyses. 

**Insert plaatje data donatie flow**

In the last years, researchers have used multiple approaches to deal with the privacy issues related to donation of DDPs. For example, @van2022promises requested participants to share their complete Instagram DDPs, which were immediately de-identified prior to further analyses [@boeschoten2021automatic]. @kmetty2022your requested participants to visit a research site, where they downloaded their DDPs which were then de-identified under the participant's supervision. @araujo2022osd2f developed software that allows for the participants to decide per data instance within a DDP whether they want to delete it prior to donation. @boeschoten2022privacy introduce a proof-of-concept of software that allows for local processing of DDPs, resulting in aggregated, de-identified data. Although especially OSD2F and PORT are promising pieces of software, they know a number of drawbacks in it's current form. While OSD2F is relatively easy to configure, it lacks the flexibility to further process the data from DDPs. Although PORT provides this feature, it is very challenging for a researcher to configure a study using PORT without extensive programming knowledge.

In this paper, we introduce D3I, an open-source software tool that combines the most useful features from both PORT and OSD2F. With D3I, any researcher can fully configure their own data donation study. It creates a website that guides participants through the data donation steps. Researchers can tailor this website to their own DDP(s) of interest on process these in their desired way, making use of functionalities that have been previously developed for PORT and OSD2F. 


# Features

D3I enables researchers to configure their own data donation flow, tailored to to the needs of their study. This allows the researcher to collect exactly those digital traces needed to answer their research question, without any unnecessary bycatch. 

In order to configure a tailored data donation flow, D3I allows for a researcher to configure the elements described below.

### Study information 

Data donation is often part of a larger study design, in which researchers inform participants about the study purpose, ask for informed consent and potentially also include other approaches for data collection, such as a questionnaire. 

Important for the data donation element are the explanations regarding data requests and data downloads at the platforms of interest, information regarding privacy and contact and all the communication that guides participants through the data donation procedure that is present on the website. 

The researcher can tailor all this information towards the level of their intended study population, and the platform(s) under study.

**Niek, kun je hier iets zeggen over hoe je teksten kunt aanpassen? En misschien ook over hoe je naar losse documenten kunt linken?**


### The Data Download Package(s)

D3I is platform agnostic, DDPs of any platform can be used. It is also possible to incorporate donations of DDPs from multiple platforms. In that case, the researcher considers the order in which the platforms are presented, and a `skip` button can be placed, for example for participants who wish to not participate for the first platform, but does want to participate for the second.

**Niek, kun je hier iets zeggen over hoe je dus extra instances van donatieschermen aan kunt maken?**


### Data extraction and processing 

To only extract from the DDP the features that are of interest to the research, D3I makes use of Pyodide. This allows us to run Python in the web-browser of the participant. A Python script is then written specifically for this research question, as it is tailored to the DDP of interest, and extracts only the data required for the specific research question.

**Niek, wil je hier nog meer aan toevoegen? Zie ook https://www.sciencedirect.com/science/article/pii/S2666389922000174 ik weet niet of er sindsdien veel veranderd is?**

To design a Python extraction script in such a way that the privacy of the participants is preserved as much as possible, the researcher can make use of two important features. First, besides extracting data from the DDP, it is also possible to further process this to better match the research question. 

**Insert plaatje raw GSLH versus aggregate**

Second, you can allow an interaction between the participant and the DDP, as such that the participant can give more meaning to the data. 

**Insert plaatje Whatsap radio buttons**


### Data visualization 

After data extraction and potential further processing, the data is shown on screen to the participants, as such that they can inspect it prior to donation. 

**Niek, volgens mij was het iets dat de data in een pandas dataframe werd gestopt en zo kon laten zien, kun jij hier meer over vertellen? En ook hoe een visualisatie van evt een histogram oid zou werken?**

The participant can have more autonomy over what data is shared exactly, by allowing them to remove individual rows from a table, or to even allow for tables to be removed completely. These options can particularly be useful if you are working with very sensitive data, such as raw private messages. 


### Data storage

### Deployment 


- deployment --> azure in release instructies staat hoe je een versie moet bouwen. geschikt om bepaalde omgeving te deployen. Bij SURF direct op een VM, SURF gebruikt S3 buckets

- om tool te deployen moet je hele platform deployen. denk niet dat jullie willen dat ze jullie hele platform deployen. 

Tool is nu met een azure configuratie die geschikt is om met de meest gevoelige data om te gaan. Dit is niet per se nodig, maar staat op die manier elke vorm van onderzoek toe. 


# Architecture 

# Example 

# Conclusion

# Acknowledgements

# Mathematics

Single dollars ($) are required for inline mathematics e.g. $f(x) = e^{\pi/x}$

Double dollars make self-standing equations:

$$\Theta(x) = \left\{\begin{array}{l}
0\textrm{ if } x < 0\cr
1\textrm{ else}
\end{array}\right.$$

You can also use plain \LaTeX for equations
\begin{equation}\label{eq:fourier}
\hat f(\omega) = \int_{-\infty}^{\infty} f(x) e^{i\omega x} dx
\end{equation}
and refer to \autoref{eq:fourier} from text.

# Citations

Citations to entries in paper.bib should be in
[rMarkdown](http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html)
format.

If you want to cite a software repository URL (e.g. something on GitHub without a preferred
citation) then you can do it with the example BibTeX entry below for @fidgit.

For a quick reference, the following citation commands can be used:
- `@author:2001`  ->  "Author et al. (2001)"
- `[@author:2001]` -> "(Author et al., 2001)"
- `[@author1:2001; @author2:2001]` -> "(Author1 et al., 2001; Author2 et al., 2002)"

# Figures

Figures can be included like this:
![Caption for example figure.\label{fig:example}](figure.png)
and referenced from text using \autoref{fig:example}.

Figure sizes can be customized by adding an optional second parameter:
![Caption for example figure.](figure.png){ width=20% }

# Acknowledgements

We acknowledge contributions from Brigitta Sipocz, Syrtis Major, and Semyeong
Oh, and support from Kathryn Johnston during the genesis of this project.

# References
