import sqlite3
massge = """
"d" => delet
"a" => add"
"s" => show
"u" => update
"""
l = input (massge).strip().lower()
k = ["a","d","s","u"]
db = sqlite3.connect("MMT25.7")
cr=db.cursor()
def close_commit ():
    db.commit()
    db.close()
    print("Database has been commit and close")
def delet():
    id = int (input ("Enter ther id to delete: "))
    name = input("Enter the name of Delet: ")
    cr.execute(f"delete from skillles where user_id='{id}' and name='{name}'")
    close_commit()
def add():
    id = int (input ("Enter ther id to add: "))
    name = input("Enter the name of add: ")
    #cr.execute(f"insert into skillles (user_id, name ) values('{id}', '{name}')")
    cr.execute(f"select name from skillles where user_id = '{id}' and name = '{name}'")
    res = cr.fetchone()
    if res != None:
        print("you can not add the name")
        Q = input("You wounte to Update the name Y or N ? ")
        if Q == "Y":
            def Update():
                id = int (input ("Enter ther New id to update: "))
                Nname = input("Enter the New name of update: ")
                cr.execute(f"update skillles set name = '{Nname}' where user_id='{id}'")
            Update()    
        elif Q == "N":
            print ("oky")        
    elif res == None:
        cr.execute(f"insert into skillles (user_id, name ) values('{id}', '{name}')")
    close_commit()
def show():
    id = int (input ("Enter ther id to show: "))
    cr.execute(f"select*from skillles where user_id= '{id}'")
    res = cr.fetchall()
    print(f"You Have {len(res)}skills")
    if len(res) > 0:
        print ("the your skills are:")
        for i in res :
            print(f"Is A {i[0]}=>",end=" ")
            print(f"{i[1]}")     
    close_commit()
def update():
    id = int (input ("Enter ther id to update: "))
    name = input("Enter the name of update: ")
    cr.execute(f"update skillles set name = '{name}' where user_id='{id}'")
    close_commit()
if l in k :
    if l == "d":
        delet()
    if l == "a":
        add()
    if l == "s":
        show()
    if l == "u":
        update()
else:
    print("it's not found")        
