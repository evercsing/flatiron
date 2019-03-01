# flatiron API Project

# Python program to find current  
# weather details of any city 
# using openweathermap api 
  
# import required modules 
import requests, json 
import matplotlib.pyplot as plt
  
# Enter your API key here 
api_key = "c4440a0676f79455da1890baf316cde9"
  
# base_url variable to store url 
base_url = "http://api.openweathermap.org/data/2.5/forecast?"

print("Hoboken: 5099133 \nPalisades Park: 5102369")  


# full API URL
#http://api.openweathermap.org/data/2.5/forecast?id=5098135&appid=c4440a0676f79455da1890baf316cde9

# Give city name 
#city_id = input("Enter city ID : ") 
  
# complete_url variable to store 
# complete url address 
complete_url = base_url + "appid=" + api_key + "&id=5102369"
  
# get method of requests module 
# return response object 
response = requests.get(complete_url) 

results = response.json()

results = results['list']

#print(len(results['list']))

file = open('temp.txt', 'w')
file.write('')
file = open('dt_txt.txt', 'w')
file.write('')

count = 0

# save in a filer
for data in results:
    file1 = open('temp.txt', 'a')
    file1.write(str(data['main']['temp']) +'\n')
    #print(data['main']['temp'])
    
    file2 = open('dt_txt.txt', 'a')
    file2.write(str(data['dt_txt']) +'\n')
    #print(data['dt_txt'])
    
    count += 1
    
    if count == 30:
        break
    
temp_list = []

# Open file
temp_file = open('temp.txt', 'r')
    
# Count lines
# We can skip ruits_file.readlines()
for line in temp_file:
    temp_list.append(float(line.rstrip('\n')))

converted_temp_list = []

for temp in temp_list:
    converted_temp_list.append((temp - 273.15) * 9/5 + 32)

dt_txt_list = []

# Open file
dt_txt_file = open('dt_txt.txt', 'r')
  
for line in dt_txt_file:
    dt_txt_list.append(line.rstrip('\n'))

#temp_file.close()    

    
# Initialize data points
x = dt_txt_list
y = converted_temp_list 

# Generate line graph
plt.plot(x,y)

# Add title
plt.title('Weather history in Palisades Park, NJ') 

# Add labels
plt.xlabel('Time')
plt.ylabel('Temp')

# Specify x and y axes range
plt.xlim(xmin=0, xmax=len(converted_temp_list))
plt.ylim(ymin=min(converted_temp_list), ymax=max(converted_temp_list))


# Add grid
plt.grid(False)

# Display line graph
plt.show()
print()
print('Temp')
print(converted_temp_list)
print()
print('Time')
print(dt_txt_list)
