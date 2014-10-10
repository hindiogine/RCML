RCML Presentation 
=================

Initial settings, libraries and cleanup.

```r
rm(list = ls())
library(foreign)
library(likert)
library(xtable)
setwd("~/Google Drive/MASC-351/")
```


Cultural Awareness Beliefs Inventory
------------------------------------

First we load the CABI data.  CABI = cultural awareness beliefs inventory.  20 multiple choice survey questions with values: "Strongly agree" (1), "Agree" (2), "Disagree" (3), and "Strongly disagree" (4). These were asked at the end of each semester.

```r
CABI.data <- read.spss("CABIPOST.sav", to.data.frame = TRUE)
```

```
## Error: unable to open file: 'No such file or directory'
```

```r
CABI.data <- CABI.data[-c(62, 77), ]
```

```
## Error: object 'CABI.data' not found
```

```r
CABI.data <- subset(CABI.data, select = -SRN)
```

```
## Error: object 'CABI.data' not found
```


Format the data and create the Likert object.

```r
CABI.tmp <- lapply(CABI.data, factor, levels = 1:4, labels = c("Strongly disagree", 
    "Disagree", "Agree", "Strongly agree"))
```

```
## Error: object 'CABI.data' not found
```

```r
CABI <- data.frame(CABI.tmp)
```

```
## Error: object 'CABI.tmp' not found
```

```r
questions <- c("Q1", "Q2", "Q3", "Q4", "Q5", "Q6", "Q7", "Q8", "Q9", "Q10", 
    "Q11", "Q12", "Q13", "Q14", "Q15", "Q16", "Q17", "Q18", "Q19", "Q20")
names(CABI) <- questions
```

```
## Error: object 'CABI' not found
```

```r
CABI.likert <- likert(CABI)
```

```
## Error: object 'CABI' not found
```



```r
plot(CABI.likert) + labs(title = "CABI")
```

```
## Error: object 'CABI.likert' not found
```


List of 20 multiple choice CABI questions:
<TABLE border=0>
<TR><TD>Q1</TD><TD>I believe all middle school students are treated equitably regardless of their race, culture, disability, gender or social economic status.</TD></TR>
<TR><TD>Q2</TD><TD>I believe all families are supportive of teachers’ work to effectively teach all middle school students.</TD></TR>
<TR><TD>Q3</TD><TD>I believe teachers have strong support for academic excellence from the surrounding school community (civic, church, business).</TD></TR>
<TR><TD>Q4</TD><TD>I believe some students do not want to learn</TD></TR>
<TR><TD>Q5</TD><TD>I believe that poor teaching is the main factor that causes the gap in math achievement between White students and students of color.</TD></TR>
<TR><TD>Q6</TD><TD>I believe I have the knowledge and skills I need to be a culturally responsive math teacher.</TD></TR>
<TR><TD>Q7</TD><TD>I believe I can implement cooperative learning effectively as an integral part of my math teaching strategies.</TD></TR>
<TR><TD>Q8</TD><TD>I believe African American students have more behavior problems than other students.</TD></TR>
<TR><TD>Q9</TD><TD>I believe most diverse students are not as eager to excel in math in comparison to their White peers.</TD></TR>
<TR><TD>Q10</TD><TD>I believe many middle school teachers engage in biased behavior toward students of color in the classroom.</TD></TR>
<TR><TD>Q11</TD><TD>I believe students who live in poverty are more difficult to teach.</TD></TR>
<TR><TD>Q12</TD><TD>I believe most diverse students do not bring as many strengths to the classroom as their White peers.</TD></TR>
<TR><TD>Q13</TD><TD>I believe it is important to identify with the racial groups of the students I serve.</TD></TR>
<TR><TD>Q14</TD><TD>I believe I am comfortable with people who exhibit values or beliefs different from my own.</TD></TR>
<TR><TD>Q15</TD><TD>I believe the cultural views of a diverse school community should be an integral component of my lesson planning.</TD></TR>
<TR><TD>Q16</TD><TD>I believe in asking families of diverse cultures how they wish to be identified (e.g., African American, Bi-racial, Mexican).</TD></TR>
<TR><TD>Q17</TD><TD>I believe that in a society with as many racial groups as the United States, I would accept the use of ethnic jokes or phrases by students.</TD></TR>
<TR><TD>Q18</TD><TD>I believe math classroom activities should enhance English Language Learners’ understanding.</TD></TR>
<TR><TD>Q19</TD><TD>I believe I am able to effectively manage students from all racial groups.</TD></TR>
<TR><TD>Q20</TD><TD>I believe I would prefer to work with students and parents whose cultures are similar to mine.</TD></TR>
</TABLE>

We display the Likert data as plots according to EFA groupings: "Teacher efficacy" (TE), "Teacher beliefs" (TB), "Cultural beliefs" (CB), and "Racial beliefs" (RB).

```r
attach(CABI)
```

```
## Error: object 'CABI' not found
```

```r
CABI.TE <- data.frame(Q6, Q7, Q8, Q9, Q12, Q13, Q14, Q15, Q16, Q17, Q18, Q19)
```

```
## Error: object 'Q6' not found
```

```r
CABI.TE.likert <- likert(CABI.TE)
```

```
## Error: object 'CABI.TE' not found
```

```r

CABI.TB <- data.frame(Q2, Q3, Q4, Q5)
```

```
## Error: object 'Q2' not found
```

```r
CABI.TB.likert <- likert(CABI.TB)
```

```
## Error: object 'CABI.TB' not found
```

```r

CABI.CB <- data.frame(Q11, Q18, Q20)
```

```
## Error: object 'Q11' not found
```

```r
CABI.CB.likert <- likert(CABI.CB)
```

```
## Error: object 'CABI.CB' not found
```

```r

CABI.RB <- data.frame(Q1, Q19)
```

```
## Error: object 'Q1' not found
```

```r
CABI.RB.likert <- likert(CABI.RB)
```

```
## Error: object 'CABI.RB' not found
```

```r
detach(CABI)
```

```
## Error: invalid 'name' argument
```



```r
plot(CABI.TE.likert) + labs(title = "CABI - Teacher efficacy")
```

```
## Error: object 'CABI.TE.likert' not found
```

```r
plot(CABI.TB.likert) + labs(title = "CABI - Teacher beliefs")
```

```
## Error: object 'CABI.TB.likert' not found
```

```r
plot(CABI.CB.likert) + labs(title = "CABI - Cultural beliefs")
```

```
## Error: object 'CABI.CB.likert' not found
```

```r
plot(CABI.RB.likert) + labs(title = "CABI - Racial beliefs")
```

```
## Error: object 'CABI.RB.likert' not found
```


Diversity Preparedness Response Inventory
-----------------------------------------
First we import and process the SPSS data set first:

```r
DPRI.data <- read.spss("diversity1.sav", to.data.frame = TRUE)
```

```
## Error: unable to open file: 'No such file or directory'
```

```r
DPRI.data <- subset(DPRI.data, select = -c(Researchcode, DIAdinner, KTADdinner))
```

```
## Error: object 'DPRI.data' not found
```


There are 32 questions, which are too many to display conveniently on a single plot. Hence we split it into the KTAD (knowledge for teaching algebra for diversity) and DIA (diversity awareness).  The following table shows the activities with the label used in the graphs to identify them

<TABLE border=0>
<TR><TD> DIA-1   </TD><TD> DIAReadingPoylatextbook</TD></TR>
<TR><TD> DIA-2   </TD><TD> DIAreadingsquestionsfromRespondingtoDiversitytbk</TD></TR>
<TR><TD> DIA-3   </TD><TD> DIApresentationsdiscussionsaboutculturediversity</TD></TR>
<TR><TD> DIA-4   </TD><TD> DIADinnerActivitySolvingProblem </TD></TR>   
<TR><TD> KTAD-1  </TD><TD> KTADReadingPoylatextbook </TD></TR>
<TR><TD> KTAD-2  </TD><TD> KTADreadingsquestionsfromRespondingtoDiversitytbk </TD></TR>
<TR><TD> KTAD-3  </TD><TD> KTADpresentationsdiscussionsaboutculturediversity </TD></TR>
<TR><TD> KTAD-4  </TD><TD> KTADDinnerActivitySolvingProblem </TD></TR>               
<TR><TD> DIA-5   </TD><TD> DIADiversityReadingsLadsonBillingsMilner </TD></TR>         
<TR><TD> DIA-6   </TD><TD> DIADrChanceLewis                   </TD></TR>
<TR><TD> DIA-7   </TD><TD> DIAHumanGraphChallenge           </TD></TR>         
<TR><TD> DIA-8   </TD><TD> DIAMeettheMiddleGradeStudentsinSL</TD></TR>                
<TR><TD> DIA-9   </TD><TD> DIATutoringtheMiddleGradeStudentsinSL</TD></TR>     
<TR><TD> DIA-10  </TD><TD> DIAAnalysisLanguageMovesfromyourtutoring   </TD></TR>    
<TR><TD> DIA-11  </TD><TD> DIADrKathrynMcKenzie                     </TD></TR>     
<TR><TD> DIA-12  </TD><TD> DIATheCreditCardFoodDriveChallenge       </TD></TR> 
<TR><TD> KTAD-5  </TD><TD> KTADDiversityReadingsLadsonBillingsMilner</TD></TR>      
<TR><TD> KTAD-6  </TD><TD> KTADDrChanceLewis                      </TD></TR>       
<TR><TD> KTAD-7  </TD><TD> KTADHumanGraphChallenge          </TD></TR> 
<TR><TD> KTAD-8  </TD><TD> KTADMeettheMiddleGradeStudentsinSL     </TD></TR>   
<TR><TD> KTAD-9  </TD><TD> KTADTutoringtheMiddleGradeStudentsinSL</TD></TR>           
<TR><TD> KTAD-10 </TD><TD> KTADAnalysisLanguageMovesfromyourtutoring</TD></TR> 
<TR><TD> KTAD-11 </TD><TD> KTADDrKathrynMcKenzie                  </TD></TR>  
<TR><TD> KTAD-12 </TD><TD> KTADTheCreditCardFoodDriveChallenge  </TD></TR>            
<TR><TD> DIA-13  </TD><TD> DIAProblemsolvinglessonPresentationinSL</TD></TR>        
<TR><TD> KTAD-14 </TD><TD> KTADProblemsolvinglessonPresentationinSL</TD></TR>        
<TR><TD> DIA-14  </TD><TD> DIADinnerProblemRespondingtostudentmisconceptions </TD></TR>
<TR><TD> DIA-15  </TD><TD> DIADinnerProblemPlanningalesson    </TD></TR>      
<TR><TD> DIA-16  </TD><TD> DIADinnerProblemRespondingtostudentquestions</TD></TR>
<TR><TD> KTAD-18 </TD><TD> KTADDinnerProblemRespondingtostudentmisconceptions</TD></TR>
<TR><TD> KTAD-19 </TD><TD> KTADinnerProblemPlanningalesson</TD></TR>  
<TR><TD> KTAD-20 </TD><TD> KTADDinnerProblemRespondingtostudentquestions</TD></TR>
</TABLE>

[NOTE: we state in this presentation that we do not show the SecLife data.  However, we have SL items in this data set.]

First we format the data and create the Likert object.

```r
DPRI.tmp <- lapply(DPRI.data, factor, levels = 1:4, labels = c("No change", 
    "Made me rethink", "Changed somewhat", "Changed a lot"))
```

```
## Error: object 'DPRI.data' not found
```

```r
DPRI <- data.frame(DPRI.tmp)
```

```
## Error: object 'DPRI.tmp' not found
```

```r
questions <- c("DIA.1", "DIA.2", "DIA.3", "DIA.4", "KTAD.1", "KTAD.2", "KTAD.3", 
    "KTAD.4", "DIA.5", "DIA.6", "DIA.7", "DIA.8", "DIA.9", "DIA.10", "DIA.11", 
    "DIA.12", "KTAD.5", "KTAD.6", "KTAD.7", "KTAD.8", "KTAD.9", "KTAD.10", "KTAD.11", 
    "KTAD.12", "DIA.13", "KTAD.14", "DIA.15", "DIA.16", "DIA.17", "KTAD.18", 
    "KTAD.19", "KTAD.20")
names(DPRI) <- questions
```

```
## Error: object 'DPRI' not found
```

```r
DPRI.likert <- likert(DPRI)
```

```
## Error: object 'DPRI' not found
```


The we split the DPRI data into ints DIA and TKAD components.

```r
attach(DPRI)
```

```
## Error: object 'DPRI' not found
```

```r
DPRI.DIA.tmp <- DPRI[, c(1, 2, 3, 4, 9, 10, 11, 12, 13, 14, 15, 16, 25, 27, 
    28, 29)]
```

```
## Error: object 'DPRI' not found
```

```r
DPRI.KTAD.tmp <- DPRI[, c(5, 6, 7, 8, 17, 18, 19, 20, 21, 22, 23, 24, 26, 30, 
    31, 32)]
```

```
## Error: object 'DPRI' not found
```

```r
detach(DPRI)
```

```
## Error: invalid 'name' argument
```

```r
DPRI.DIA <- data.frame(DPRI.DIA.tmp)
```

```
## Error: object 'DPRI.DIA.tmp' not found
```

```r
DPRI.KTAD <- data.frame(DPRI.KTAD.tmp)
```

```
## Error: object 'DPRI.KTAD.tmp' not found
```

```r
DPRI.DIA.likert <- likert(DPRI.DIA)
```

```
## Error: object 'DPRI.DIA' not found
```

```r
DPRI.KTAD.likert <- likert(DPRI.KTAD)
```

```
## Error: object 'DPRI.KTAD' not found
```



```r
plot(DPRI.DIA.likert, wrap = 18, center = 1.5) + labs(title = "DPRI - DIA")
```

```
## Error: object 'DPRI.DIA.likert' not found
```

```r
plot(DPRI.KTAD.likert, wrap = 18, center = 1.5) + labs(title = "DPRI - KTAD")
```

```
## Error: object 'DPRI.KTAD.likert' not found
```


Linear models of EFA factors
-------------------------------
The following table shows our predictor and outcome variables:
<table border=0>
<tr><td>Predictor variable</td><td>Outcome variable</td><td>p value</td><td>Effect size (R^2)</td></tr>
<tr><td>TEK</td><td>Math</td><td>0.007</td><td>0.167</td></tr>
<tr><td>TEK</td><td>Teaching efficacy</td><td>0.006</td><td>0.170</td></tr>
<tr><td>TEK</td><td>Teaching beliefs</td><td>0.001</td><td>0.224</td></tr>
<tr><td>TPSK</td><td>Teaching beliefs</td><td>0.027</td><td>0.125</td></tr>
</table>

We load the data used to calculate the models

```r
RCML.data <- read.spss("spssdataRCML.sav", to.data.frame = TRUE)
```

```
## Error: unable to open file: 'No such file or directory'
```


First we create the TPSK and TEK variables from the DPRI data.

```r
names(DPRI.data) <- questions
```

```
## Error: object 'DPRI.data' not found
```

```r
TPSK <- data.frame(TKAD.1 = DPRI.data$KTAD.1, TKAD.2 = DPRI.data$KTAD.2, TKAD.3 = DPRI.data$KTAD.3, 
    TKAD.4 = DPRI.data$KTAD.4)
```

```
## Error: object 'DPRI.data' not found
```

```r

TEK <- data.frame(KTAD.5 = DPRI.data$KTAD.5, KTAD.6 = DPRI.data$KTAD.6, KTAD.7 = DPRI.data$KTAD.7, 
    KTAD.10 = DPRI.data$KTAD.10, KTAD.11 = DPRI.data$KTAD.11, KTAD.12 = DPRI.data$KTAD.12)
```

```
## Error: object 'DPRI.data' not found
```


Then we retrieve the appropriate variables from the RCML data set.  In addition we remove the rows with zero values.

```r
attach(RCML.data)
```

```
Error: object 'RCML.data' not found
```

```r
RCML <- data.frame(TeachEff = F1c, TeachBelief = F2CA, Math = MKATE)
```

```
Error: object 'F1c' not found
```

```r
detach(RCML.data)
```

```
Error: invalid 'name' argument
```

```r
RCML$TPSK <- apply(TPSK, 1, mean)
```

```
Error: object 'TPSK' not found
```

```r
RCML$TEK <- apply(TEK, 1, mean)
```

```
Error: object 'TEK' not found
```

```r
RCML <- RCML[-c(6, 7, 13, 19, 21, 25, 29, 31), ]
```

```
Error: object 'RCML' not found
```

```r
print(RCML)
```

```
Error: object 'RCML' not found
```


First we consider these 6 factors independently and calculate their correlations.
[need to add "Cultural beliefs", "Racial beliefs", and "Teach"]


```r
corRCML <- cor(RCML)
```

```
Error: object 'RCML' not found
```

```r
print(corRCML)
```

```
Error: object 'corRCML' not found
```


```r
# library(Kmisc) kTable(corRCML)
```


Now that we have the predictor and outcome variables we can run the linear and quadratic models.

A. Math predicted by TEK (linear)

```r
Reg.1 <- lm(RCML$Math ~ RCML$TEK)
```

```
Error: object 'RCML' not found
```

```r
summary(Reg.1)
```

```
Error: object 'Reg.1' not found
```

And we plot it

```r
p.1 <- ggplot(RCML, aes(x = TEK, y = Math)) + geom_point() + stat_smooth(method = "lm", 
    formula = y ~ x, size = 1, se = FALSE)
```

```
## Error: object 'RCML' not found
```

```r
p.1
```

```
## Error: object 'p.1' not found
```


B: Teaching efficacy predicted by TEK

```r
Reg.2 <- lm(RCML$TeachEff ~ RCML$TEK)
```

```
Error: object 'RCML' not found
```

```r
summary(Reg.2)
```

```
Error: object 'Reg.2' not found
```

And we plot it

```r
p.2 <- ggplot(RCML, aes(x = TEK, y = TeachEff)) + geom_point() + stat_smooth(method = "lm", 
    formula = y ~ x, size = 1, se = FALSE)
```

```
## Error: object 'RCML' not found
```

```r
p.2
```

```
## Error: object 'p.2' not found
```


C. Teaching beliefs predicted by TEK

```r
Reg.3 <- lm(RCML$TeachBelief ~ RCML$TEK)
```

```
Error: object 'RCML' not found
```

```r
summary(Reg.3)
```

```
Error: object 'Reg.3' not found
```

And we plot it

```r
p.3 <- ggplot(RCML, aes(x = TEK, y = TeachBelief)) + geom_point() + stat_smooth(method = "lm", 
    formula = y ~ x, size = 1, se = FALSE)
```

```
## Error: object 'RCML' not found
```

```r
p.3
```

```
## Error: object 'p.3' not found
```


D. Teaching beliefs predicted by TPSK

```r
Reg.4 <- lm(RCML$TeachBelief ~ RCML$TPSK)
```

```
Error: object 'RCML' not found
```

```r
summary(Reg.4)
```

```
Error: object 'Reg.4' not found
```

And we plot it

```r
p.4 <- ggplot(RCML, aes(x = TPSK, y = TeachBelief)) + geom_point() + stat_smooth(method = "lm", 
    formula = y ~ x, size = 1, se = FALSE)
```

```
## Error: object 'RCML' not found
```

```r
p.4
```

```
## Error: object 'p.4' not found
```

