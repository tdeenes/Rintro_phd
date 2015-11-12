# Az R és az RStudio IDE telepítése

- az alábbiak nem keverendők:    
    - az R magának a programnyelvnek a neve    
    - a CRAN (Comprehensive R Archive Network) tulajdonképpen ftp- és webszerverek
hálózata, amely az R nyelv kódjának verzióit és dokumentációját tárolja     
        - egy-egy "mirror" tulajdonképpen ezen gyűjtemény egy-egy klónja     
        - a magyarországi mirror-t a Rapporter cég biztosítja a 
http://cran.rapporter.net címen      
        - a CRAN mellett egyéb más "hivatalos" és "nem hivatalos" repozitórium létezik (pl. [Bioconductor](http://www.bioconductor.org/), ill. a nem R-specifikus, Git alapú hosting szolgáltatás, a [GitHub](https://github.com/))
    - minden programnyelvre igaz, hogy jellemzően IDE-ben (Integrated Developmental
Environment), azaz integrált fejlesztői környezetben folyik az alkalmazások 
fejlesztése      
        - az R legnépszerűbb IDE-jét ([RStudio IDE](https://www.rstudio.com/products/RStudio/)) az RStudio nevű cég fejleszti     
        - emellett sok más IDE is használható (a legerőteljesebb az Emacs editorra 
épülő [ESS](http://ess.r-project.org/)), de ha Windows-t használsz, érdemes
lehet telepíteni akár a [Notepad++](https://notepad-plus-plus.org/) szerkesztőt 
is az [NppToR](http://sourceforge.net/projects/npptor/) pluginnal     

### Az R telepítése

- válaszd ki a tartózkodási helyedhez legközelebbi mirror-t, és az operációs
rendszerednek megfelelően telepítsd a "precompiled binary" disztribúciót     
    - ha Windows-t használsz, az [alapváltozaton](http://cran.rapporter.net/bin/windows/base/) felül érdemes 
telepítened az [Rtools](http://cran.rapporter.net/bin/windows/Rtools/) legújabb
változatát is     

### Az RStudio telepítése és használata

- az RStudio telepítése szintén rém egyszerű; telepítsd az operációs rendszerednek
megfelelő legújabb [stabil](https://www.rstudio.com/products/rstudio/download/) vagy a többnyire újabb funkciókkal gazdagított, de
kevésbé stabil [fejlesztői](https://www.rstudio.com/products/rstudio/download/preview/) változatot
- az RStudio nagyon intuitíven használható, de érdemes rászánni az időt a súgó (Help/RStudio Docs) tanulmányozására
- a kurzus során az RStudio-t fogjuk használni, így a legfontosabb funkciókat 
(néhány kényelmi tipp-pel együtt) menet közben bemutatom

![Az RStudio kezelőfelülete (példa)](/images/rstudio.png)
