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
for (i in 1:nrow(Poverty)) ## Poverty = dataset des indicateurs de pauvretés et leur signification
  {
      ### Calcul de NA
      code=Poverty[i,3]
      nbNA=sum(is.na(WorldBank[[toString(code)]]))
      Poverty_NA[i,]<-list(toString(code),toString(Poverty[i,4]),nbNA,nbNA/138*100)
}
##Affichage du résultat
Poverty_NA
```

    ##                          Code
    ## 1              SI.DST.02ND.20
    ## 2              SI.DST.03RD.20
    ## 3              SI.DST.04TH.20
    ## 4              SI.DST.05TH.20
    ## 5              SI.DST.10TH.10
    ## 6              SI.DST.FRST.10
    ## 7              SI.DST.FRST.20
    ## 8                 SI.POV.2DAY
    ## 9                 SI.POV.DDAY
    ## 10                SI.POV.GAP2
    ## 11                SI.POV.GAPS
    ## 12                SI.POV.GINI
    ## 13                SI.POV.NAHC
    ## 14          SL.AGR.EMPL.FE.ZS
    ## 15          SL.AGR.EMPL.MA.ZS
    ## 16             SL.AGR.EMPL.ZS
    ## 17    SL.EMP.1524.SP.FE.NE.ZS
    ## 18       SL.EMP.1524.SP.FE.ZS
    ## 19    SL.EMP.1524.SP.MA.NE.ZS
    ## 20       SL.EMP.1524.SP.MA.ZS
    ## 21       SL.EMP.1524.SP.NE.ZS
    ## 22          SL.EMP.1524.SP.ZS
    ## 23          SL.EMP.INSV.FE.ZS
    ## 24          SL.EMP.MPYR.FE.ZS
    ## 25          SL.EMP.MPYR.MA.ZS
    ## 26             SL.EMP.MPYR.ZS
    ## 27          SL.EMP.SELF.FE.ZS
    ## 28          SL.EMP.SELF.MA.ZS
    ## 29             SL.EMP.SELF.ZS
    ## 30    SL.EMP.TOTL.SP.FE.NE.ZS
    ## 31       SL.EMP.TOTL.SP.FE.ZS
    ## 32    SL.EMP.TOTL.SP.MA.NE.ZS
    ## 33       SL.EMP.TOTL.SP.MA.ZS
    ## 34       SL.EMP.TOTL.SP.NE.ZS
    ## 35          SL.EMP.TOTL.SP.ZS
    ## 36          SL.EMP.VULN.FE.ZS
    ## 37          SL.EMP.VULN.MA.ZS
    ## 38             SL.EMP.VULN.ZS
    ## 39          SL.EMP.WORK.FE.ZS
    ## 40          SL.EMP.WORK.MA.ZS
    ## 41             SL.EMP.WORK.ZS
    ## 42          SL.FAM.WORK.FE.ZS
    ## 43          SL.FAM.WORK.MA.ZS
    ## 44             SL.FAM.WORK.ZS
    ## 45          SL.GDP.PCAP.EM.KD
    ## 46          SL.IND.EMPL.FE.ZS
    ## 47          SL.IND.EMPL.MA.ZS
    ## 48             SL.IND.EMPL.ZS
    ## 49          SL.SRV.EMPL.FE.ZS
    ## 50          SL.SRV.EMPL.MA.ZS
    ## 51             SL.SRV.EMPL.ZS
    ## 52  SL.TLF.ACTI.1524.FE.NE.ZS
    ## 53     SL.TLF.ACTI.1524.FE.ZS
    ## 54  SL.TLF.ACTI.1524.MA.NE.ZS
    ## 55     SL.TLF.ACTI.1524.MA.ZS
    ## 56     SL.TLF.ACTI.1524.NE.ZS
    ## 57        SL.TLF.ACTI.1524.ZS
    ## 58          SL.TLF.ADVN.FE.ZS
    ## 59          SL.TLF.ADVN.MA.ZS
    ## 60             SL.TLF.ADVN.ZS
    ## 61          SL.TLF.BASC.FE.ZS
    ## 62          SL.TLF.BASC.MA.ZS
    ## 63             SL.TLF.BASC.ZS
    ## 64       SL.TLF.CACT.FE.NE.ZS
    ## 65          SL.TLF.CACT.FE.ZS
    ## 66       SL.TLF.CACT.FM.NE.ZS
    ## 67          SL.TLF.CACT.FM.ZS
    ## 68       SL.TLF.CACT.MA.NE.ZS
    ## 69          SL.TLF.CACT.MA.ZS
    ## 70          SL.TLF.CACT.NE.ZS
    ## 71             SL.TLF.CACT.ZS
    ## 72          SL.TLF.INTM.FE.ZS
    ## 73          SL.TLF.INTM.MA.ZS
    ## 74             SL.TLF.INTM.ZS
    ## 75          SL.TLF.TOTL.FE.ZS
    ## 76             SL.TLF.TOTL.IN
    ## 77       SL.UEM.1524.FE.NE.ZS
    ## 78          SL.UEM.1524.FE.ZS
    ## 79       SL.UEM.1524.MA.NE.ZS
    ## 80          SL.UEM.1524.MA.ZS
    ## 81          SL.UEM.1524.NE.ZS
    ## 82             SL.UEM.1524.ZS
    ## 83          SL.UEM.ADVN.FE.ZS
    ## 84          SL.UEM.ADVN.MA.ZS
    ## 85             SL.UEM.ADVN.ZS
    ## 86          SL.UEM.BASC.FE.ZS
    ## 87          SL.UEM.BASC.MA.ZS
    ## 88             SL.UEM.BASC.ZS
    ## 89          SL.UEM.INTM.FE.ZS
    ## 90          SL.UEM.INTM.MA.ZS
    ## 91             SL.UEM.INTM.ZS
    ## 92          SL.UEM.NEET.FE.ZS
    ## 93          SL.UEM.NEET.MA.ZS
    ## 94             SL.UEM.NEET.ZS
    ## 95       SL.UEM.TOTL.FE.NE.ZS
    ## 96          SL.UEM.TOTL.FE.ZS
    ## 97       SL.UEM.TOTL.MA.NE.ZS
    ## 98          SL.UEM.TOTL.MA.ZS
    ## 99          SL.UEM.TOTL.NE.ZS
    ## 100            SL.UEM.TOTL.ZS
    ## 101               SM.POP.NETM
    ## 102               SM.POP.REFG
    ## 103            SM.POP.REFG.OR
    ## 104               SM.POP.TOTL
    ## 105            SM.POP.TOTL.ZS
    ## 106            GC.AST.TOTL.CN
    ## 107         GC.AST.TOTL.GD.ZS
    ## 108            GC.DOD.TOTL.CN
    ## 109         GC.DOD.TOTL.GD.ZS
    ## 110            GC.LBL.TOTL.CN
    ## 111         GC.LBL.TOTL.GD.ZS
    ## 112            GC.NFN.TOTL.CN
    ## 113         GC.NFN.TOTL.GD.ZS
    ## 114            GC.NLD.TOTL.CN
    ## 115         GC.NLD.TOTL.GD.ZS
    ## 116            GC.REV.GOTR.CN
    ## 117            GC.REV.GOTR.ZS
    ## 118            GC.REV.SOCL.CN
    ## 119            GC.REV.SOCL.ZS
    ## 120            GC.REV.XGRT.CN
    ## 121         GC.REV.XGRT.GD.ZS
    ## 122            GC.TAX.EXPT.CN
    ## 123            GC.TAX.EXPT.ZS
    ## 124            GC.TAX.GSRV.CN
    ## 125         GC.TAX.GSRV.RV.ZS
    ## 126         GC.TAX.GSRV.VA.ZS
    ## 127            GC.TAX.IMPT.CN
    ## 128            GC.TAX.IMPT.ZS
    ## 129            GC.TAX.INTT.CN
    ## 130         GC.TAX.INTT.RV.ZS
    ## 131            GC.TAX.OTHR.CN
    ## 132         GC.TAX.OTHR.RV.ZS
    ## 133            GC.TAX.TOTL.CN
    ## 134         GC.TAX.TOTL.GD.ZS
    ## 135            GC.TAX.YPKG.CN
    ## 136         GC.TAX.YPKG.RV.ZS
    ## 137            GC.TAX.YPKG.ZS
    ## 138            GC.XPN.COMP.CN
    ## 139            GC.XPN.COMP.ZS
    ## 140            GC.XPN.GSRV.CN
    ## 141            GC.XPN.GSRV.ZS
    ## 142            GC.XPN.INTP.CN
    ## 143         GC.XPN.INTP.RV.ZS
    ## 144            GC.XPN.INTP.ZS
    ## 145            GC.XPN.OTHR.CN
    ## 146            GC.XPN.OTHR.ZS
    ## 147            GC.XPN.TOTL.CN
    ## 148         GC.XPN.TOTL.GD.ZS
    ## 149            GC.XPN.TRFT.CN
    ## 150            GC.XPN.TRFT.ZS
    ## 151            IQ.CPA.BREG.XQ
    ## 152            IQ.CPA.DEBT.XQ
    ## 153            IQ.CPA.ECON.XQ
    ## 154            IQ.CPA.ENVR.XQ
    ## 155            IQ.CPA.FINQ.XQ
    ## 156            IQ.CPA.FINS.XQ
    ## 157            IQ.CPA.FISP.XQ
    ## 158            IQ.CPA.GNDR.XQ
    ## 159            IQ.CPA.HRES.XQ
    ## 160            IQ.CPA.IRAI.XQ
    ## 161            IQ.CPA.MACR.XQ
    ## 162            IQ.CPA.PADM.XQ
    ## 163            IQ.CPA.PRES.XQ
    ## 164            IQ.CPA.PROP.XQ
    ## 165            IQ.CPA.PROT.XQ
    ## 166            IQ.CPA.PUBS.XQ
    ## 167            IQ.CPA.REVN.XQ
    ## 168            IQ.CPA.SOCI.XQ
    ## 169            IQ.CPA.STRC.XQ
    ## 170            IQ.CPA.TRAD.XQ
    ## 171            IQ.CPA.TRAN.XQ
    ## 172               IQ.SCI.MTHD
    ## 173               IQ.SCI.OVRL
    ## 174               IQ.SCI.PRDC
    ## 175               IQ.SCI.SRCE
    ## 176            MS.MIL.MPRT.KD
    ## 177            MS.MIL.TOTL.P1
    ## 178         MS.MIL.TOTL.TF.ZS
    ## 179            MS.MIL.XPND.CN
    ## 180         MS.MIL.XPND.GD.ZS
    ## 181            MS.MIL.XPND.ZS
    ## 182            MS.MIL.XPRT.KD
    ## 183               VC.BTL.DETH
    ## 184            VC.IDP.TOTL.HE
    ## 185            VC.IHR.PSRC.P5
    ##                                                                                                                  Nom
    ## 1                                                                                    Income share held by second 20%
    ## 2                                                                                     Income share held by third 20%
    ## 3                                                                                    Income share held by fourth 20%
    ## 4                                                                                   Income share held by highest 20%
    ## 5                                                                                   Income share held by highest 10%
    ## 6                                                                                    Income share held by lowest 10%
    ## 7                                                                                    Income share held by lowest 20%
    ## 8                                                Poverty headcount ratio at $3.10 a day (2011 PPP) (% of population)
    ## 9                                                Poverty headcount ratio at $1.90 a day (2011 PPP) (% of population)
    ## 10                                                                         Poverty gap at $3.10 a day (2011 PPP) (%)
    ## 11                                                                         Poverty gap at $1.90 a day (2011 PPP) (%)
    ## 12                                                                                  GINI index (World Bank estimate)
    ## 13                                               Poverty headcount ratio at national poverty lines (% of population)
    ## 14                                                        Employment in agriculture, female (% of female employment)
    ## 15                                                            Employment in agriculture, male (% of male employment)
    ## 16                                                                 Employment in agriculture (% of total employment)
    ## 17                                        Employment to population ratio, ages 15-24, female (%) (national estimate)
    ## 18                                     Employment to population ratio, ages 15-24, female (%) (modeled ILO estimate)
    ## 19                                          Employment to population ratio, ages 15-24, male (%) (national estimate)
    ## 20                                       Employment to population ratio, ages 15-24, male (%) (modeled ILO estimate)
    ## 21                                         Employment to population ratio, ages 15-24, total (%) (national estimate)
    ## 22                                      Employment to population ratio, ages 15-24, total (%) (modeled ILO estimate)
    ## 23           Share of women in wage employment in the nonagricultural sector (% of total nonagricultural employment)
    ## 24                                                                        Employers, female (% of female employment)
    ## 25                                                                            Employers, male (% of male employment)
    ## 26                                                                          Employers, total (% of total employment)
    ## 27                                                                    Self-employed, female (% of female employment)
    ## 28                                                                        Self-employed, male (% of male employment)
    ## 29                                                                      Self-employed, total (% of total employment)
    ## 30                                               Employment to population ratio, 15+, female (%) (national estimate)
    ## 31                                            Employment to population ratio, 15+, female (%) (modeled ILO estimate)
    ## 32                                                 Employment to population ratio, 15+, male (%) (national estimate)
    ## 33                                              Employment to population ratio, 15+, male (%) (modeled ILO estimate)
    ## 34                                                Employment to population ratio, 15+, total (%) (national estimate)
    ## 35                                             Employment to population ratio, 15+, total (%) (modeled ILO estimate)
    ## 36                                                            Vulnerable employment, female (% of female employment)
    ## 37                                                                Vulnerable employment, male (% of male employment)
    ## 38                                                              Vulnerable employment, total (% of total employment)
    ## 39                                                        Wage and salaried workers, female (% of female employment)
    ## 40                                                            Wage and salaried workers, male (% of male employment)
    ## 41                                                          Wage and salaried workers, total (% of total employment)
    ## 42                                                      Contributing family workers, female (% of female employment)
    ## 43                                                          Contributing family workers, male (% of male employment)
    ## 44                                                        Contributing family workers, total (% of total employment)
    ## 45                                                                     GDP per person employed (constant 2011 PPP $)
    ## 46                                                           Employment in industry, female (% of female employment)
    ## 47                                                               Employment in industry, male (% of male employment)
    ## 48                                                                    Employment in industry (% of total employment)
    ## 49                                                           Employment in services, female (% of female employment)
    ## 50                                                               Employment in services, male (% of male employment)
    ## 51                                                                    Employment in services (% of total employment)
    ## 52                                     Labor force participation rate for ages 15-24, female (%) (national estimate)
    ## 53                                  Labor force participation rate for ages 15-24, female (%) (modeled ILO estimate)
    ## 54                                       Labor force participation rate for ages 15-24, male (%) (national estimate)
    ## 55                                    Labor force participation rate for ages 15-24, male (%) (modeled ILO estimate)
    ## 56                                      Labor force participation rate for ages 15-24, total (%) (national estimate)
    ## 57                                   Labor force participation rate for ages 15-24, total (%) (modeled ILO estimate)
    ## 58          Labor force with advanced education, female (% of female working-age population with advanced education)
    ## 59              Labor force with advanced education, male (% of male working-age population with advanced education)
    ## 60                   Labor force with advanced education (% of total working-age population with advanced education)
    ## 61                Labor force with basic education, female (% of female working-age population with basic education)
    ## 62                    Labor force with basic education, male (% of male working-age population with basic education)
    ## 63                         Labor force with basic education (% of total working-age population with basic education)
    ## 64                      Labor force participation rate, female (% of female population ages 15+) (national estimate)
    ## 65                   Labor force participation rate, female (% of female population ages 15+) (modeled ILO estimate)
    ## 66                                    Ratio of female to male labor force participation rate (%) (national estimate)
    ## 67                                 Ratio of female to male labor force participation rate (%) (modeled ILO estimate)
    ## 68                          Labor force participation rate, male (% of male population ages 15+) (national estimate)
    ## 69                       Labor force participation rate, male (% of male population ages 15+) (modeled ILO estimate)
    ## 70                        Labor force participation rate, total (% of total population ages 15+) (national estimate)
    ## 71                     Labor force participation rate, total (% of total population ages 15+) (modeled ILO estimate)
    ## 72  Labor force with intermediate education, female (% of female working-age population with intermediate education)
    ## 73      Labor force with intermediate education, male (% of male working-age population with intermediate education)
    ## 74           Labor force with intermediate education (% of total working-age population with intermediate education)
    ## 75                                                                      Labor force, female (% of total labor force)
    ## 76                                                                                                Labor force, total
    ## 77                               Unemployment, youth female (% of female labor force ages 15-24) (national estimate)
    ## 78                            Unemployment, youth female (% of female labor force ages 15-24) (modeled ILO estimate)
    ## 79                                   Unemployment, youth male (% of male labor force ages 15-24) (national estimate)
    ## 80                                Unemployment, youth male (% of male labor force ages 15-24) (modeled ILO estimate)
    ## 81                                 Unemployment, youth total (% of total labor force ages 15-24) (national estimate)
    ## 82                              Unemployment, youth total (% of total labor force ages 15-24) (modeled ILO estimate)
    ## 83                    Unemployment with advanced education, female (% of female labor force with advanced education)
    ## 84                        Unemployment with advanced education, male (% of male labor force with advanced education)
    ## 85                             Unemployment with advanced education (% of total labor force with advanced education)
    ## 86                          Unemployment with basic education, female (% of female labor force with basic education)
    ## 87                              Unemployment with basic education, male (% of male labor force with basic education)
    ## 88                                   Unemployment with basic education (% of total labor force with basic education)
    ## 89            Unemployment with intermediate education, female (% of female labor force with intermediate education)
    ## 90                Unemployment with intermediate education, male (% of male labor force with intermediate education)
    ## 91                     Unemployment with intermediate education (% of total labor force with intermediate education)
    ## 92                    Share of youth not in education, employment or training, female (% of female youth population)
    ## 93                        Share of youth not in education, employment or training, male (% of male youth population)
    ## 94                            Share of youth not in education, employment or training, total (% of youth population)
    ## 95                                                Unemployment, female (% of female labor force) (national estimate)
    ## 96                                             Unemployment, female (% of female labor force) (modeled ILO estimate)
    ## 97                                                    Unemployment, male (% of male labor force) (national estimate)
    ## 98                                                 Unemployment, male (% of male labor force) (modeled ILO estimate)
    ## 99                                                  Unemployment, total (% of total labor force) (national estimate)
    ## 100                                              Unemployment, total (% of total labor force) (modeled ILO estimate)
    ## 101                                                                                                    Net migration
    ## 102                                                             Refugee population by country or territory of asylum
    ## 103                                                             Refugee population by country or territory of origin
    ## 104                                                                               International migrant stock, total
    ## 105                                                                    International migrant stock (% of population)
    ## 106                                                                Net acquisition of financial assets (current LCU)
    ## 107                                                                   Net acquisition of financial assets (% of GDP)
    ## 108                                                                     Central government debt, total (current LCU)
    ## 109                                                                        Central government debt, total (% of GDP)
    ## 110                                                               Net incurrence of liabilities, total (current LCU)
    ## 111                                                                  Net incurrence of liabilities, total (% of GDP)
    ## 112                                                              Net investment in nonfinancial assets (current LCU)
    ## 113                                                                 Net investment in nonfinancial assets (% of GDP)
    ## 114                                                                Net lending (+) / net borrowing (-) (current LCU)
    ## 115                                                                   Net lending (+) / net borrowing (-) (% of GDP)
    ## 116                                                                           Grants and other revenue (current LCU)
    ## 117                                                                          Grants and other revenue (% of revenue)
    ## 118                                                                               Social contributions (current LCU)
    ## 119                                                                              Social contributions (% of revenue)
    ## 120                                                                          Revenue, excluding grants (current LCU)
    ## 121                                                                             Revenue, excluding grants (% of GDP)
    ## 122                                                                                   Taxes on exports (current LCU)
    ## 123                                                                              Taxes on exports (% of tax revenue)
    ## 124                                                                        Taxes on goods and services (current LCU)
    ## 125                                                                       Taxes on goods and services (% of revenue)
    ## 126                                             Taxes on goods and services (% value added of industry and services)
    ## 127                                                                    Customs and other import duties (current LCU)
    ## 128                                                               Customs and other import duties (% of tax revenue)
    ## 129                                                                       Taxes on international trade (current LCU)
    ## 130                                                                      Taxes on international trade (% of revenue)
    ## 131                                                                                        Other taxes (current LCU)
    ## 132                                                                                       Other taxes (% of revenue)
    ## 133                                                                                        Tax revenue (current LCU)
    ## 134                                                                                           Tax revenue (% of GDP)
    ## 135                                                         Taxes on income, profits and capital gains (current LCU)
    ## 136                                                        Taxes on income, profits and capital gains (% of revenue)
    ## 137                                                    Taxes on income, profits and capital gains (% of total taxes)
    ## 138                                                                          Compensation of employees (current LCU)
    ## 139                                                                         Compensation of employees (% of expense)
    ## 140                                                                         Goods and services expense (current LCU)
    ## 141                                                                        Goods and services expense (% of expense)
    ## 142                                                                                  Interest payments (current LCU)
    ## 143                                                                                 Interest payments (% of revenue)
    ## 144                                                                                 Interest payments (% of expense)
    ## 145                                                                                      Other expense (current LCU)
    ## 146                                                                                     Other expense (% of expense)
    ## 147                                                                                            Expense (current LCU)
    ## 148                                                                                               Expense (% of GDP)
    ## 149                                                                      Subsidies and other transfers (current LCU)
    ## 150                                                                     Subsidies and other transfers (% of expense)
    ## 151                                                    CPIA business regulatory environment rating (1=low to 6=high)
    ## 152                                                                        CPIA debt policy rating (1=low to 6=high)
    ## 153                                                       CPIA economic management cluster average (1=low to 6=high)
    ## 154                           CPIA policy and institutions for environmental sustainability rating (1=low to 6=high)
    ## 155                                      CPIA quality of budgetary and financial management rating (1=low to 6=high)
    ## 156                                                                   CPIA financial sector rating (1=low to 6=high)
    ## 157                                                                      CPIA fiscal policy rating (1=low to 6=high)
    ## 158                                                                    CPIA gender equality rating (1=low to 6=high)
    ## 159                                                           CPIA building human resources rating (1=low to 6=high)
    ## 160                                                                  IDA resource allocation index (1=low to 6=high)
    ## 161                                                           CPIA macroeconomic management rating (1=low to 6=high)
    ## 162                                                   CPIA quality of public administration rating (1=low to 6=high)
    ## 163                                                      CPIA equity of public resource use rating (1=low to 6=high)
    ## 164                                          CPIA property rights and rule-based governance rating (1=low to 6=high)
    ## 165                                                                  CPIA social protection rating (1=low to 6=high)
    ## 166                                 CPIA public sector management and institutions cluster average (1=low to 6=high)
    ## 167                                                 CPIA efficiency of revenue mobilization rating (1=low to 6=high)
    ## 168                                      CPIA policies for social inclusion/equity cluster average (1=low to 6=high)
    ## 169                                                       CPIA structural policies cluster average (1=low to 6=high)
    ## 170                                                                              CPIA trade rating (1=low to 6=high)
    ## 171                  CPIA transparency, accountability, and corruption in the public sector rating (1=low to 6=high)
    ## 172                                                   Methodology assessment of statistical capacity (scale 0 - 100)
    ## 173                                                            Overall level of statistical capacity (scale 0 - 100)
    ## 174                                    Periodicity and timeliness assessment of statistical capacity (scale 0 - 100)
    ## 175                                                   Source data assessment of statistical capacity (scale 0 - 100)
    ## 176                                                                      Arms imports (SIPRI trend indicator values)
    ## 177                                                                                    Armed forces personnel, total
    ## 178                                                                  Armed forces personnel (% of total labor force)
    ## 179                                                                               Military expenditure (current LCU)
    ## 180                                                                                  Military expenditure (% of GDP)
    ## 181                                                       Military expenditure (% of central government expenditure)
    ## 182                                                                      Arms exports (SIPRI trend indicator values)
    ## 183                                                                         Battle-related deaths (number of people)
    ## 184                                                             Internally displaced persons (number, high estimate)
    ## 185                                                                       Intentional homicides (per 100,000 people)
    ##     Nombre de NA   % de NA
    ## 1             61  44.20290
    ## 2             61  44.20290
    ## 3             61  44.20290
    ## 4             61  44.20290
    ## 5             61  44.20290
    ## 6             61  44.20290
    ## 7             61  44.20290
    ## 8             61  44.20290
    ## 9             61  44.20290
    ## 10            61  44.20290
    ## 11            61  44.20290
    ## 12            61  44.20290
    ## 13           107  77.53623
    ## 14            36  26.08696
    ## 15            36  26.08696
    ## 16            35  25.36232
    ## 17           100  72.46377
    ## 18            63  45.65217
    ## 19           100  72.46377
    ## 20            63  45.65217
    ## 21            99  71.73913
    ## 22            63  45.65217
    ## 23            74  53.62319
    ## 24            74  53.62319
    ## 25            74  53.62319
    ## 26            73  52.89855
    ## 27           134  97.10145
    ## 28           134  97.10145
    ## 29           134  97.10145
    ## 30            81  58.69565
    ## 31            63  45.65217
    ## 32            81  58.69565
    ## 33            63  45.65217
    ## 34            79  57.24638
    ## 35            63  45.65217
    ## 36            74  53.62319
    ## 37            74  53.62319
    ## 38            73  52.89855
    ## 39            74  53.62319
    ## 40            74  53.62319
    ## 41            73  52.89855
    ## 42            74  53.62319
    ## 43            74  53.62319
    ## 44            73  52.89855
    ## 45            63  45.65217
    ## 46            36  26.08696
    ## 47            36  26.08696
    ## 48            34  24.63768
    ## 49            36  26.08696
    ## 50            36  26.08696
    ## 51            34  24.63768
    ## 52            72  52.17391
    ## 53            60  43.47826
    ## 54            72  52.17391
    ## 55            60  43.47826
    ## 56            71  51.44928
    ## 57            60  43.47826
    ## 58           121  87.68116
    ## 59           121  87.68116
    ## 60           120  86.95652
    ## 61           121  87.68116
    ## 62           121  87.68116
    ## 63           120  86.95652
    ## 64            42  30.43478
    ## 65            60  43.47826
    ## 66            42  30.43478
    ## 67            60  43.47826
    ## 68            42  30.43478
    ## 69            60  43.47826
    ## 70            40  28.98551
    ## 71            60  43.47826
    ## 72           121  87.68116
    ## 73           121  87.68116
    ## 74           120  86.95652
    ## 75            60  43.47826
    ## 76            60  43.47826
    ## 77            71  51.44928
    ## 78            63  45.65217
    ## 79            71  51.44928
    ## 80            63  45.65217
    ## 81            70  50.72464
    ## 82            63  45.65217
    ## 83           110  79.71014
    ## 84           110  79.71014
    ## 85           109  78.98551
    ## 86           110  79.71014
    ## 87           110  79.71014
    ## 88           109  78.98551
    ## 89           110  79.71014
    ## 90           110  79.71014
    ## 91           109  78.98551
    ## 92           119  86.23188
    ## 93           119  86.23188
    ## 94           119  86.23188
    ## 95            28  20.28986
    ## 96            63  45.65217
    ## 97            28  20.28986
    ## 98            63  45.65217
    ## 99            25  18.11594
    ## 100           63  45.65217
    ## 101          111  80.43478
    ## 102           60  43.47826
    ## 103           61  44.20290
    ## 104          108  78.26087
    ## 105          120  86.95652
    ## 106          118  85.50725
    ## 107          118  85.50725
    ## 108          111  80.43478
    ## 109          111  80.43478
    ## 110          118  85.50725
    ## 111          118  85.50725
    ## 112           66  47.82609
    ## 113           66  47.82609
    ## 114           66  47.82609
    ## 115           66  47.82609
    ## 116           49  35.50725
    ## 117           49  35.50725
    ## 118           49  35.50725
    ## 119           49  35.50725
    ## 120           49  35.50725
    ## 121           49  35.50725
    ## 122           90  65.21739
    ## 123           91  65.94203
    ## 124           63  45.65217
    ## 125           64  46.37681
    ## 126           63  45.65217
    ## 127           62  44.92754
    ## 128           63  45.65217
    ## 129           59  42.75362
    ## 130           60  43.47826
    ## 131           60  43.47826
    ## 132           61  44.20290
    ## 133           49  35.50725
    ## 134           49  35.50725
    ## 135           59  42.75362
    ## 136           60  43.47826
    ## 137           60  43.47826
    ## 138           51  36.95652
    ## 139           51  36.95652
    ## 140           50  36.23188
    ## 141           50  36.23188
    ## 142           50  36.23188
    ## 143           50  36.23188
    ## 144           50  36.23188
    ## 145           85  61.59420
    ## 146           85  61.59420
    ## 147           50  36.23188
    ## 148           50  36.23188
    ## 149           72  52.17391
    ## 150           72  52.17391
    ## 151          138 100.00000
    ## 152          138 100.00000
    ## 153          138 100.00000
    ## 154          138 100.00000
    ## 155          138 100.00000
    ## 156          138 100.00000
    ## 157          138 100.00000
    ## 158          138 100.00000
    ## 159          138 100.00000
    ## 160          138 100.00000
    ## 161          138 100.00000
    ## 162          138 100.00000
    ## 163          138 100.00000
    ## 164          138 100.00000
    ## 165          138 100.00000
    ## 166          138 100.00000
    ## 167          138 100.00000
    ## 168          138 100.00000
    ## 169          138 100.00000
    ## 170          138 100.00000
    ## 171          138 100.00000
    ## 172          102  73.91304
    ## 173          102  73.91304
    ## 174          102  73.91304
    ## 175          102  73.91304
    ## 176           34  24.63768
    ## 177           56  40.57971
    ## 178           62  44.92754
    ## 179           54  39.13043
    ## 180           54  39.13043
    ## 181           73  52.89855
    ## 182           97  70.28986
    ## 183          111  80.43478
    ## 184          111  80.43478
    ## 185           93  67.39130

On conserve les variables avec moins de 30% de valeurs manquantes, ce qui nous donne :

``` r
(Poverty_NA<-Poverty_NA[Poverty_NA$`% de NA`<=30,])
```

    ##                     Code
    ## 14     SL.AGR.EMPL.FE.ZS
    ## 15     SL.AGR.EMPL.MA.ZS
    ## 16        SL.AGR.EMPL.ZS
    ## 46     SL.IND.EMPL.FE.ZS
    ## 47     SL.IND.EMPL.MA.ZS
    ## 48        SL.IND.EMPL.ZS
    ## 49     SL.SRV.EMPL.FE.ZS
    ## 50     SL.SRV.EMPL.MA.ZS
    ## 51        SL.SRV.EMPL.ZS
    ## 70     SL.TLF.CACT.NE.ZS
    ## 95  SL.UEM.TOTL.FE.NE.ZS
    ## 97  SL.UEM.TOTL.MA.NE.ZS
    ## 99     SL.UEM.TOTL.NE.ZS
    ## 176       MS.MIL.MPRT.KD
    ##                                                                                            Nom
    ## 14                                  Employment in agriculture, female (% of female employment)
    ## 15                                      Employment in agriculture, male (% of male employment)
    ## 16                                           Employment in agriculture (% of total employment)
    ## 46                                     Employment in industry, female (% of female employment)
    ## 47                                         Employment in industry, male (% of male employment)
    ## 48                                              Employment in industry (% of total employment)
    ## 49                                     Employment in services, female (% of female employment)
    ## 50                                         Employment in services, male (% of male employment)
    ## 51                                              Employment in services (% of total employment)
    ## 70  Labor force participation rate, total (% of total population ages 15+) (national estimate)
    ## 95                          Unemployment, female (% of female labor force) (national estimate)
    ## 97                              Unemployment, male (% of male labor force) (national estimate)
    ## 99                            Unemployment, total (% of total labor force) (national estimate)
    ## 176                                                Arms imports (SIPRI trend indicator values)
    ##     Nombre de NA  % de NA
    ## 14            36 26.08696
    ## 15            36 26.08696
    ## 16            35 25.36232
    ## 46            36 26.08696
    ## 47            36 26.08696
    ## 48            34 24.63768
    ## 49            36 26.08696
    ## 50            36 26.08696
    ## 51            34 24.63768
    ## 70            40 28.98551
    ## 95            28 20.28986
    ## 97            28 20.28986
    ## 99            25 18.11594
    ## 176           34 24.63768

Il ne reste alors que les 14 variables indiquées ci-dessus.
