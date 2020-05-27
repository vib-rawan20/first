import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

#Reading the file
data=pd.read_csv(path)

#Creating a new variable to store the value counts
loan_status=data['Loan_Status'].value_counts()
plt.plot(kind='bar',x=loan_status.index,y=loan_status)
#Plotting bar plot

# Step 2
#Plotting an unstacked bar plot
property_and_loan=data.groupby(['Loan_Status','Property_Area'])

plt.xlabel('Property Area')
plt.ylabel('Loan Status')
plt.xticks(rotation=45)
# Step 3
#Plotting a stacked bar plot
education=data.groupby(['Loan_Status','Education']).size().unstack()
education.plot()
plt.xlabel('Education Status')
plt.ylabel('Loan Status')
plt.xticks(rotation=45)

# Step 4 
#Subsetting the dataframe based on 'Education' column
graduate=data[data['Education']=='Graduate']

#Subsetting the dataframe based on 'Education' column
not_graduate=data[data['Education']=='Not Graduate']


#Plotting density plot for 'Graduate'
graduate['LoanAmount'].plot(kind='density',label='Graduate')

#Plotting density plot for 'Graduate'
not_graduate['LoanAmount'].plot(kind='density',label='Not Graduate')


#For automatic legend display


# Step 5
#Setting up the subplots
fig, (ax_1,ax_2,ax_3)=plt.subplots(3,1)

#Plotting scatter plot
ax_1.scatter(data['ApplicantIncome'],data['LoanAmount'])

#Setting the subplot axis title
plt.title('Applicant Income')

#Plotting scatter plot
ax_2.scatter(data['CoapplicantIncome'],data['LoanAmount'])

#Setting the subplot axis title
plt.title('Coapplicant Income')

#Creating a new column 'TotalIncome'
data['TotalIncome']=data['ApplicantIncome']+data['CoapplicantIncome']

#Plotting scatter plot
ax_3.scatter(data['TotalIncome'],data['LoanAmount'])


#Setting the subplot axis title
plt.title('Total Income')
