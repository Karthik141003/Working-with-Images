# Working-with-Images

import tkinter
from tkinter import *
from tkinter import ttk
from tkinter import filedialog
from PIL import Image, ImageTk

class Root(Tk):
    def __init__(self):                                                    #Creating label
        super(Root, self).__init__()
        self.title("Working With Images")
        self.minsize(640, 400)
        instructions=tkinter.Label(self,text="Select the picture",font=("Comic Sans MS",40))
        instructions.pack()
        label=tkinter.Label(self)
        label.pack()

        self.labelFrame = ttk.LabelFrame(self,text ="Open File")
        self.labelFrame.pack(side="top",fill=None,expand=False)

        self.button()

    def button(self):                                                #Creating button

        self.button = ttk.Button(self.labelFrame, text = "Browse A File",command = self.fileDialog)
        self1=ttk.Button(self.labelFrame, text = "Return",command = self.destroy)
        self.button.pack(side="top",fill=None,expand=False)
        self1.pack(side="bottom",fill=None,expand=False)


    def fileDialog(self):                                               #File dialog box

        self.filename = filedialog.askopenfilename(initialdir =  "/", title = "Select A File", filetype =
        (("jpeg files","*.jpg"),("png files","*.png"),("all files","*.*")) )
        self.label = ttk.Label(self.labelFrame, text = "")
        self.label.pack(fill="both",expand=True)
        self.label.configure(text = self.filename)

        global img                                                       #Opening image
        img = Image.open(self.filename)
        photo = ImageTk.PhotoImage(img)

        self.label2 = Label(image=photo)
        self.label2.image = photo 
        self.label2.pack(fill="both",expand=True)

root = Root()
root.mainloop()

def save_img(edit):
    global f
    f=0                                                                                    #Saving image
    ch=input("Do you want to save the editted image (Y/N) : ")
    if ch=="Y":
        f+=1
        save_path=input("Enter path where the image should be saved : ")
        save_name=input("Enter name of the editted image with format : ")
        path=save_path+"\\"+save_name
        edit.save(path)

    elif ch=="N":
        print('------------------------------------------------')
        pass

    else:
        print("Invalid choice")
        print('------------------------------------------------')


c=input("Do you want to edit the selected image (Y/N) : ")
if c=="N":
    print('------------------------------------------------')
    pass


elif c=="Y":
    print("-------------WORKING WITH IMAGES-------------")
    print('------------------------------------------------')
    while True:                                                                 #Choice list
        print("| 1.To Rotate an Image")
        print("| 2.To Crop an Image")
        print("| 3.To Resize an Image")
        print("| 4.To Convert an Image into Grayscale")
        print("| 5.To Transpose an Image")
        print("| 6.To Split an Image into RGB values")
        print("| 7.Exit")
        print('------------------------------------------------')

        choice=int(input("-Enter your choice for performing image operations: "))
        print('------------------------------------------------')

        if choice==7:
            print("--------------------Thank You--------------------")
            print('------------------------------------------------')
            break

        elif choice==1:                                                           #To Rotate an Image 
            rotate=int(input("Enter rotation angle : "))
            rotate_img=img.rotate(rotate)
            rotate_img.show()
            print("Image Rotated")
            print('------------------------------------------------')
            save_img(rotate_img)
            if f==1:
                print("Rotated Image Saved")
                print('------------------------------------------------')

        elif choice==2:                                                           #To Crop an Image
            left=int(input("Enter left dimemsion of the cropped image : "))
            top=int(input("Enter top dimemsion of the cropped image: "))
            right=int(input("Enter right dimemsion of the cropped image : "))
            bottom=int(input("Enter bottom dimemsion of the cropped image : "))	
            try:
                crop_img=img.crop((left,top,right,bottom))
                crop_img.show()
                print("Image Cropped")
                print('------------------------------------------------')
                save_img(crop_img)
                if f==1:
                    print("Cropped Image Saved")
                    print('------------------------------------------------')
            except SystemError:
                print("Image cannot be cropped using the given dimensions")
                print('------------------------------------------------')

        elif choice==3:                                                           #To Resize an Image
            width=int(input("Enter width of the resized image : "))
            height=int(input("Enter height of the resized image : "))
            try:
                resize_img=img.resize((width,height))		
                resize_img.show()
                print("Image Resized")
                print('------------------------------------------------')
                save_img(resize_img)
                if f==1:
                    print("Resized Image Saved")
                    print('------------------------------------------------')
            except MemoryError: 
                print("Image cannot be resized using the given dimensions")
                print('------------------------------------------------')

        elif choice==4:                                                           #To convert into grayscale 
            grayscale=img.convert("L")
            grayscale.show()
            print("Image converted to Graysacle")
            print('------------------------------------------------')
            save_img(grayscale)
            if f==1:
                print("Grayscale of image is saved")
                print('------------------------------------------------')

        elif choice==5:                                                           #To Transpose an Image
            transpose_img=img.transpose(Image.FLIP_LEFT_RIGHT) 
            transpose_img.show()
            print("Image Transposed")
            print('------------------------------------------------')
            save_img(transpose_img)
            if f==1:
                print("Transposed Image Saved")
                print('------------------------------------------------')

        elif choice==6:                                                           #To Split an Image into its RGB values 		
            rgb=img.split()
            print("RGB values are : ")
            print(rgb)
            print('------------------------------------------------')

        else:
            print("Enter valid choice")
            print('------------------------------------------------')

else:
    print("Invalid choice")
    print('------------------------------------------------')


