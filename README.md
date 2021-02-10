# OsuRecolorCode
The source code, here it is

FOR THOSE WHO WERE WORRIED, HERE IS THE SOURCE CODE, THAT'S IT, JUST A VERY BAD AND EASY AND QUICKLY MADE PYTHON PROGRAM. I DIDNT WANT TO SHOW IT BECAUSE MY CODE SUCKS, I'M JUST A 17 YEAR OLD COMPUTER SCIENCE STUDENT, NOT A PROFESSIONAL, I HAVE NO IDEA HOW VIRUSES WORK. IDEK HOW TO PUT THIS ON GITHUB

import os
import PIL
from PIL import Image, ImageEnhance
import numpy as np
import colorsys


"""Différents filtres pour Projet NSI"""



rgb_to_hsv = np.vectorize(colorsys.rgb_to_hsv)
hsv_to_rgb = np.vectorize(colorsys.hsv_to_rgb)

def shift_hue(arr, hout):
    r, g, b, a = np.rollaxis(arr, axis=-1)
    h, s, v = rgb_to_hsv(r, g, b)
    h = hout
    r, g, b = hsv_to_rgb(h, s, v)
    arr = np.dstack((r, g, b, a))
    return arr

def colorize(image, hue):
    """
    Colorize PIL image `original` with the given
    `hue` (hue within 0-360); returns another PIL image.
    """
    img = image.convert('RGBA')
    arr = np.array(np.asarray(img).astype('float'))
    new_img = Image.fromarray(shift_hue(arr, hue/360.).astype('uint8'), 'RGBA')
    return new_img

def copy(ListIM):
    p =  ".../copy"
    try:
        os.mkdir(p)
    except OSError:
        print ("Creation of the directory %s failed" % p)
        input("You should try and make a copy yourself ! (Press Enter to keep going)")
    else:
        print ("Successfully created the directory %s " % p)
        for l in range(len(ListIM)):
            Stop = False
            n = 0
            while Stop == False:
                try:
                    imn = ListIM[l]+str(n)+".png"
                    im = Image.open(imn)
                    path = "/copy/"+imn
                    im.save(path,"PNG")
                    n += 1
                except:
                    Stop = True


        for l in range(len(ListIM)):
            try:

                imn = ListIM[l]+".png"
                im = Image.open(imn)
                path = "/copy/"+imn
                im.save(path,"PNG")
            except:
                pass

def wholeskin(ListIM,C):
    for l in range(len(ListIM)):
        Stop = False
        n = 0
        while Stop == False:
            try:
                imn = ListIM[l]+str(n)+".png"


                im = Image.open(imn)
                im = colorize(im,C)

                im.save(imn,"PNG")
                n += 1
            except:
                Stop = True


    for l in range(len(ListIM)):
        try:

            imn = ListIM[l]+".png"

            im = Image.open(imn)
            im = colorize(im,C)
            im.save(imn,"PNG")
        except:
            pass


ListIM = ["mode-osu-small","fail-background","menu-back-","menu-back","menu-background","menu-button-background","menu-snow","mode-fruits-small","mode-mania-small","mode-taiko-small","multi-skipped","pause-overlay","play-skip","ranking-panel","scorebar-bg","ready","scorebar-colour-","section-fail","section-pass","selection-mode","selection-mods-over","selection-mode-over","selection-options","selection-options-over","selection-random-over","selection-random","selection-tab","arrow-pause","arrow-warning","count","play-skip","play-skip-","ranking-perfect-","scorebar-colour","selection-mods","selection-option","selection-random","welcome-text"]



check = 0
while check != True:
        a = str(input("Would you like to make a copy of this folder ? \n Y/N"))
        if a == "Y":
            check = True
            print("Creating copy...(Can take a while)")
            copy(ListIM)
        else:
            check = True

colors = {"1":-180,"2":-60,"3":-120,"4":-25,"5":60,"6":120}#1 = light blue, 2 = pink,3 = blue/purple, 4 = reddish, 5 = yellow, 6 = green

imn = ListIM[0]+".png"
im = Image.open(imn)
im = im.copy()

try:
    C = str(input("What color would you like? \n 1.Light Blue \n 2.Pink \n 3. Blue/purple \n 4 = Red ish? \n 5.Yellow \n 6.Green \n Anything above or below will allow for HUE value choice "))
    if int(C) > 6 or int(C) < 1:
        C = int(input("What HUE value would you like to apply ?"))
        if C < -180:
            C = -180
        if C > 180:
            C = 180
    else:
        C = colors[C]

    imn = ListIM[0]+".png"
    im = Image.open(imn)
    im = im.copy()
    im = colorize(im,C)
    im.show()

    e = 1
    check = 0
    while check != True:
            a = str(input("Would you like to enhance the color or is this good ?(If you can't see the preview wait a bit) (Enhancing too much will look weird)\n Y/N")).upper()
            if a == "Y":
                e += 1
                print("Enhancing...")
                enhancer = ImageEnhance.Color(im)
                im = enhancer.enhance(e)
                im.show()
            else:
                check = True



    REGULAR = int(input("Would you like to recolour the \n 1. regular images (Takes a while) \n 2. @2x images ?(Takes longer)\n 1/2"))
    if REGULAR == 2:
        print("WORKED")
        check = 0
        while check != True:
                a = str(input("Are you happy with your choices ?\n Y/N (N ends the program)")).upper()
                if a == "Y":
                    check = True
                    print("working super hard....")
                    for l in range(len(ListIM)):
                        Stop = False
                        n = 0
                        while Stop == False:
                            try:
                                imn = ListIM[l]+str(n)+"@2x"+".png"


                                im = Image.open(imn)
                                im = colorize(im,C)
                                enhancer = ImageEnhance.Color(im)
                                im = enhancer.enhance(e)

                                im.save(imn,"PNG")
                                n += 1
                            except:
                                Stop = True


                    for l in range(len(ListIM)):
                        try:

                            imn = ListIM[l]+"@2x"+".png"

                            im = Image.open(imn)
                            im = colorize(im,C)
                            enhancer = ImageEnhance.Color(im)
                            im = enhancer.enhance(e)
                            im.save(imn,"PNG")
                        except:
                            pass
                else:
                    break
    else:
        check = 0
        while check != True:
                a = str(input("Are you happy with your choices ?\n Y/N (N ends the program)")).upper()
                if a == "Y":
                    check = True
                    print("working super hard....")
                    for l in range(len(ListIM)):
                        Stop = False
                        n = 0
                        while Stop == False:
                            try:
                                imn = ListIM[l]+str(n)+".png"


                                im = Image.open(imn)
                                im = colorize(im,C)
                                enhancer = ImageEnhance.Color(im)
                                im = enhancer.enhance(e)

                                im.save(imn,"PNG")
                                n += 1
                            except:
                                Stop = True


                    for l in range(len(ListIM)):
                        try:

                            imn = ListIM[l]+".png"

                            im = Image.open(imn)
                            im = colorize(im,C)
                            enhancer = ImageEnhance.Color(im)
                            im = enhancer.enhance(e)
                            im.save(imn,"PNG")
                        except:
                            pass
                else:
                    break
except:
    print("Something went wrong ! Perhaps an unvalid answer ?")
    input("Press Enter to close")

input("Made by @AtherIdk")
