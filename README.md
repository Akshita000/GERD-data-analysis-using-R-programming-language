# GERD-data-analysis-using-R-programming-language
R programming language project to identify and assess the risk factors of gastroesophageal reflux disease (GERD).
# Performing univariate analysis to identify the association of individual risk factors with GERD.
# Risk Factors: H.pylori, Gender, Age, Lifestyle habits (smoking, alcohol intake, and NSAID usage), FSSG score, Hiatus hernia, and BMI.
library(readxl)
data <- read_excel("path of the file.xlsx")  
result <- fisher.test(data)
print(result)

library(readxl)
file_path <- "Age_distribution_metadata.xlsx"
data <- read_excel("Age distribution metadata.xlsx")
str(data)
contingency_table <- table(data$Variable1, data$Variable2)
result <- chisq.test(contingency_table)
print(result)

# Performing multivariate regression analysis to identify the association between risk factors as a whole on GERD.
library(readxl)
data <- read_excel("Multivariate regression analysis.xlsx")
str(data)  # Check the structure of the data
summary(data)  # Summarize the data
model <- glm(Disease~ HP + Age + Gender + NSAID + Smoker + Alcohol + FSSG + Hernia + BMI, data = data, family = binomial)
odds_ratios <- exp(coef(model))
conf_intervals <- exp(confint.default(model))
results <- data.frame(Odds_Ratio = odds_ratios, 
                      Lower_CI = conf_intervals[, 1], 
                      Upper_CI = conf_intervals[, 2])
print(results)






