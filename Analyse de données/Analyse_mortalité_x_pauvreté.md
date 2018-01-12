Analyse mortalité x indicateur de pauvreté
================

GitHub Documents
----------------

This is an R Markdown format used for publishing markdown documents to GitHub. When you click the **Knit** button all R code chunks are run and a markdown file (.md) suitable for publishing to GitHub is generated.

Afin de pouvoir étudier l'influence des indicateurs de pauvreté sur la mortalité, on détermine d'abord les indicateurs que l'on va étudier. Dans un premier temps on regarde, le nombre de valeurs manquantes pour chacune des variables. En effet si le nombre de valeurs manquantes est trop important, il n'est pas pertinent de conserver la variable.

On crée une fonction qui calcule le nombre de valeurs manquantes pour toutes les variables :

``` r
load(file="~/PST.RData")
## création du dataframe à remplir
Poverty_NA<- data.frame(matrix(ncol = 4, nrow = 0))
colnames(Poverty_NA)<-c("Code","Nom","Nombre de NA","% de NA")
for (i in 1:nrow(Poverty)) ## Poverty = dataset des indicateurs de pauvreté et leur signification
  {
      ### Calcul de NA
      code=Poverty[i,3]
      nbNA=sum(is.na(WorldBank[[toString(code)]]))
      Poverty_NA[i,]<-list(toString(code),toString(Poverty[i,4]),nbNA,nbNA/46*100)
}
##Affichage du résultat
library(knitr)
kable(Poverty_NA,caption="Valeurs manquantes pour les variables Pauvreté")
```

| Code                      | Nom                                                                                                              |  Nombre de NA|    % de NA|
|:--------------------------|:-----------------------------------------------------------------------------------------------------------------|-------------:|----------:|
| SI.DST.02ND.20            | Income share held by second 20%                                                                                  |            16|   34.78261|
| SI.DST.03RD.20            | Income share held by third 20%                                                                                   |            16|   34.78261|
| SI.DST.04TH.20            | Income share held by fourth 20%                                                                                  |            16|   34.78261|
| SI.DST.05TH.20            | Income share held by highest 20%                                                                                 |            16|   34.78261|
| SI.DST.10TH.10            | Income share held by highest 10%                                                                                 |            16|   34.78261|
| SI.DST.FRST.10            | Income share held by lowest 10%                                                                                  |            16|   34.78261|
| SI.DST.FRST.20            | Income share held by lowest 20%                                                                                  |            16|   34.78261|
| SI.POV.2DAY               | Poverty headcount ratio at $3.10 a day (2011 PPP) (% of population)                                              |            16|   34.78261|
| SI.POV.DDAY               | Poverty headcount ratio at $1.90 a day (2011 PPP) (% of population)                                              |            16|   34.78261|
| SI.POV.GAP2               | Poverty gap at $3.10 a day (2011 PPP) (%)                                                                        |            16|   34.78261|
| SI.POV.GAPS               | Poverty gap at $1.90 a day (2011 PPP) (%)                                                                        |            16|   34.78261|
| SI.POV.GINI               | GINI index (World Bank estimate)                                                                                 |            16|   34.78261|
| SI.POV.NAHC               | Poverty headcount ratio at national poverty lines (% of population)                                              |            33|   71.73913|
| SL.AGR.EMPL.FE.ZS         | Employment in agriculture, female (% of female employment)                                                       |            16|   34.78261|
| SL.AGR.EMPL.MA.ZS         | Employment in agriculture, male (% of male employment)                                                           |            16|   34.78261|
| SL.AGR.EMPL.ZS            | Employment in agriculture (% of total employment)                                                                |            15|   32.60870|
| SL.EMP.1524.SP.FE.NE.ZS   | Employment to population ratio, ages 15-24, female (%) (national estimate)                                       |            41|   89.13043|
| SL.EMP.1524.SP.FE.ZS      | Employment to population ratio, ages 15-24, female (%) (modeled ILO estimate)                                    |            21|   45.65217|
| SL.EMP.1524.SP.MA.NE.ZS   | Employment to population ratio, ages 15-24, male (%) (national estimate)                                         |            41|   89.13043|
| SL.EMP.1524.SP.MA.ZS      | Employment to population ratio, ages 15-24, male (%) (modeled ILO estimate)                                      |            21|   45.65217|
| SL.EMP.1524.SP.NE.ZS      | Employment to population ratio, ages 15-24, total (%) (national estimate)                                        |            40|   86.95652|
| SL.EMP.1524.SP.ZS         | Employment to population ratio, ages 15-24, total (%) (modeled ILO estimate)                                     |            21|   45.65217|
| SL.EMP.INSV.FE.ZS         | Share of women in wage employment in the nonagricultural sector (% of total nonagricultural employment)          |            30|   65.21739|
| SL.EMP.MPYR.FE.ZS         | Employers, female (% of female employment)                                                                       |            33|   71.73913|
| SL.EMP.MPYR.MA.ZS         | Employers, male (% of male employment)                                                                           |            33|   71.73913|
| SL.EMP.MPYR.ZS            | Employers, total (% of total employment)                                                                         |            33|   71.73913|
| SL.EMP.SELF.FE.ZS         | Self-employed, female (% of female employment)                                                                   |            46|  100.00000|
| SL.EMP.SELF.MA.ZS         | Self-employed, male (% of male employment)                                                                       |            46|  100.00000|
| SL.EMP.SELF.ZS            | Self-employed, total (% of total employment)                                                                     |            46|  100.00000|
| SL.EMP.TOTL.SP.FE.NE.ZS   | Employment to population ratio, 15+, female (%) (national estimate)                                              |            31|   67.39130|
| SL.EMP.TOTL.SP.FE.ZS      | Employment to population ratio, 15+, female (%) (modeled ILO estimate)                                           |            21|   45.65217|
| SL.EMP.TOTL.SP.MA.NE.ZS   | Employment to population ratio, 15+, male (%) (national estimate)                                                |            31|   67.39130|
| SL.EMP.TOTL.SP.MA.ZS      | Employment to population ratio, 15+, male (%) (modeled ILO estimate)                                             |            21|   45.65217|
| SL.EMP.TOTL.SP.NE.ZS      | Employment to population ratio, 15+, total (%) (national estimate)                                               |            31|   67.39130|
| SL.EMP.TOTL.SP.ZS         | Employment to population ratio, 15+, total (%) (modeled ILO estimate)                                            |            21|   45.65217|
| SL.EMP.VULN.FE.ZS         | Vulnerable employment, female (% of female employment)                                                           |            33|   71.73913|
| SL.EMP.VULN.MA.ZS         | Vulnerable employment, male (% of male employment)                                                               |            33|   71.73913|
| SL.EMP.VULN.ZS            | Vulnerable employment, total (% of total employment)                                                             |            33|   71.73913|
| SL.EMP.WORK.FE.ZS         | Wage and salaried workers, female (% of female employment)                                                       |            33|   71.73913|
| SL.EMP.WORK.MA.ZS         | Wage and salaried workers, male (% of male employment)                                                           |            33|   71.73913|
| SL.EMP.WORK.ZS            | Wage and salaried workers, total (% of total employment)                                                         |            33|   71.73913|
| SL.FAM.WORK.FE.ZS         | Contributing family workers, female (% of female employment)                                                     |            33|   71.73913|
| SL.FAM.WORK.MA.ZS         | Contributing family workers, male (% of male employment)                                                         |            33|   71.73913|
| SL.FAM.WORK.ZS            | Contributing family workers, total (% of total employment)                                                       |            33|   71.73913|
| SL.GDP.PCAP.EM.KD         | GDP per person employed (constant 2011 PPP $)                                                                    |            21|   45.65217|
| SL.IND.EMPL.FE.ZS         | Employment in industry, female (% of female employment)                                                          |            16|   34.78261|
| SL.IND.EMPL.MA.ZS         | Employment in industry, male (% of male employment)                                                              |            16|   34.78261|
| SL.IND.EMPL.ZS            | Employment in industry (% of total employment)                                                                   |            14|   30.43478|
| SL.SRV.EMPL.FE.ZS         | Employment in services, female (% of female employment)                                                          |            16|   34.78261|
| SL.SRV.EMPL.MA.ZS         | Employment in services, male (% of male employment)                                                              |            16|   34.78261|
| SL.SRV.EMPL.ZS            | Employment in services (% of total employment)                                                                   |            14|   30.43478|
| SL.TLF.ACTI.1524.FE.NE.ZS | Labor force participation rate for ages 15-24, female (%) (national estimate)                                    |            18|   39.13043|
| SL.TLF.ACTI.1524.FE.ZS    | Labor force participation rate for ages 15-24, female (%) (modeled ILO estimate)                                 |            20|   43.47826|
| SL.TLF.ACTI.1524.MA.NE.ZS | Labor force participation rate for ages 15-24, male (%) (national estimate)                                      |            18|   39.13043|
| SL.TLF.ACTI.1524.MA.ZS    | Labor force participation rate for ages 15-24, male (%) (modeled ILO estimate)                                   |            20|   43.47826|
| SL.TLF.ACTI.1524.NE.ZS    | Labor force participation rate for ages 15-24, total (%) (national estimate)                                     |            17|   36.95652|
| SL.TLF.ACTI.1524.ZS       | Labor force participation rate for ages 15-24, total (%) (modeled ILO estimate)                                  |            20|   43.47826|
| SL.TLF.ADVN.FE.ZS         | Labor force with advanced education, female (% of female working-age population with advanced education)         |            41|   89.13043|
| SL.TLF.ADVN.MA.ZS         | Labor force with advanced education, male (% of male working-age population with advanced education)             |            41|   89.13043|
| SL.TLF.ADVN.ZS            | Labor force with advanced education (% of total working-age population with advanced education)                  |            40|   86.95652|
| SL.TLF.BASC.FE.ZS         | Labor force with basic education, female (% of female working-age population with basic education)               |            41|   89.13043|
| SL.TLF.BASC.MA.ZS         | Labor force with basic education, male (% of male working-age population with basic education)                   |            41|   89.13043|
| SL.TLF.BASC.ZS            | Labor force with basic education (% of total working-age population with basic education)                        |            40|   86.95652|
| SL.TLF.CACT.FE.NE.ZS      | Labor force participation rate, female (% of female population ages 15+) (national estimate)                     |            14|   30.43478|
| SL.TLF.CACT.FE.ZS         | Labor force participation rate, female (% of female population ages 15+) (modeled ILO estimate)                  |            20|   43.47826|
| SL.TLF.CACT.FM.NE.ZS      | Ratio of female to male labor force participation rate (%) (national estimate)                                   |            14|   30.43478|
| SL.TLF.CACT.FM.ZS         | Ratio of female to male labor force participation rate (%) (modeled ILO estimate)                                |            20|   43.47826|
| SL.TLF.CACT.MA.NE.ZS      | Labor force participation rate, male (% of male population ages 15+) (national estimate)                         |            14|   30.43478|
| SL.TLF.CACT.MA.ZS         | Labor force participation rate, male (% of male population ages 15+) (modeled ILO estimate)                      |            20|   43.47826|
| SL.TLF.CACT.NE.ZS         | Labor force participation rate, total (% of total population ages 15+) (national estimate)                       |            14|   30.43478|
| SL.TLF.CACT.ZS            | Labor force participation rate, total (% of total population ages 15+) (modeled ILO estimate)                    |            20|   43.47826|
| SL.TLF.INTM.FE.ZS         | Labor force with intermediate education, female (% of female working-age population with intermediate education) |            41|   89.13043|
| SL.TLF.INTM.MA.ZS         | Labor force with intermediate education, male (% of male working-age population with intermediate education)     |            41|   89.13043|
| SL.TLF.INTM.ZS            | Labor force with intermediate education (% of total working-age population with intermediate education)          |            40|   86.95652|
| SL.TLF.TOTL.FE.ZS         | Labor force, female (% of total labor force)                                                                     |            20|   43.47826|
| SL.TLF.TOTL.IN            | Labor force, total                                                                                               |            20|   43.47826|
| SL.UEM.1524.FE.NE.ZS      | Unemployment, youth female (% of female labor force ages 15-24) (national estimate)                              |            22|   47.82609|
| SL.UEM.1524.FE.ZS         | Unemployment, youth female (% of female labor force ages 15-24) (modeled ILO estimate)                           |            21|   45.65217|
| SL.UEM.1524.MA.NE.ZS      | Unemployment, youth male (% of male labor force ages 15-24) (national estimate)                                  |            22|   47.82609|
| SL.UEM.1524.MA.ZS         | Unemployment, youth male (% of male labor force ages 15-24) (modeled ILO estimate)                               |            21|   45.65217|
| SL.UEM.1524.NE.ZS         | Unemployment, youth total (% of total labor force ages 15-24) (national estimate)                                |            21|   45.65217|
| SL.UEM.1524.ZS            | Unemployment, youth total (% of total labor force ages 15-24) (modeled ILO estimate)                             |            21|   45.65217|
| SL.UEM.ADVN.FE.ZS         | Unemployment with advanced education, female (% of female labor force with advanced education)                   |            39|   84.78261|
| SL.UEM.ADVN.MA.ZS         | Unemployment with advanced education, male (% of male labor force with advanced education)                       |            39|   84.78261|
| SL.UEM.ADVN.ZS            | Unemployment with advanced education (% of total labor force with advanced education)                            |            38|   82.60870|
| SL.UEM.BASC.FE.ZS         | Unemployment with basic education, female (% of female labor force with basic education)                         |            39|   84.78261|
| SL.UEM.BASC.MA.ZS         | Unemployment with basic education, male (% of male labor force with basic education)                             |            39|   84.78261|
| SL.UEM.BASC.ZS            | Unemployment with basic education (% of total labor force with basic education)                                  |            38|   82.60870|
| SL.UEM.INTM.FE.ZS         | Unemployment with intermediate education, female (% of female labor force with intermediate education)           |            39|   84.78261|
| SL.UEM.INTM.MA.ZS         | Unemployment with intermediate education, male (% of male labor force with intermediate education)               |            39|   84.78261|
| SL.UEM.INTM.ZS            | Unemployment with intermediate education (% of total labor force with intermediate education)                    |            38|   82.60870|
| SL.UEM.NEET.FE.ZS         | Share of youth not in education, employment or training, female (% of female youth population)                   |            41|   89.13043|
| SL.UEM.NEET.MA.ZS         | Share of youth not in education, employment or training, male (% of male youth population)                       |            41|   89.13043|
| SL.UEM.NEET.ZS            | Share of youth not in education, employment or training, total (% of youth population)                           |            41|   89.13043|
| SL.UEM.TOTL.FE.NE.ZS      | Unemployment, female (% of female labor force) (national estimate)                                               |             9|   19.56522|
| SL.UEM.TOTL.FE.ZS         | Unemployment, female (% of female labor force) (modeled ILO estimate)                                            |            21|   45.65217|
| SL.UEM.TOTL.MA.NE.ZS      | Unemployment, male (% of male labor force) (national estimate)                                                   |             9|   19.56522|
| SL.UEM.TOTL.MA.ZS         | Unemployment, male (% of male labor force) (modeled ILO estimate)                                                |            21|   45.65217|
| SL.UEM.TOTL.NE.ZS         | Unemployment, total (% of total labor force) (national estimate)                                                 |             8|   17.39130|
| SL.UEM.TOTL.ZS            | Unemployment, total (% of total labor force) (modeled ILO estimate)                                              |            21|   45.65217|
| SM.POP.NETM               | Net migration                                                                                                    |            37|   80.43478|
| SM.POP.REFG               | Refugee population by country or territory of asylum                                                             |            20|   43.47826|
| SM.POP.REFG.OR            | Refugee population by country or territory of origin                                                             |            20|   43.47826|
| SM.POP.TOTL               | International migrant stock, total                                                                               |            36|   78.26087|
| SM.POP.TOTL.ZS            | International migrant stock (% of population)                                                                    |            40|   86.95652|
| GC.AST.TOTL.CN            | Net acquisition of financial assets (current LCU)                                                                |            36|   78.26087|
| GC.AST.TOTL.GD.ZS         | Net acquisition of financial assets (% of GDP)                                                                   |            36|   78.26087|
| GC.DOD.TOTL.CN            | Central government debt, total (current LCU)                                                                     |            36|   78.26087|
| GC.DOD.TOTL.GD.ZS         | Central government debt, total (% of GDP)                                                                        |            36|   78.26087|
| GC.LBL.TOTL.CN            | Net incurrence of liabilities, total (current LCU)                                                               |            36|   78.26087|
| GC.LBL.TOTL.GD.ZS         | Net incurrence of liabilities, total (% of GDP)                                                                  |            36|   78.26087|
| GC.NFN.TOTL.CN            | Net investment in nonfinancial assets (current LCU)                                                              |            16|   34.78261|
| GC.NFN.TOTL.GD.ZS         | Net investment in nonfinancial assets (% of GDP)                                                                 |            16|   34.78261|
| GC.NLD.TOTL.CN            | Net lending (+) / net borrowing (-) (current LCU)                                                                |            16|   34.78261|
| GC.NLD.TOTL.GD.ZS         | Net lending (+) / net borrowing (-) (% of GDP)                                                                   |            16|   34.78261|
| GC.REV.GOTR.CN            | Grants and other revenue (current LCU)                                                                           |            12|   26.08696|
| GC.REV.GOTR.ZS            | Grants and other revenue (% of revenue)                                                                          |            12|   26.08696|
| GC.REV.SOCL.CN            | Social contributions (current LCU)                                                                               |            12|   26.08696|
| GC.REV.SOCL.ZS            | Social contributions (% of revenue)                                                                              |            12|   26.08696|
| GC.REV.XGRT.CN            | Revenue, excluding grants (current LCU)                                                                          |            12|   26.08696|
| GC.REV.XGRT.GD.ZS         | Revenue, excluding grants (% of GDP)                                                                             |            12|   26.08696|
| GC.TAX.EXPT.CN            | Taxes on exports (current LCU)                                                                                   |            41|   89.13043|
| GC.TAX.EXPT.ZS            | Taxes on exports (% of tax revenue)                                                                              |            42|   91.30435|
| GC.TAX.GSRV.CN            | Taxes on goods and services (current LCU)                                                                        |            22|   47.82609|
| GC.TAX.GSRV.RV.ZS         | Taxes on goods and services (% of revenue)                                                                       |            23|   50.00000|
| GC.TAX.GSRV.VA.ZS         | Taxes on goods and services (% value added of industry and services)                                             |            22|   47.82609|
| GC.TAX.IMPT.CN            | Customs and other import duties (current LCU)                                                                    |            24|   52.17391|
| GC.TAX.IMPT.ZS            | Customs and other import duties (% of tax revenue)                                                               |            25|   54.34783|
| GC.TAX.INTT.CN            | Taxes on international trade (current LCU)                                                                       |            22|   47.82609|
| GC.TAX.INTT.RV.ZS         | Taxes on international trade (% of revenue)                                                                      |            23|   50.00000|
| GC.TAX.OTHR.CN            | Other taxes (current LCU)                                                                                        |            22|   47.82609|
| GC.TAX.OTHR.RV.ZS         | Other taxes (% of revenue)                                                                                       |            23|   50.00000|
| GC.TAX.TOTL.CN            | Tax revenue (current LCU)                                                                                        |            12|   26.08696|
| GC.TAX.TOTL.GD.ZS         | Tax revenue (% of GDP)                                                                                           |            12|   26.08696|
| GC.TAX.YPKG.CN            | Taxes on income, profits and capital gains (current LCU)                                                         |            22|   47.82609|
| GC.TAX.YPKG.RV.ZS         | Taxes on income, profits and capital gains (% of revenue)                                                        |            23|   50.00000|
| GC.TAX.YPKG.ZS            | Taxes on income, profits and capital gains (% of total taxes)                                                    |            23|   50.00000|
| GC.XPN.COMP.CN            | Compensation of employees (current LCU)                                                                          |            12|   26.08696|
| GC.XPN.COMP.ZS            | Compensation of employees (% of expense)                                                                         |            12|   26.08696|
| GC.XPN.GSRV.CN            | Goods and services expense (current LCU)                                                                         |            12|   26.08696|
| GC.XPN.GSRV.ZS            | Goods and services expense (% of expense)                                                                        |            12|   26.08696|
| GC.XPN.INTP.CN            | Interest payments (current LCU)                                                                                  |            12|   26.08696|
| GC.XPN.INTP.RV.ZS         | Interest payments (% of revenue)                                                                                 |            12|   26.08696|
| GC.XPN.INTP.ZS            | Interest payments (% of expense)                                                                                 |            12|   26.08696|
| GC.XPN.OTHR.CN            | Other expense (current LCU)                                                                                      |            31|   67.39130|
| GC.XPN.OTHR.ZS            | Other expense (% of expense)                                                                                     |            31|   67.39130|
| GC.XPN.TOTL.CN            | Expense (current LCU)                                                                                            |            12|   26.08696|
| GC.XPN.TOTL.GD.ZS         | Expense (% of GDP)                                                                                               |            12|   26.08696|
| GC.XPN.TRFT.CN            | Subsidies and other transfers (current LCU)                                                                      |            21|   45.65217|
| GC.XPN.TRFT.ZS            | Subsidies and other transfers (% of expense)                                                                     |            21|   45.65217|
| IQ.CPA.BREG.XQ            | CPIA business regulatory environment rating (1=low to 6=high)                                                    |            46|  100.00000|
| IQ.CPA.DEBT.XQ            | CPIA debt policy rating (1=low to 6=high)                                                                        |            46|  100.00000|
| IQ.CPA.ECON.XQ            | CPIA economic management cluster average (1=low to 6=high)                                                       |            46|  100.00000|
| IQ.CPA.ENVR.XQ            | CPIA policy and institutions for environmental sustainability rating (1=low to 6=high)                           |            46|  100.00000|
| IQ.CPA.FINQ.XQ            | CPIA quality of budgetary and financial management rating (1=low to 6=high)                                      |            46|  100.00000|
| IQ.CPA.FINS.XQ            | CPIA financial sector rating (1=low to 6=high)                                                                   |            46|  100.00000|
| IQ.CPA.FISP.XQ            | CPIA fiscal policy rating (1=low to 6=high)                                                                      |            46|  100.00000|
| IQ.CPA.GNDR.XQ            | CPIA gender equality rating (1=low to 6=high)                                                                    |            46|  100.00000|
| IQ.CPA.HRES.XQ            | CPIA building human resources rating (1=low to 6=high)                                                           |            46|  100.00000|
| IQ.CPA.IRAI.XQ            | IDA resource allocation index (1=low to 6=high)                                                                  |            46|  100.00000|
| IQ.CPA.MACR.XQ            | CPIA macroeconomic management rating (1=low to 6=high)                                                           |            46|  100.00000|
| IQ.CPA.PADM.XQ            | CPIA quality of public administration rating (1=low to 6=high)                                                   |            46|  100.00000|
| IQ.CPA.PRES.XQ            | CPIA equity of public resource use rating (1=low to 6=high)                                                      |            46|  100.00000|
| IQ.CPA.PROP.XQ            | CPIA property rights and rule-based governance rating (1=low to 6=high)                                          |            46|  100.00000|
| IQ.CPA.PROT.XQ            | CPIA social protection rating (1=low to 6=high)                                                                  |            46|  100.00000|
| IQ.CPA.PUBS.XQ            | CPIA public sector management and institutions cluster average (1=low to 6=high)                                 |            46|  100.00000|
| IQ.CPA.REVN.XQ            | CPIA efficiency of revenue mobilization rating (1=low to 6=high)                                                 |            46|  100.00000|
| IQ.CPA.SOCI.XQ            | CPIA policies for social inclusion/equity cluster average (1=low to 6=high)                                      |            46|  100.00000|
| IQ.CPA.STRC.XQ            | CPIA structural policies cluster average (1=low to 6=high)                                                       |            46|  100.00000|
| IQ.CPA.TRAD.XQ            | CPIA trade rating (1=low to 6=high)                                                                              |            46|  100.00000|
| IQ.CPA.TRAN.XQ            | CPIA transparency, accountability, and corruption in the public sector rating (1=low to 6=high)                  |            46|  100.00000|
| IQ.SCI.MTHD               | Methodology assessment of statistical capacity (scale 0 - 100)                                                   |            34|   73.91304|
| IQ.SCI.OVRL               | Overall level of statistical capacity (scale 0 - 100)                                                            |            34|   73.91304|
| IQ.SCI.PRDC               | Periodicity and timeliness assessment of statistical capacity (scale 0 - 100)                                    |            34|   73.91304|
| IQ.SCI.SRCE               | Source data assessment of statistical capacity (scale 0 - 100)                                                   |            34|   73.91304|
| MS.MIL.MPRT.KD            | Arms imports (SIPRI trend indicator values)                                                                      |             0|    0.00000|
| MS.MIL.TOTL.P1            | Armed forces personnel, total                                                                                    |            18|   39.13043|
| MS.MIL.TOTL.TF.ZS         | Armed forces personnel (% of total labor force)                                                                  |            20|   43.47826|
| MS.MIL.XPND.CN            | Military expenditure (current LCU)                                                                               |            18|   39.13043|
| MS.MIL.XPND.GD.ZS         | Military expenditure (% of GDP)                                                                                  |            18|   39.13043|
| MS.MIL.XPND.ZS            | Military expenditure (% of central government expenditure)                                                       |            20|   43.47826|
| MS.MIL.XPRT.KD            | Arms exports (SIPRI trend indicator values)                                                                      |             7|   15.21739|
| VC.BTL.DETH               | Battle-related deaths (number of people)                                                                         |            46|  100.00000|
| VC.IDP.TOTL.HE            | Internally displaced persons (number, high estimate)                                                             |            39|   84.78261|
| VC.IHR.PSRC.P5            | Intentional homicides (per 100,000 people)                                                                       |            41|   89.13043|

On conserve les variables avec moins de 30% de valeurs manquantes, ce qui nous donne :

``` r
library(knitr)
Poverty_NA<-Poverty_NA[Poverty_NA$`% de NA`<=30,]
kable(Poverty_NA,caption="Variables restantes (NA<30%)")
```

|     | Code                 | Nom                                                                |  Nombre de NA|   % de NA|
|-----|:---------------------|:-------------------------------------------------------------------|-------------:|---------:|
| 95  | SL.UEM.TOTL.FE.NE.ZS | Unemployment, female (% of female labor force) (national estimate) |             9|  19.56522|
| 97  | SL.UEM.TOTL.MA.NE.ZS | Unemployment, male (% of male labor force) (national estimate)     |             9|  19.56522|
| 99  | SL.UEM.TOTL.NE.ZS    | Unemployment, total (% of total labor force) (national estimate)   |             8|  17.39130|
| 116 | GC.REV.GOTR.CN       | Grants and other revenue (current LCU)                             |            12|  26.08696|
| 117 | GC.REV.GOTR.ZS       | Grants and other revenue (% of revenue)                            |            12|  26.08696|
| 118 | GC.REV.SOCL.CN       | Social contributions (current LCU)                                 |            12|  26.08696|
| 119 | GC.REV.SOCL.ZS       | Social contributions (% of revenue)                                |            12|  26.08696|
| 120 | GC.REV.XGRT.CN       | Revenue, excluding grants (current LCU)                            |            12|  26.08696|
| 121 | GC.REV.XGRT.GD.ZS    | Revenue, excluding grants (% of GDP)                               |            12|  26.08696|
| 133 | GC.TAX.TOTL.CN       | Tax revenue (current LCU)                                          |            12|  26.08696|
| 134 | GC.TAX.TOTL.GD.ZS    | Tax revenue (% of GDP)                                             |            12|  26.08696|
| 138 | GC.XPN.COMP.CN       | Compensation of employees (current LCU)                            |            12|  26.08696|
| 139 | GC.XPN.COMP.ZS       | Compensation of employees (% of expense)                           |            12|  26.08696|
| 140 | GC.XPN.GSRV.CN       | Goods and services expense (current LCU)                           |            12|  26.08696|
| 141 | GC.XPN.GSRV.ZS       | Goods and services expense (% of expense)                          |            12|  26.08696|
| 142 | GC.XPN.INTP.CN       | Interest payments (current LCU)                                    |            12|  26.08696|
| 143 | GC.XPN.INTP.RV.ZS    | Interest payments (% of revenue)                                   |            12|  26.08696|
| 144 | GC.XPN.INTP.ZS       | Interest payments (% of expense)                                   |            12|  26.08696|
| 147 | GC.XPN.TOTL.CN       | Expense (current LCU)                                              |            12|  26.08696|
| 148 | GC.XPN.TOTL.GD.ZS    | Expense (% of GDP)                                                 |            12|  26.08696|
| 176 | MS.MIL.MPRT.KD       | Arms imports (SIPRI trend indicator values)                        |             0|   0.00000|
| 182 | MS.MIL.XPRT.KD       | Arms exports (SIPRI trend indicator values)                        |             7|  15.21739|

Il ne reste alors que les 22 variables indiquées ci-dessus.

On va donc réaliser l'analyse pour ces 14 variables. Pour cela il faut d'abord lier les deux datasets en un même dataset.

``` r
library(dplyr)
## Création d'un dataset avec uniquement les données pauvreté et l'année
poverty_data<-WorldBank[,4,drop=FALSE]
  for (i in 1:nrow(Poverty_NA)) ## indicateur conservé
  {
      code=Poverty_NA[i,1]
      poverty_data<-cbind(poverty_data,WorldBank[toString(code)])
}
mortalityPoverty<-inner_join(mortalityBr,poverty_data,by=c("Periode"="year"))
```

On peut alors calculer les coefficients de corrélation pour chaque variable.

On commence par SL.UEM.TOTL.FE.NE.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$SL.UEM.TOTL.FE.NE.ZS,use = "complete.obs")
```

    ## [1] -0.1325128

SL.UEM.TOTL.MA.NE.ZS :

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$SL.UEM.TOTL.MA.NE.ZS,use = "complete.obs")
```

    ## [1] -0.1152989

SL.UEM.TOTL.NE.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$SL.UEM.TOTL.NE.ZS,use = "complete.obs")
```

    ## [1] -0.1216883

GC.REV.GOTR.CN

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.REV.GOTR.CN,use = "complete.obs")
```

    ## [1] -0.1231238

GC.REV.GOTR.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.REV.GOTR.ZS,use = "complete.obs")
```

    ## [1] 0.1519632

GC.REV.SOCL.CN

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.REV.SOCL.CN,use = "complete.obs")
```

    ## [1] -0.1350938

GC.REV.SOCL.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.REV.SOCL.ZS,use = "complete.obs")
```

    ## [1] 0.02006514

GC.REV.XGRT.CN

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.REV.XGRT.CN,use = "complete.obs")
```

    ## [1] -0.1550303

GC.REV.XGRT.GD.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.REV.XGRT.GD.ZS,use = "complete.obs")
```

    ## [1] 0.2114836

GC.TAX.TOTL.CN

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.TAX.TOTL.CN,use = "complete.obs")
```

    ## [1] -0.1763968

GC.TAX.TOTL.GD.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.TAX.TOTL.GD.ZS,use = "complete.obs")
```

    ## [1] 0.2040418

GC.XPN.COMP.CN :

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.COMP.CN,use = "complete.obs")
```

    ## [1] -0.178087

GC.XPN.COMP.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.COMP.ZS,use = "complete.obs")
```

    ## [1] -0.154289

GC.XPN.GSRV.CN

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.GSRV.CN,use = "complete.obs")
```

    ## [1] -0.218706

GC.XPN.GSRV.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.GSRV.ZS,use = "complete.obs")
```

    ## [1] -0.0321723

GC.XPN.INTP.CN

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.INTP.CN,use = "complete.obs")
```

    ## [1] -0.1480564

GC.XPN.INTP.RV.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.INTP.RV.ZS,use = "complete.obs")
```

    ## [1] 0.1937705

GC.XPN.INTP.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.INTP.ZS,use = "complete.obs")
```

    ## [1] 0.2014358

GC.XPN.TOTL.CN

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.TOTL.CN,use = "complete.obs")
```

    ## [1] -0.1535387

GC.XPN.TOTL.GD.ZS

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$GC.XPN.TOTL.GD.ZS,use = "complete.obs")
```

    ## [1] 0.2081211

MS.MIL.MPRT.KD

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$MS.MIL.MPRT.KD,use = "complete.obs")
```

    ## [1] -0.0449081

MS.MIL.XPRT.KD

``` r
cor(mortalityPoverty$TauxMortalite,mortalityPoverty$MS.MIL.XPRT.KD,use = "complete.obs")
```

    ## [1] 0.08860194

ON observe des coefficients de corélation très faible pour chacune des variables, il n'est donc pas pertinent de les conserver dans le modèle.
