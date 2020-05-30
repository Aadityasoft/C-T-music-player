# C-T-music-player
C&amp;T music player Repository
import tkinter
from pygame import mixer
import tkinter.messagebox
from tkinter import filedialog
window = tkinter.Tk()

mixer.init()
icon = window.iconbitmap(r'icon.ico')
title = window.title("C&T Music Player")
size = window.geometry("400x400")
window.configure(bg="yellow")
toptext = tkinter.Label(window, text = "welcome to C&T Music Player").pack(pady=10)


def for_menu():
      print("work is done by aditya")
menubar = tkinter.Menu(window)
submenu1 = tkinter.Menu(menubar,tearoff=0)
submenu2 = tkinter.Menu(menubar,tearoff=0)
submenu3 = tkinter.Menu(menubar,tearoff=0)
def open_file():
    global filename
    filename = filedialog.askopenfilename()
menubar.add_cascade(label="File",menu=submenu1,command=for_menu)
submenu1.add_cascade(label="Open",command= open_file )
submenu1.add_cascade(label="Open recent")
submenu1.add_cascade(label="Setting")
submenu1.add_cascade(label="Exit")
menubar.add_cascade(label="Help",menu=submenu2,command=for_menu)
submenu2.add_cascade(label=" Edit file")
submenu2.add_cascade(label=" select ")
submenu2.add_cascade(label="paste")
submenu2.add_cascade(label="copy")
menubar.add_cascade(label="About us", menu=submenu3,command=for_menu)
def error():
    tkinter.messagebox.showwarning('C&T Music Player','you are in problem')
submenu3.add_cascade(label="Exit",command=error)
window.config(menu=menubar)

middleframe= tkinter.Frame(window)
middleframe.pack(pady=10)

#def show_details():
#    a= mixer.sound(filename)
#    total_lenght= a.get_length()
#    mins,secs= divmod(total_lenght,60)
#    print(mins)
#    print(secs)
#lenghtlabel=tkinter.Label(window, command= show_details ,text=" Totoal_length :  00:00 ").pack(pady=10)

def Play_btn():
    try:
        paused
    except NameError:
        try:
            mixer.music.load(filename)
            mixer.music.play()
            statusbar["text"]="playing music..."
        except:
               tkinter.messagebox.showerror("file not found","please check again")
    else:
        mixer.music.unpause()


playphoto=tkinter.PhotoImage(file="play-button.png")
playbtn=tkinter.Button(middleframe, image=playphoto,command=Play_btn).grid(row=0,column=1,padx=10)

def stop_music():
    statusbar['text']="stop music"
    mixer.music.stop()
stophoto =tkinter.PhotoImage(file="stop.png")
stopbtn = tkinter.Button(middleframe, image= stophoto , command = stop_music).grid(row=0,column=2,padx=10)

def pause_btn():
     global paused
     paused= True
     mixer.music.pause()
     statusbar['text']="paused music"
pausephoto =tkinter.PhotoImage(file="pause.png")
pausebtn= tkinter.Button(middleframe,image= pausephoto,command= pause_btn).grid(row=0,column=3,padx=10)

def mute_music():
    volumeBtn.configure(image=mutephoto)

bottomframe=tkinter.Frame(window)
bottomframe.pack()

def set_volume(val):
    volume = int(val)/100
    mixer.music.set_volume(volume)
volumeset = tkinter.Scale(bottomframe,from_=0,to=100, orient="horizontal", command = set_volume)
volumeset.set(45)
mixer.music.set_volume(0.45)
volumeset.grid(row=0,column=1)
def mute_music():
     volumeBtn.configure(image=mutephoto)

mutephoto=tkinter.PhotoImage(file="muted (1).png")
volumephoto=tkinter.PhotoImage(file="volume (1).png")
volumeBtn=tkinter.Button(bottomframe,image=volumephoto,command= mute_music).grid(row=0,column=0)


statusbar = tkinter.Label(window,text="About us-C&T Music Player",relief="sunken",anchor="w")
statusbar.pack(side="bottom",fill="x")

window.mainloop()




