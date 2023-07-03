from tabulate import tabulate
import mysql.connector
con=mysql.connector.connect(host="localhost",user="root",password="root",database="SMS")

def select():
    res=con.cursor()
    sql="select * from Studentsmarksheet"
    res.execute(sql)
    result=res.fetchall()
    print("****************************************************************************************************")
    #print(result)
    print(tabulate(result,headers=["StdID","Stdname","Stdclass","Tamil","English","Maths","Science","Social","Total"]))
    print("****************************************************************************************************")
def insert(StdID,name,stdclass,tamil,english,maths,science,social,total):
    res=con.cursor()
    qry="insert into Studentsmarksheet(StdID,Stdname,Stdclass,Tamil,English,Maths,Science,Social,Total)values(%s,%s,%s,%s,%s,%s,%s,%s,%s)"
    user=(StdID,name,stdclass,tamil,english,maths,science,social,total)
    res.execute(qry,user)
    con.commit()
    print("********************************************************")
    print("Data insert successfully")
def delete(StdID):
    print("********************************************************")
    res=con.cursor()
    qry="delete from Studentsmarksheet where StdID=%s"
    user=(StdID,)
    res.execute(qry,user)
    con.commit()
    print("********************************************************")
    print("Delete the row successfully")
def update():
    print("********************************************************")
    StdID= int(input("Pls enter the StdID of Studentsmarksheet: "))
    print("********************************************************")
    res = con.cursor()
    qry = "select * from Studentsmarksheet where StdID = %s"
    value = (StdID,)
    res.execute(qry, value)
    record = res.fetchone()
    print("********************************************************")
    print(record)
    print("********************************************************")

    print("\nPress the option you want to edit: ")
    print("1.Name\n2.Stdclass\n3.Update Std Mark Details")
    print("********************************************************")

    edit = int(input("Pls enter the choice of edit: "))
    print("********************************************************")

    if edit == 1:
        print("********************************************************")
        name= input("Enter new Name: ")
        print("********************************************************")
        sql = "UPDATE Studentsmarksheet SET Stdname = %s WHERE StdID = %s"
        values = (name,StdID)
        res.execute(sql, values)
        con.commit()
        print("********************************************************")
        print("\n***Name updated successfully***")
    
    elif edit == 2:
        print("********************************************************")
        stdclass = input("Enter Stdclass : ")
        sql = "UPDATE Studentsmarksheet SET Stdclass = %s WHERE StdID = %s"
        values = (stdclass,StdID)
        res.execute(sql, values)
        con.commit()
        print("********************************************************")
        print("\n***Stdclass updated sucessfully***")
    elif edit ==3:
        tamil=int(input("Enter your Tamil mark:"))
        english=int(input("Enter your English mark:"))
        maths=int(input("Enter your Maths mark:"))
        science=int(input("Enter your Science mark:"))
        social=int(input("Enter your Social mark:"))
        sql = "UPDATE Studentsmarksheet SET Tamil = %s WHERE StdID = %s"
        values = (tamil,StdID)
        res.execute(sql, values)
        con.commit()
        sql = "UPDATE Studentsmarksheet SET English = %s WHERE StdID = %s"
        values = (english,StdID)
        res.execute(sql, values)
        con.commit()
        sql = "UPDATE Studentsmarksheet SET Maths = %s WHERE StdID = %s"
        values = (maths,StdID)
        res.execute(sql, values)
        con.commit()
        sql = "UPDATE Studentsmarksheet SET Science = %s WHERE StdID = %s"
        values = (science,StdID)
        res.execute(sql, values)
        con.commit()
        sql = "UPDATE Studentsmarksheet SET Social = %s WHERE StdID = %s"
        values = (social,StdID)
        res.execute(sql, values)
        con.commit()
        total=tamil+english+maths+science+social
        sql = "UPDATE Studentsmarksheet SET Total = %s WHERE StdID = %s"
        values = (total,StdID)
        res.execute(sql, values)
        con.commit()
        print("********************************************************")
        print("\n***Std Mark Details updated sucessfully***")
    else:
        print("\n***invalid edit option***\n")

    

    

def markanalysis():
    print("********************************************************")
    user = int(input("1.Tamil\n2.English\n3.Maths\n4.Science\n5.Social\n6.Total\nEnter your choice: "))
    print("********************************************************")

    if user == 1:
        Tamil = int(input("Enter a mark range: "))
        res = con.cursor()
        qry = "SELECT StdID, Stdname, Tamil FROM Studentsmarksheet WHERE Tamil >= %s"
        res.execute(qry, (Tamil,))
        result = res.fetchall()
        print("********************************************************")
        if len(result) > 0:
            print(tabulate(result, headers=["StdID", "Stdname", "Tamil"]))
        else:
            print("No students scored more than", Tamil, "marks in Tamil.")
        print("********************************************************")
    elif user == 2:
        English = int(input("Enter a mark range: "))
        res = con.cursor()
        qry = "SELECT StdID, Stdname, English FROM Studentsmarksheet WHERE English >= %s"
        res.execute(qry, (English,))
        result = res.fetchall()
        print("********************************************************")
        if len(result) > 0:
            print(tabulate(result, headers=["StdID", "Stdname", "English"]))
        else:
            print("No students scored more than", English, "marks in English.")
        print("********************************************************")
    elif user == 3:
        Maths = int(input("Enter a mark range: "))
        res = con.cursor()
        qry = "SELECT StdID, Stdname, Maths FROM Studentsmarksheet WHERE Maths >= %s"
        res.execute(qry, (Maths,))
        result = res.fetchall()
        print("********************************************************")
        if len(result) > 0:
            print(tabulate(result, headers=["StdID", "Stdname", "Maths"]))
        else:
            print("No students scored more than", Maths, "marks in Maths.")
        print("********************************************************")
    elif user == 4:
        Science = int(input("Enter a mark range: "))
        res = con.cursor()
        qry = "SELECT StdID, Stdname, Science FROM Studentsmarksheet WHERE Science >= %s"
        res.execute(qry, (Science,))
        result = res.fetchall()
        print("********************************************************")
        if len(result) > 0:
            print(tabulate(result, headers=["StdID", "Stdname", "Science"]))
        else:
            print("No students scored more than", Science, "marks in Science.")
        print("********************************************************")
    elif user == 5:
        Social = int(input("Enter a mark range: "))
        res = con.cursor()
        qry = "SELECT StdID, Stdname, Social FROM Studentsmarksheet WHERE Social >= %s"
        res.execute(qry, (Social,))
        result = res.fetchall()
        print("********************************************************")
        if len(result) > 0:
            print(tabulate(result, headers=["StdID", "Stdname", "Social"]))
        else:
            print("No students scored more than", Social, "marks in Social.")
        print("********************************************************")
    elif user == 6:
        Total = int(input("Enter a mark range: "))
        res = con.cursor()
        qry = "SELECT StdID, Stdname, Total FROM Studentsmarksheet WHERE Total >= %s"
        res.execute(qry, (Total,))
        result = res.fetchall()
        print("********************************************************")
        if len(result) > 0:
            print(tabulate(result, headers=["StdID", "Stdname", "Total"]))
        else:
            print("No students scored more than", Total, "marks in Total.")
        print("********************************************************")
    else:
        print("Invalid choice")

    
ch = "yes"
while ch == "yes":
    print("Welcome to Student DataBase")
    user = int(input("Your choice \n1.Insert\n2.Show data\n3.Delete\n4.Update\n5.Mark Analysis\nEnter a number:"))
    if user == 1:
        StdID=int(input("enter the student id:"))
        name=input("Enter your name:")
        stdclass=input("Enter a student class:")
        tamil=int(input("Enter your Tamil mark:"))
        english=int(input("Enter your English mark:"))
        maths=int(input("Enter your Maths mark:"))
        science=int(input("Enter your Science mark:"))
        social=int(input("Enter your Social mark:"))
        total=(tamil+english+maths+science+social)
        insert(StdID,name,stdclass,tamil,english,maths,science,social,total)
    elif user == 2:
        select()
    elif user==3:
        StdID=input("Enter a StdID:")
        delete(StdID)
    elif user==4:
        update()
    elif user==5:
        markanalysis()
    else:
        print("Invalid choice selected")
    ch = input("do you want to continue:")
