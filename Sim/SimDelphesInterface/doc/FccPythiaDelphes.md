[]() FCC Pythia + Delphes + Analysis (Documentation)
==================================================

Contents

-   [FCC Pythia + Delphes + Analysis (Documentation)](#fcc-pythia-delphes-analysis-docu)
    -   [Introduction](#introduction)
    -   [Installation Procedure](#installation-procedure)
    -   [How to Run?](#how-to-run)
    -   [FCC-EDM output](#fcc-edm-output)
    -   [Other documentation](#other-documentation)

[]() Introduction
------------------

**A small tutorial on how to study FCC-hh benchmark channels** within
the **[FCCSW
framework](https://github.com/HEP-FCC/FCCSW "FCCSW framework")** with
**[Pythia](http://home.thep.lu.se/~torbjorn/pythia81html/Welcome.html "Pythia")**
generator, **[Delphes](https://cp3.irmp.ucl.ac.be/projects/delphes)** simulation, and 
**[Heppy](https://github.com/cbernet/heppy)** analysis framework.

The event generation (Pythia8) and the detector simulation (Delphes) are handled by the FCCSW. 
Heppy is then configured used to apply an event selection, and produce a flat ROOT tree containing 
the observables that are relevant for the physics channel under study.

[]() Installation Procedure
---------------------------

The analysis is run within the **FCCSW framework** , based on **Gaudi** .
The framework is linked against **Pythia,** **Delphes, FCC-EDM, PODIO,**
... libraries. All the necessary compile tools (CMake, gcc, ...) and
up-to-date libraries are properly installed on **lxplus** machines, in a
FCC dedicated storage area. Thus, one only needs to install the FCCSW
framework. For detailed instructions see [FCCSW installation
instructions](https://github.com/HEP-FCC/FCCSW#installation "FCCSW installation instructions").

In short: 


To get familiar with the **Delphes software** , follow a [quick
tour](https://cp3.irmp.ucl.ac.be/projects/delphes/wiki/WorkBook/QuickTour)
on the Delphes official web page. Let us stress that the Delphes card
needs to be compatible with the Delphes software version. Only in such
case, the support for parametrization and physics object output of all
Delphes modules can be guaranteed!

Input/Output:

-   The Pythia input is required through
    [LHE](https://en.wikipedia.org/wiki/Les_Houches_Accords "Les Houches Event")
    (Les Houches Event) data file together with a special Pythia config
    file or just standard Pythia config file (for details see below).
-   The Pythia output is through transient memory data store using
    [HepMC](http://lcgapp.cern.ch/project/simu/HepMC/ "HepMC") event
    data format.

-   The Delphes input is preferably from event data store, but can be in
    principal read-in from
    [HepMC](http://lcgapp.cern.ch/project/simu/HepMC/) data file.
-   The Delphes output objects (collections, relations) are written out
    through standard
    **[FCC-EDM](https://github.com/HEP-FCC/fcc-edm "FCC-EDM")** (FCC
    event-data model) library. Thus, can be then easily processed by
    other framework reconstruction/analysis modules or written out to
    [ROOT
    tree](https://root.cern.ch/root/html604/TTree.html "ROOT tree") format.
-   In addition, for backwards compatibility and/or testing purposes the
    Delphes output is also supported. The output is in Delphes ROOT tree
    format, using standard Delphes ROOT tree writer.

FCCSW command file (python script) to run Pythia & Delphes:

-   [PythiaDelphes\_config.py](https://github.com/HEP-FCC/FCCSW/blob/master/Sim/SimDelphesInterface/options/PythiaDelphes_config.py)
    : set all GAUDI parameters to run Pythia, Delphes & Output
    module, i.e. configure Pythia, Delphes and ROOT output branches
    (prepared in
    [Sim/SimDelphesInterface/options](https://github.com/HEP-FCC/FCCSW/tree/master/Sim/SimDelphesInterface/options) directory)

Pythia configuration file(s), 2 use cases prepared in
[Generation/data](https://github.com/HEP-FCC/FCCSW/tree/master/Generation/data "Generation/options")
directory:

-   [Pythia\_LHEinput.cmd](https://github.com/HEP-FCC/FCCSW/blob/master/Generation/data/Pythia_LHEinput.cmd "Pythia_LHEinput.cmd")
    : read-in by Pythia-module the LHE file (generated by Madgraph,
    etc.), set Pythia configuration
-   [Pythia\_standard.cmd](https://github.com/HEP-FCC/FCCSW/blob/master/Generation/data/Pythia_standard.cmd "Pythia_standard.cmd")
    : no input, set Pythia configuration


Delphes configuration card - use the official FCC-hh experiment card located in
[Sim/SimDelphesInterface/data](https://github.com/HEP-FCC/FCCSW/tree/master/Sim/SimDelphesInterface/data)
directory:

-   [FCChh\_DelphesCard\_Baseline\_v01.tcl](https://github.com/HEP-FCC/FCCSW/blob/master/Sim/SimDelphesInterface/data/FCChh_DelphesCard_Baseline_v01.tcl)
    : FCC-hh baseline detector desctription

Program workflow:

![PythiaDelphes\_ZDrasal\_Scheme.jpg](https://twiki.cern.ch/twiki/pub/FCC/FccPythiaDelphes/PythiaDelphes_ZDrasal_Scheme.jpg "PythiaDelphes_ZDrasal_Scheme.jpg"){width="675"
height="343"}

[]() Installation Procedure
---------------------------

The analysis is run within a **FCCSW framework** , based on **Gaudi** .
The framework is linked against **Pythia,** **Delphes, FCC-EDM, PODIO,**
... libraries. All the necessary compile tools (CMake, gcc, ...) and
up-to-date libraries are properly installed on **lxplus** machines, in a
FCC dedicated storage area. Thus, one only needs to install the FCCSW
framework. For detailed instructions see [FCCSW installation
instructions](https://github.com/HEP-FCC/FCCSW#installation "FCCSW installation instructions")
.

To get familiar with the **Delphes software** , follow a [quick
tour](https://cp3.irmp.ucl.ac.be/projects/delphes/wiki/WorkBook/QuickTour)
on the Delphes official web page. Let us stress that the Delphes card
needs to be compatible with the Delphes software version. Only in such
case, the support for parametrization and physics object output of all
Delphes modules can be guaranteed!

[]() How to Run?
----------------

Login to lxplus machine and **don't forget** to source **init.sh** ,
anytime you log in!

``` {style="padding-left: 30px;"}
cd FCCSW
source init.sh
```

First, start with the configuration files, adjust them accordingly:

-   **PythiaDelphes\_config.py** : FCCSW run config file --&gt; defines
    input/output, main algorithms running (i.e. Pythia & Delphes),
    Pythia starting configuration, Delphes detector/running sequence
    configuration ...
    -   Variables to be set-up:
    -   `             nEvents           ` --&gt; events to be simulated
    -   `             messageLevel           ` --&gt; GAUDI messaging
        verbosity: ERROR, WARNING, INFO, DEBUG, ... --&gt; use WARNING
        or INFO
    -   `             pythiaconfFile           ` --&gt; Pythia
        configuration file (use either Pythia\_LHEinput.cmd
        or Pythia\_standard.cmd)
    -   `             delphesCard           ` --&gt; Delphes
        configuration file (use official Delphes card)
    -   `             delphesHepMCInFile           ` --&gt; Delphes
        input file (use "" to read <span class="twikiNewLink"> HepMC
        </span> directly from Pythia, i.e. from transient data store)
    -   `             delphesRootOutFile           ` --&gt; Delphes
        output file (use "" to avoid extra output with Delphes objects
        to ROOT file, FCC-EDM objects automatically written out!)
    -   `             delphesXXXOutArray           ` --&gt; Define
        Delphes output arrays to be processed as FCC-EDM XXX particles
        (muons, electrons, etc.) --&gt; various Delphes modules provide
        the same type of particle with different level of processing.
        (For better understanding, watch the content of the Delphes card
        and search e.g. for muons to see how individual Delphes modules
        work out muon particles. Focus on
        `      OutputArray     ` variable.)

-   **Pythia\_LHEinput.cmd** : An example of Pythia configuration to
    execute and work-out (process & hadronize) LHE event-data file
    (provided by e.g. Madgraph etc.)
    -   Variables to be set-up:
    -   `             PartonLevel:MPI = on/off           ` --&gt; Switch
        on/off Multi-Particle-Interaction
    -   `             PartonLevel:ISR = on/off           ` --&gt; Switch
        on/off Initial-State-Radiation
    -   `             PartonLevel:FSR = on/off           ` --&gt; Switch
        on/off Final-State-Radiation
    -   `             HadronLevel:all = on/off           ` --&gt; Switch
        on/off Hadronization
    -   `             HadronLevel:Decay = on/off           ` --&gt;
        Switch on/off Decays
    -   `             Beams:LHEF = data/name.lhe           ` --&gt;
        Define LHE event data file

-   **Pythia\_standard.cmd** : An example of standard Pythia
    configuration to start generation.
    -   Variables to be set-up (different from those already described
        for Pythia\_LHEinput.cmd):
    -   `             Random:setSeed = on           ` --&gt; Apply
        user-set seed everytime the Pythia::init is called
    -   `             Random:seed = 0           ` --&gt; Set seed:
        -1=default seed, 0=seed based on time, &gt;0 user seed number

-   **FCChh\_DelphesCard\_Baseline\_vXX.tcl** : Official FCChh Delphes
    configuration card, defining sequence of Delphes modules to be
    executed and detector characterization.

**Run FCCSW** using the following command:

``` {style="padding-left: 30px;"}
./run gaudirun.py Sim/SimDelphesInterface/options/PythiaDelphes_config.py
```

[]() FCC-EDM output
-------------------

The following collections and relations will be saved in the output
file. Each collection (relation) is handled in the FCCSW through a
dedicated handle. To get an idea on the EDM, have a look at the [yaml](https://github.com/HEP-FCC/fcc-edm/blob/master/edm.yaml) file.
For reference, the handle name (specified in a
[DelphesPythia\_config.py](https://github.com/HEP-FCC/FCCSW/blob/master/Sim/SimDelphesInterface/options/PythiaDelphes_config.py)
file) is given in the brackets \[\] below:

-   **Collections:**
    -   `             fcc::MCParticleCollection           ` --&gt;
        generated particles `      [genParticles]     `
    -   `             fcc::GenVertexCollection           ` --&gt;
        generated vertices `      [genVertices]     `
    -   `             fcc::GenJetCollection           ` --&gt; generated
        jets `      [genJets]     `
    -   `             fcc::ParticleCollection           ` --&gt;
        reconstructed muons `      [muons]     ` , electrons
        `      [electrons]     ` , charged particles
        `      [charged]     ` , neutral particles
        `      [neutral]     ` , photons `      [photons]     ` and jet
        constituents `      [jetParts]     `
    -   `             fcc::JetCollection           ` --&gt;
        reconstructed jets `      [jets]     `
    -   `             fcc::METCollection           ` --&gt;
        reconstructed missing Et `      [met]     `
    -   `             fcc::TaggedJetCollection           ` --&gt;
        collection of reconstructed tagged jets - b-tags, c-tags and tau-tags, holds a relation to the original jet
        `      [bTags, cTags, tauTags]     `
    -   `             fcc::TaggedParticleCollection           ` --&gt;
        collection reconstructed isolation tag info for electrons, muons and
        photons, holds a relation to the original particle `      [muonITags, electronITags, photonITags]     `

-   **Relations:**
    -   `             fcc::ParticleMCParticleAssociationCollection           `
        --&gt; relations of reconstructed object to MC particle for
        muons `      [muonsToMC]     ` , electrons
        `      [electronsToMC]     ` , charged particles
        `      [chargedToMC]     ` , neutral particles
        `      [neutralToMC]     ` and photons
        `      [photonsToMC]     `

    
[]() Other documentation
------------------------

For more details, you can have a look at:

-   [Talk](https://indico.cern.ch/event/446602/contribution/6/attachments/1238094/1818990/PythiaDelphes_ZDrasal.pdf)
    (FCC-hh group) on Mar 3rd 2016
-   [Talk](https://indico.cern.ch/event/443015/contribution/2/attachments/1155286/1660371/PythiaDelphes_ZDrasal.pdf)
    (FCC-hh group) on Sep 15th 2015
-   [Talk](https://indico.cern.ch/event/399484/contribution/0/attachments/800169/1096662/FCCSW_MDG_040615.pdf)
    (FCC software group) on Jun 4th 2015
-   [Talk](https://indico.cern.ch/event/370378/contribution/2/attachments/736634/1010596/FCCSW_MDG_050215.pdf)
    (FCC sofware group) on Feb 5th 2015

------------------------------------------------------------------------
