import os
import filecmp
from dateutil.relativedelta import *
from datetime import date



file = "P1DataB.csv"
student_records = []
def getData(file):
	infile = open(file, 'r')
	lines = infile.readlines()[1:]
	infile.close()
	list_dics = []

	for line in lines:
		rec = line.split(",")
		fname = rec[0]
		lname = rec[1]
		email = rec[2]
		year = rec[3]
		dob = rec[4]

		dic = {}
		dic["First"] = fname
		dic["Last"] = lname
		dic["Email"] = email
		dic["Class"] = year
		dic["DOB"] = dob
		list_dics.append(dic)

	return list_dics
#Input: file name
#Ouput: return a list of dictionary objects where
#the keys are from the first row in the data. and the values are each of the other rows

	pass

def mySort(data,col):
# Sort based on key/column
#Input: list of dictionaries and col (key) to sort on
#Output: Return the first item in the sorted list as a string of just: firstName lastName
	sort_data = sorted(data, key = lambda k : k[col])

	first_line = sort_data[0]
	f_name = first_line["First"]
	l_name = first_line["Last"]

	return f_name + " " + l_name

	pass


def classSizes(data):
# Create a histogram
# Input: list of dictionaries
# Output: Return a list of tuples sorted by the number of students in that class in
# descending order
# [('Senior', 26), ('Junior', 25), ('Freshman', 21), ('Sophomore', 18)]
	class_list = []

	seniors = 0
	juniors = 0
	sophomores = 0
	freshmen = 0

	for stu in data:
		if stu["Class"] == "Senior":
			seniors += 1
		elif stu["Class"] == "Junior":
			juniors += 1
		elif stu["Class"] == "Sophomore":
			sophomores += 1
		elif stu["Class"] == "Freshman":
			freshmen += 1

	class_list.append(("Senior", seniors))
	class_list.append(("Junior", juniors))
	class_list.append(("Sophomore", sophomores))
	class_list.append(("Freshman", freshmen))

	sorted_list = sorted(class_list, key = lambda tup : tup[1], reverse = True)
	return sorted_list

	pass


def findMonth(a):
# Find the most common birth month form this data
# Input: list of dictionaries
# Output: Return the month (1-12) that had the most births in the data
	months = {}

	for stu in a:
		birth = stu["DOB"]
		birth = birth.split("/")
		birth_month = int(birth[0])
		if birth_month in months:
			months[birth_month] += 1
		else:
			months[birth_month] = 1

	sorted_months = sorted(months.items(), key = lambda val : val[1], reverse = True)
	most_pop_month = sorted_months[0][0]

	return most_pop_month


	pass

def mySortPrint(a,col,fileName):
#Similar to mySort, but instead of returning single
#Student, the sorted data is saved to a csv file.
# as fist,last,email
#Input: list of dictionaries, col (key) to sort by and output file name
#Output: No return value, but the file is written
	file = open(fileName, "w")
	sorted_a = sorted(a, key = lambda k: k[col])

	for stu in sorted_a:
		fname = stu["First"]
		lname = stu["Last"]
		email = stu["Email"]
		file.write(fname + "," + lname + "," + email + "\n")

	file.close()

	pass

def findAge(a):
# def findAge(a):
# Input: list of dictionaries
# Output: Return the average age of the students and round that age to the nearest
# integer.  You will need to work with the DOB and the current date to find the current
# age in years.
	sum_ages = 0

	year = 2018
	month = 10
	day = 20

	for stu in a:
		dob = stu["DOB"]
		dob = dob.split("/")
		ye = int(dob[2])
		mo = int(dob[0])
		d = int(dob[1])
		age = year - ye
		if mo >= month and d > day:
			age -= 1
		sum_ages += age

	students = len(a)
	avg_age = round(sum_ages/students)
	return avg_age

	pass


################################################################
## DO NOT MODIFY ANY CODE BELOW THIS
################################################################

## We have provided simple test() function used in main() to print what each function returns vs. what it's supposed to return.
def test(got, expected, pts):
  score = 0;
  if got == expected:
    score = pts
    print(" OK ", end=" ")
  else:
    print (" XX ", end=" ")
  print("Got: ",got, "Expected: ",expected)
  return score


# Provided main() calls the above functions with interesting inputs, using test() to check if each result is correct or not.
def main():
	total = 0
	print("Read in Test data and store as a list of dictionaries")
	data = getData('P1DataA.csv')
	data2 = getData('P1DataB.csv')
	total += test(type(data),type([]),50)

	print()
	print("First student sorted by First name:")
	total += test(mySort(data,'First'),'Abbot Le',25)
	total += test(mySort(data2,'First'),'Adam Rocha',25)

	print("First student sorted by Last name:")
	total += test(mySort(data,'Last'),'Elijah Adams',25)
	total += test(mySort(data2,'Last'),'Elijah Adams',25)

	print("First student sorted by Email:")
	total += test(mySort(data,'Email'),'Hope Craft',25)
	total += test(mySort(data2,'Email'),'Orli Humphrey',25)

	print("\nEach grade ordered by size:")
	total += test(classSizes(data),[('Junior', 28), ('Senior', 27), ('Freshman', 23), ('Sophomore', 22)],25)
	total += test(classSizes(data2),[('Senior', 26), ('Junior', 25), ('Freshman', 21), ('Sophomore', 18)],25)

	print("\nThe most common month of the year to be born is:")
	total += test(findMonth(data),3,15)
	total += test(findMonth(data2),3,15)

	print("\nSuccessful sort and print to file:")
	mySortPrint(data,'Last','results.csv')
	if os.path.exists('results.csv'):
		total += test(filecmp.cmp('outfile.csv', 'results.csv'),True,20)

	print("\nTest of extra credit: Calcuate average age")
	total += test(findAge(data), 40, 5)
	total += test(findAge(data2), 42, 5)

	print("Your final score is " + str(total))

# Standard boilerplate to call the main() function that tests all your code
if __name__ == '__main__':
    main()
