# STA-141A-project

## Please change the directory of file while used:
### 1. load the session data:
session <- lapply(1:18, function(i) {
  readRDS(paste("Your Directory\\session", i, '.rds', sep = ''))
})
### 2. load the time_coefficient data
#### Note: Time coefficient data is AR1 for all trails of each session
Time_coef<-read.csv("Your Directory\\all_sessions_time_coefficients.csv")
time_coeff_data<-Time_coef
session_ids <- unique(time_coeff_data$Session)
time_coeff_data$Feedback_time=time_coeff_data$Time_Coefficient_Feedback_1+time_coeff_data$Time_Coefficient_Feedback_neg1

##  Getting access to the parameter_importance...csv(optional)
#### Description: here is all score of importance score generated by the 5-f cross cv and 10 number of different values to try each parameter(select importance>1) 
train_control <- trainControl(
  method = "cv",          # Cross-validation
  number = 5,            # 5-fold cross-validation
  verboseIter = TRUE,     
  savePredictions = "final" 
)
#### Train model with hyperparameter tuning
rf_model <- train(
  feedback_type ~ contrast_left + contrast_right + total_neurons + total_spikes, 
  data = Model_df,
  method = "rf", # Random Forest, but you can use other methods
  trControl = train_control,
  tuneLength = 10 # Number of different values to try for each hyperparameter
)
### You could get top highest importance parameters, optimal number of trees(400),mtry(18) for your optimal training model :)







