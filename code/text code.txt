from tkinter import *
from PIL import Image, ImageTk
import winsound

# python -m pip install --upgrade pip
# python -m pip install --upgrade Pillow

#  python -m pip install https://github.com/pyinstaller/pyinstaller/archive/develop.tar.gz

root = Tk()
root.title("The 8th Gate")
root.iconbitmap('images\\carnival-mask.ico')

H = 700
W = 900
room = 1
karma = 0
basecolor = "SlateGray"
frame = Frame(root, height=H, width=W)
frame.pack()

paper = ImageTk.PhotoImage(Image.open("images\\darkpaper.png"))
paperL = Label(frame, image=paper).place(relwidth=1, relheight=1)


# Info: ---------------------------------------------------------------------------------
def info():
    clicked = OList.curselection()

    window = Toplevel()
    window.iconbitmap('images\\carnival-mask.ico')
    window.title("Information")
    space = Frame(window, height=200, width=200)
    space.pack()

    if clicked == (0,):
        global morse
        morse = ImageTk.PhotoImage(Image.open("images\\morse.jpg"))
        morseL = Label(space, image=morse).pack()

    elif clicked == (1,):
        global lovecraft
        lovecraft = ImageTk.PhotoImage(Image.open("images\\lovecraft.jpg"))
        lovecraftL = Label(space, image=lovecraft).pack()

    elif clicked == (2,):
        global druids
        druids = ImageTk.PhotoImage(Image.open("images\\druids.png"))
        druidsL = Label(space, image=druids).pack()

    elif clicked == (3,):
        global shift
        shift = ImageTk.PhotoImage(Image.open("images\\shift.png"))
        shiftL = Label(space, image=shift).pack()

    elif clicked == (4,):
        global Dante
        Dante = ImageTk.PhotoImage(Image.open("images\\Dante.png"))
        DanteL = Label(space, image=Dante).pack()

    elif clicked == (5,):
        global map
        map = ImageTk.PhotoImage(Image.open("images\\map.png"))
        mapL = Label(space, image=map).pack()

    elif clicked == (6,):
        global wendigo
        wendigo = ImageTk.PhotoImage(Image.open("images\\wendigo.png"))
        wendigoL = Label(space, image=wendigo).pack()

    elif clicked == (7,):
        global ouroboros
        ouroboros = ImageTk.PhotoImage(Image.open("images\\Ouroboros.png"))
        ouroborosL = Label(space, image=ouroboros).pack()


    else:
        spaceL = Label(space, text="To use the information, \npick an object from the list and press the Skull.",
                       font=('Rockwell', 25))
        spaceL.pack()


InfoFrame = Frame(frame)
InfoFrame.place(relwidth=0.187, relheight=0.5, relx=0.75, rely=0.46)
paperL = Label(InfoFrame, image=paper).place(relwidth=1, relheight=1)

skull = ImageTk.PhotoImage(Image.open("images\\skull.png"))
skull_B = Button(InfoFrame, image=skull, command=info).place(rely=0.5)

listLabel = Label(InfoFrame, text="Information", bg="SlateGray", font=('Rockwell', 16), relief=RAISED)
listLabel.place(relwidth=1, relheight=0.09)

listScroll = Scrollbar(InfoFrame)
listScroll.place(relwidth=0.12, relheight=0.32, relx=0.87, rely=0.09)
OList = Listbox(InfoFrame, yscrollcommand=listScroll.set, font=('Rockwell', 14))
OList.place(relwidth=0.88, relheight=0.32, rely=0.09)
listScroll.config(command=OList.yview)

OList.insert(0, "Morse code")
OList.insert(1, "H.P. Lovecraft")
OList.insert(2, "Druids")
OList.insert(3, "A1Z26")
OList.insert(4, "Dante Alighieri")
OList.insert(5, "Mind Maze")
OList.insert(6, "Wendigo")
OList.insert(7, "Ouroboros")




# Actual puzzles: ---------------------------------------------------------------------------------

def enter():

    winsound.PlaySound("sounds\\normal_click.wav", winsound.SND_ASYNC)

    global skull
    global skull_B
    global karma
    global room
    global Bcode
    word = entry.get().lower()
    radioC = int(radioCONT.get())
    num1 = int(numlist1.get())
    num2 = int(numlist2.get())
    num3 = int(numlist3.get())
    num4 = int(numlist4.get())

    if room == 1 and word == "fear":
        inst.set("On your arm, written in black ink is the number 1618.\nThere must be a meaning, there must be a purpose.")
        room += 1
        notes.insert(INSERT, "Don't forget\n\n")

    if room == 2 and num1 == 1 and num2 == 6 and num3 == 1 and num4 == 8:
        inst.set("Up is no roof.\n\nLeft and Right are walls made of liquid.\n\nBellow you a hard floor of mist and fog.")
        room += 1

    if room == 3 and Bcode == 213:
        inst.set("Infinity beyond numbers.\n\nThere must have been One entrance.\nTo a world of Zero things.\nWith your Two eyes you can only see,\nOne path.")
        room += 1

    if room == 4 and num1 == 1 and num2 == 0 and num3 == 2 and num4 == 1:
        inst.set("In a world of no direction, you follow your own path.\n\nLeft trough the liquid,\nUp you climb trough the spiral of mist.\nRight then Right again trough memories forgotten,\nUp one more time.\nEnding it right.")
        room += 1
        notes.insert(INSERT, "Does it end?\n\n")

    if room == 5 and Bcode == 123323:
        inst.set("Wendigo, foul creature of famine and death,\n\n\"Strongly associated with Winter and the north,\"\nOnce human overpowered by the thing you already know,\n\nThe deadly sin that once almost caused your demise.")
        room += 1

    if room == 6 and radioC == 3 and word == "greed":
        inst.set("Down the rabbit hole, you keep on descending, from layer to layer.\n\nYou keep on wandering like Dante trough the 9 layers of hell until his First Year of Death.")
        room += 1
        notes.insert(INSERT, "The mind lies\n\n")

    if room == 7 and num1 == 1 and num2 == 3 and num3 == 2 and num4 == 1:
        inst.set("The name is Inferno.\n\nWhere Red is the air like the Autumn leaves,\nA deep crimson Red your breath that you take.\nNo place nor direction just a lucid Red.\nRed is the color that governs them all.")
        room += 1

    if room == 8 and radioC == 2 and word == "inferno":
        inst.set("The name is Purgatorio.\n\nWalk or be stuck,\nFor when movement stops your blood Freezes Blue,\nDon't let the frost bite you,\nOr here you'll be left.")
        room += 1
        notes.insert(INSERT, "Searching for meaning\n\n")

    if room == 9 and radioC == 3 and word == "purgatorio":
        inst.set("The name is Paradiso\n\nYou are not yet here.\nA place of yellow sky,\nSun sets with a yellow halo\nSlight breeze with a yellow tint.\nPeace and serenity.\n")
        room += 1

    if room == 10 and radioC == 1 and word == "paradiso":
        inst.set("In front of you is a child, staring into the void.\nApproach or forget him, the choice is yours:\n\n-Approach\n-Forget")
        room += 1

    if room == 11 and (word == "approach" or word == "forget"):
        if word == "approach":
            karma += 1
        else:
            karma -= 1

        skull = ImageTk.PhotoImage(Image.open("images\\skull2.png"))
        skull_B = Button(InfoFrame, image=skull, command=info).place(rely=0.5)

        inst.set("Your awakening begins,\nAs one eye opens, the other those the same.\n18 5 12 9 22 5")
        room += 1

    if room == 12 and word == "relive":
        inst.set("Druids forgotten, their age has passed,\nThey only remain in history and thought.\nLearn from them, their history and open their scroll.\nTo advance remember,\n\nthe Last Word.")
        room += 1
        notes.insert(INSERT, "How many     times?\n\n")

    if room == 13 and word == "magic":
        inst.set("The word is: Ascend\nThe Green breath of nature, of trees and of Spring.\nThe cycle of life, no start and no end.\nRemember the Green and it's peace of mind.")
        room += 1

    if room == 14 and radioC == 4 and word == "ascend":
        inst.set("Cycle of life, biting it's own tail,\nDeath, birth and rebirth in an endless loop,\nLike a dragon eating it's own tail,\nThe Word is the Symbol that represents them all. ")
        room += 1
        notes.insert(INSERT, "It's not what it seems\n\n")

    if room == 15 and word == "ouroboros":
        inst.set("Between fantasy and reality is were you are now.\nFind the way out by struggling left up and right to wake up.\nAs you begin from the eye, you challenge the Mind Maze.\n\nYou enter the Cave and then the Crypt.")
        room += 1

    if room == 16 and Bcode == 23:
        inst.set("Sound that is real mixes with inaudible noise.\n\nFrom the Crypt you enter the room to the left of the Hold that is below the Vault.\nThen you walk into the room below the Wine Cellar.")
        room += 1
        notes.insert(INSERT, "Your heart   has value\n\n")

    if room == 17 and Bcode == 22:
        inst.set("From the Throne Room you enter the room to the left of the Vault.\n\nYou walk in the room below the Forge and Mine that is near the Hold.\n\nYou move into the Tomb and escape your unreality.")
        room += 1

    if room == 18 and Bcode == 332:
        inst.set("A mirror stands at the end of your path,\nThe choice is to break it or gaze into it.\n\n-Break\n-Gaze")
        room += 1
        notes.insert(INSERT, "Who am I?\n\n")

    if room == 19 and (word == "break" or word == "gaze"):
        if word == "break":
            karma -= 1
        else:
            karma += 1

        skull = ImageTk.PhotoImage(Image.open("images\\eye.jpg"))
        skull_B = Button(InfoFrame, image=skull, command=info).place(rely=0.5)

        inst.set("As your Two legs stand you wake up,\nYou are surrounded by Four white walls\nYou are but One mind,\nCaged in One body.")
        room += 1

    if room == 20 and num1 == 2 and num2 == 4 and num3 == 1 and num4 == 1:
        inst.set("Sparks from your mind still seem to flicker:\n\n...   .-   -.-.   .-.   ..   ..-.   ..   -.-.   .")
        room += 1

    if room == 21 and word == "sacrifice":
        inst.set("Who am I and why am I here?\n\n...   ..-   .-.   ...-   ..   ...-   .")
        room += 1
        notes.insert(INSERT, "Are you there\n\n")

    if room == 22 and word == "survive":
        inst.set("What do I want and what am I seeking?\n\n.--.   .   .-   -.-.   .")
        room += 1
        notes.insert(INSERT, "Am I alone?\n\n")

    if room == 23 and word == "peace":
        inst.set("The four corners of your mind branded with one symbol each,\nInfinity on each of them ∞.\nTo master your mind,\nTurn infinity back. ")
        room += 1
        notes.insert(INSERT, "So long ago\n\n")

    if room == 24 and num1 == 8 and num2 == 8 and num3 == 8 and num4 == 8:
        inst.set("Don't forget the past, but don't get trapped either.\nFor occult and or magic, you need Love for your Craft.\nSurpass the cursed 6th line.")
        room += 1
        notes.insert(INSERT, "Trust your     senses\n\n")

    if room == 25 and word == "aeons":
        inst.set("Your last choice has come,at the end of your journey,\nBelow the door a red light begins to shine.\nWill you pass or will the cycle repeat,\nThe choice was yours.\nOpen the door or ignore the light.\n\n-Open\n-Ignore")

        skull = ImageTk.PhotoImage(Image.open("images\\door.jpg"))
        skull_B = Button(InfoFrame, image=skull, command=info).place(rely=0.5)

        room += 1

    if room == 26 and (word == "open" or word == "ignore"):
        if word == "open":
            karma += 1
        else:
            karma -= 1

        global frame
        global end
        if karma == 3:
            end = ImageTk.PhotoImage(Image.open("images\\good.png"))
        else:
            end = ImageTk.PhotoImage(Image.open("images\\bad.png"))
        endL = Label(frame, image=end).pack()

    buttonR()
    entry.delete(0, 'end')




# Text instructions ---------------------------------------------------------------------------------
inst = StringVar()
instructions = Message(frame, textvariable=inst, anchor=NW, font=('Century', 20), width=440)
instructions.place(relwidth=0.5, relheight=0.6, relx=0.2, rely=0.13)
inst.set("Your first word is: Fear .\nThe most powerful human emotion.")



# Notes Code ---------------------------------------------------------------------------------
notesFrame = Frame(frame, bg="black")
notesFrame.place(relwidth=0.15, relheight=0.5, relx=0.02, rely=0.02)

notesScroll = Scrollbar(notesFrame)
notesScroll.place(relwidth=0.12, relheight=0.87, relx=0.88, rely=0.13)

notes = Text(notesFrame, yscrollcommand=notesScroll.set, fg="black", font=('Monotype Corsiva', 18))
notes.place(relwidth=0.88, relheight=0.87, rely=0.13)
notes.insert(INSERT, "When you    want to          confirm any  code, press   ENTER.\n\n")
notesScroll.config(command=notes.yview)

notesL = Label(notesFrame, text="Your Notes:", fg="black", bg=basecolor, font=('Rockwell', 16), relief=GROOVE)
notesL.place(relwidth=1, relheight=0.13)



# Entry code ---------------------------------------------------------------------------------
entry = Entry(frame, font=('Century', 18))
entry.place(relwidth=0.5, relheight=0.07, relx=0.2, rely=0.02)

entryENTER = Button(entry, text="Enter", command=enter, bg=basecolor, font=('Stencil', 19))
entryENTER.place(relwidth=0.2, relheight=1, relx=0.8, )



# Number selections ---------------------------------------------------------------------------------
numlistFrame = Frame(frame)
numlistFrame.place(relwidth=0.23, relheight=0.38, relx=0.74, rely=0.04)
paperL = Label(numlistFrame, image=paper).place(relwidth=1, relheight=1)

numlist1 = Spinbox(numlistFrame, from_=0, to=9, font=('Cooper Black', 40))
numlist1.place(relwidth=0.45, relheight=0.35)
num1L = Label(numlistFrame, text="I", fg="black", bg=basecolor, font=('Cooper Black', 20), relief=GROOVE)
num1L.place(relwidth=0.45, relheight=0.12, rely=0.35)

numlist2 = Spinbox(numlistFrame, from_=0, to=9, font=('Cooper Black', 40))
numlist2.place(relwidth=0.45, relheight=0.35, relx=0.55)
num2L = Label(numlistFrame, text="II", fg="black", bg=basecolor, font=('Cooper Black', 20), relief=GROOVE)
num2L.place(relwidth=0.45, relheight=0.12, relx=0.55, rely=0.35)

numlist3 = Spinbox(numlistFrame, from_=0, to=9, font=('Cooper Black', 40))
numlist3.place(relwidth=0.45, relheight=0.35, rely=0.54)
num3L = Label(numlistFrame, text="III", fg="black", bg=basecolor, font=('Cooper Black', 20), relief=GROOVE)
num3L.place(relwidth=0.45, relheight=0.12, rely=0.88)

numlist4 = Spinbox(numlistFrame, from_=0, to=9, font=('Cooper Black', 40))
numlist4.place(relwidth=0.45, relheight=0.35, relx=0.55, rely=0.54)
num4L = Label(numlistFrame, text="IV", fg="black", bg=basecolor, font=('Cooper Black', 20), relief=GROOVE)
num4L.place(relwidth=0.45, relheight=0.12, relx=0.55, rely=0.88)



# Radio Button: ---------------------------------------------------------------------------------
radioF = Frame(frame)
radioF.place(relwidth=0.15, relheight=0.2, relx=0.02, rely=0.54)
radioCONT = IntVar()

radio1 = Radiobutton(radioF, variable=radioCONT, value=1, text="Summer", relief=SUNKEN, font=('Rockwell', 16),bg="Goldenrod", anchor=NW)
radio1.pack(fill=X)

radio2 = Radiobutton(radioF, variable=radioCONT, value=2, text="Autumn", relief=SUNKEN, font=('Rockwell', 16),bg="Tomato", anchor=NW)
radio2.pack(fill=X)

radio3 = Radiobutton(radioF, variable=radioCONT, value=3, text="Winter", relief=SUNKEN, font=('Rockwell', 16),bg="SkyBlue", anchor=NW)
radio3.pack(fill=X)

radio4 = Radiobutton(radioF, variable=radioCONT, value=4, text="Spring", relief=SUNKEN, font=('Rockwell', 16),bg="YellowGreen", anchor=NW)
radio4.pack(fill=X)



# Buttons: ---------------------------------------------------------------------------------
Bcode = 0

def buttonR():
    global Bcode
    Bcode = 0

def buttoncode(button):
    global Bcode
    Bcode = Bcode * 10 + button

def button1():
    buttoncode(1)
def button2():
    buttoncode(2)
def button3():
    buttoncode(3)

ButtonFrame = Frame(frame)
ButtonFrame.place(relwidth=0.6, relheight=0.15, relx=0.08, rely=0.79)
paperL = Label(ButtonFrame, image=paper).place(relwidth=1, relheight=1)

redLeft = ImageTk.PhotoImage(Image.open("images\\redLeft.png"))
Button1 = Button(ButtonFrame, relief=RIDGE, image=redLeft, command=button1)
Button1.place(relwidth=0.2, relheight=1)

redUp = ImageTk.PhotoImage(Image.open("images\\redUp.png"))
Button2 = Button(ButtonFrame, relief=RIDGE, image=redUp, command=button2)
Button2.place(relwidth=0.2, relheight=1, relx=0.28)

redRight = ImageTk.PhotoImage(Image.open("images\\redRight.png"))
Button3 = Button(ButtonFrame, relief=RIDGE, image=redRight, command=button3)
Button3.place(relwidth=0.2, relheight=1, relx=0.56)

ButtonReset = Button(ButtonFrame, bg="Maroon", fg="Salmon", text="Reset", font=('Stencil', 13), command=buttonR)
ButtonReset.place(relwidth=0.13, relheight=0.5, relx=0.84, rely=0.25)



root.mainloop()

# Made by: Pilescu Adrian Mihai
# First Python project
# 2019