# STA-141A-project

## please change the directory of file while used:
### 1 load the session data:
session <- lapply(1:18, function(i) {
  readRDS(paste("Your Directory\\session", i, '.rds', sep = ''))
})
### 2 load the time_coefficient data
#### Note: Time coefficient data is AR1 for all trails of each session
Time_coef<-read.csv("Your Directory\\all_sessions_time_coefficients.csv")
time_coeff_data<-Time_coef
session_ids <- unique(time_coeff_data$Session)
time_coeff_data$Feedback_time=time_coeff_data$Time_Coefficient_Feedback_1+time_coeff_data$Time_Coefficient_Feedback_neg1

### 3 getting access to the 
