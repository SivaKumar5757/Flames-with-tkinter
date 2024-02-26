# Flames-with-tkinter
its a simple flames game with tkinter
from tkinter import *
from tkinter import messagebox
from smtplib import *
from turtle import *
dark=Tk()
dark.geometry('515x600')
dark.title("Dark's Flames")
dark.config(background="black",highlightthickness=0)
loadingimg=PhotoImage(file="lods.png")
lscreen=Label(dark,image=loadingimg,highlightthickness=0,background="black")
menupic=PhotoImage(file="menu.png")
flamespic=PhotoImage(file="flames.png")
iconimg=PhotoImage(file="icon.png")
icon=Label(dark,image=iconimg,background="#202020")
loveimg=PhotoImage(file="love.png")
enemyimg=PhotoImage(file="enemy.png")
friendsimg=PhotoImage(file="friends.png")
affectionimg=PhotoImage(file="affection.png")
siblingimg=PhotoImage(file="siblings.png")
marriageimg=PhotoImage(file="marriage.png")
cardfont=("Helvetica",10,"bold")
result =None
str1=None
str2=None
final=None
def change():
     dark.config(background="white")
def flamesportion():
    lscreen.config(background="white")
    home.config(background="white")
    icon.config(image="")
    back.place(x=300,y=15)
    can.place(x=0,y=0)
    firstname.place(x=10,y=100)
    FN.place(x=140,y=100)
    secondname.place(x=10,y=140)
    SN.place(x=140,y=140)
    b.place(x=400,y=400)
    FN.focus()
def hide():
    FN.delete(0,END)
    SN.delete(0,END)
    dark.config(background="#202020")
    home.config(background="#202020")
    lscreen.config(background="#202020")
    icon.config(image=iconimg)
    can.place_forget()
#starting statement for flames mechanism.
def sample(evn):
    if len(SN.get())==0 and len(FN.get())!=0:
        SN.focus()
    else:
        hi()
def hi():
    str1=FN.get()
    while " " in str1:
        str1=list(str1)
        str1.remove(" ")
    str1="".join(str1)
    str2=SN.get()
    while " " in str2:
        str2=list(str2)
        str2.remove(" ")
    str2="".join(str2)
    checker(str1,str2)
def checker(str1,str2):
    err=False
    if not str1.isalpha():
        err=True
    elif not str2.isalpha():
        err=True
    if ((len(str1)<3 or len(str2)< 3) and (not err)) or (len(str1)==0 or len(str2)==0):
        messagebox.showinfo("Lack of data",f"check whether the name is entered.")
    elif not err:
        flamesmech(str1,str2)
    else:
        messagebox.showinfo("Invalid character",f"Plese check the characters entered.")
def lover(str1,str2):
    card.create_image(250,300,image=loveimg)
    card.create_text(135,125,fill="#DCB088",font=("Helvetica",15,"bold"),text=str1.capitalize())
    card.create_text(372,440,fill="#DCB088",font=("Helvetica",15,"bold"),text=str2.capitalize())
    card.place(x=0,y=0)
def enemy(str1,str2):
    card.create_image(250,300,image=enemyimg)
    card.create_text(110,135,fill="white",font=("Helvetica",15,"bold"),text=str1.capitalize())
    card.create_text(400,460,fill="white",font=("Helvetica",15,"bold"),text=str2.capitalize())
    card.place(x=0,y=0)
def friends (str1,str2):
    card.create_image(250,300,image=friendsimg)
    card.create_text(125,125,fill="#173899",font=cardfont,text=str1.capitalize())
    card.create_text(383,125,fill="#173899",font=cardfont,text=str2.capitalize())
    card.place(x=0,y=0)
def affection(str1,str2):
    card.create_image(250,300,image=affectionimg)
    card.create_text(100,475,fill="black",font=("Helvetica",15,"bold"),text=str1.capitalize())
    card.create_text(405,475,fill="black",font=("Helvetica",15,"bold"),text=str2.capitalize())
    card.place(x=0,y=0)
def marriage(str1,str2):
    card.create_image(250,300,image=marriageimg)
    card.create_text(125,300,fill="white",font=("Helvetica",10,"bold"),text=str1.capitalize())
    card.create_text(400,300,fill="white",font=("Helvetica",10,"bold"),text=str2.capitalize())
    card.place(x=0,y=0)
def siblings(str1,str2):
    card.create_image(250,300,image=siblingimg)
    card.create_text(125,125,fill="black",font=("Helvetica",15,"bold"),text=str1.capitalize())
    card.create_text(390,475,fill="black",font=("Helvetica",15,"bold"),text=str2.capitalize())
    card.place(x=0,y=0)
def flamesmech(str1,str2):
    str1=str1.lower()
    str2=str2.lower()
    namelist=list(str1)
    namelist2=list(str2)
    namelist3=namelist+namelist2
    set1=set(namelist3)
    namelist3=sorted(set1)
    flames=0
    for i in namelist3:
        count1=namelist.count(i)
        count2=namelist2.count(i)
        if count1>count2:
            point = count1-count2
            flames+=point
        elif count2>count1:
            point=count2-count1
            flames+=point
    result = ["Friends", "Love", "Affection", "Marriage", "Enemy", "Siblings"]
    while len(result) > 1:
        split_index = (flames % len(result) - 1)
        if split_index >= 0:
                right = result[split_index + 1:]
                left = result[: split_index]
                result = right + left
        else:
                result = result[: len(result) - 1]
    final=result[0]
    if flames==0:
        final="Enemy"
    if final=="Love":
        home.after(1,lover(str1,str2))
        lscreen.config(background="#D9AF87")
    elif final=="Enemy":
        home.after(1,enemy(str1,str2))
        lscreen.config(background="#2B313F")
    elif final=="Affection":
        home.after(1,affection(str1,str2))
        lscreen.config(background="#77B0C3")
    elif final=="Siblings":
        home.after(1,siblings(str1,str2))
        lscreen.config(background="#2A2A2A")
    elif final=="Marriage":
        home.after(1,marriage(str1,str2))
        lscreen.config(background="#94142D")
    elif final=="Friends":
        home.after(1,friends(str1,str2))
        lscreen.config(background="#90ADBB")
    FN.delete(0,END)
    SN.delete(0,END)
#closing statement
def mid():
    dark.config(background="#202020")
    lscreen.config(image="",background="#202020")
lscreen.after(2000,mid)

def load():
    lscreen.place(x=0,y=0)
    lscreen.lift()
    lscreen.after(100,load)
load()
def nd():
    messagebox.showinfo("Not in use","not devoloped yet")
home=Canvas(width=515,height=600,background="#202020",highlightthickness=0)
menu=Button(home,image=menupic,command=nd,cursor="watch").place(x=470,y=15)
flamesb=Button(home,image=flamespic,background="#202020",highlightthickness=0,command=lambda : [flamesportion(),change()],cursor="arrow").place(x=15,y=100)
def iconf():
    icon.place(x=-6,y=0)
    icon.lift()
    icon.after(100,iconf)
home.grid(column=0,row=0)
home.after(2000,iconf)
can=Canvas(width=515,height=600,background="white",highlightthickness=0)
card=Canvas(width=515,height=600,background="#2B313F",highlightthickness=0)
logo=PhotoImage(file="logo.png")
can.create_image(30,30,image=logo)
can.create_text(170,30,text="Love is an endless act of sacrifice")
firstname=Label(can,background="white",text="First Name:")
FN=Entry(can,width=35,highlightbackground="gray",highlightthickness=1,highlightcolor="royalblue")
SN=Entry(can,width=35,highlightbackground="gray",highlightthickness=1,highlightcolor="royalblue")
back=Button(can,text="🔙",command=hide)
secondname=Label(can,background="white",text="Second Name:")
b=Button(can,text="Done",command=hi)
dark.bind(sequence="<Return>",func=sample)
dark.mainloop()
