marks=[]
max = 0
n=int(input("enter no. of students : "))
def accept():
        for i in range(n):
                 num=int(input("enter marks of the students : "))
                 marks.append(num)
def selection_sort():
        for i in range(n-1):
            for j in range(i+1,n):
                if marks[i]>marks[j]:
                    marks[i],marks[j]=marks[j],marks[i]
        for i in range(n):
            print(marks[i])
        print("this was selection sort")    
def bubble_sort():
        for i in range(n-1):
            for j in range(0, n-i-1):
                if marks[j] > marks[j+1]:
                    marks[j], marks[j+1] = marks[j+1], marks[j]
        for i in range(n):
            print(marks[i])
        print("this was bubble sort")    
def top_fivemarks(marks):
    print("top five scores")
    count=len(marks)
    if(count<5):
        start,stop=count-1,-1
    else:
        start,stop=count-1,count-6
    for i in range(start,stop,-1):
        print(marks[i], end=" ")
accept()
selection_sort()
bubble_sort()
top_fivemarks(marks)