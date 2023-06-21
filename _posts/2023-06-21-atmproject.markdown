---
title: " We Built Our Own ATM Application Using Python!"
layout: post
date: 2023-06-21 08:04
image: /assets/images/atm_ai.jpg
headerImage: false
tag:
- books
- hobbies
- extra
category: project
author: yusifmirzebeyli
description: You should check out!
---

# I Built My Own ATM Application Using Python!

Hello, everyone! In this post, I would like to share with you an amateur ATM application that I developed with two of my friends using the Python programming language. I hope you find it interesting!

We are a group of friends who are taking our first steps into the world of programming, and fueled by our curiosity about the power of Python, we embarked on this project together. Our goal was to create a simple application that mimics ATM transactions and, in the process, gain a better understanding of the fundamental concepts of Python.

## Project Overview

Before diving into the project, we defined our requirements and objectives. We planned to develop an ATM application that would validate account information by requesting the user's card number and PIN, and perform basic operations such as balance inquiries, withdrawals, and deposits.You can check out our project 
{% highlight html %}

#This program was made by team work with The Hashad, Sleuth and Selim  https://discord.gg/e8EttN5HaE

class Kart():

    def __init__(self,ad,soyad,kartNo,sifre,bakiye,borc,maxKredi):
        self.ad = ad
        self.soyad = soyad
        self.kartNo = kartNo
        self.sifre = sifre
        self.bakiye = bakiye
        self.borc = borc
        self.maxKredi = maxKredi


class ATM():
    def __init__(self):
        self.kart = self.kartNumaraDenetleme() 
        self.sifreYoklama()        

    def anaFonksiyon(self):
        
        secim = self.menu()
        
        if secim == 1:
            self.paraCekme()
            
        elif secim == 2:
            self.paraYatirma()
        
        elif secim == 3:
            self.borcOdeme()   
            
        elif secim == 4:
            self.borcAlma()

        elif secim == 5:
            self.bakiye()

        elif secim == 6:
            self.cikis()
        

    def menu(self):
    
        print("""\t\t------------------| Hoş Geldiniz Değerli Müşterimiz! Yapmak istediğiniz işlemi rakamıyla belirtiniz. |------------------\n
\t\t[1] => Para çekme
\t\t[2] => Para yatırma
\t\t[3] => Borç ödeme
\t\t[4] => Borç alma
\t\t[5] => Bakiye
\t\t[6] => Çıkış\n""")
                
        liste = [1,2,3,4,5]
        while True:
            secim = int(input('Yapmak istediğiniz işlemi seçiniz: '))
            if secim not in liste:
                print('1-5 arasında seçim yapınız.\n')
                continue
            break    
        print()
                   
          
        return secim

               
    def sifreYoklama(self):
        
        can = 2
        
        for i in range(0,3):
    
            girilenKod = input("Buraya sifrenizi giriniz: ")
        
            if girilenKod == self.kart.sifre:
                print('Giriş başarılı.\n')
                self.anaFonksiyon()
                exit()

            elif girilenKod != self.kart.sifre and can > 0:
                print("Şifre yanliş kalan hakkiniz {}\n".format(can))
                can -= 1
                continue

            elif girilenKod != self.kart.sifre and can == 0:
                print("Giriş yapılamadı.\n")
                exit()
                
       
    def borcOdeme(self):

        odenecekMiktar = int(input('{} $ borcunuz var. Ödemek istediğiniz borç tutarını giriniz: '.format(self.kart.borc)))
        
        deger = self.elleOdeme()
        

        if self.kart.borc > 0:
        
            if odenecekMiktar <= self.kart.borc:

                if deger == 'elle':
                    self.kart.borc -= odenecekMiktar

                if deger == 'bakiye':
                    if odenecekMiktar <= self.kart.bakiye:
                        self.kart.bakiye -= odenecekMiktar
                        self.kart.borc -= odenecekMiktar
                    else:
                        print('Yeterli bakiyeniz yoktur. {} $ eksiğiniz var'.format(odenecekMiktar - self.kart.bakiye))
                        self.menuDonme()
            else:
                
                if deger == 'elle':
                    print('\nBorcunuz girdiğiniz değerden daha azdır. Borcunuz kalmamıştır. {} $ geri verildi\n'.format(odenecekMiktar - self.kart.borc))   
                    self.kart.borc = 0
                        
                elif deger == "bakiye":
                        
                    if odenecekMiktar <= self.kart.bakiye:
                        print('\nBorcunuz girdiğiniz değerden daha azdır. Borcunuz kalmamıştır. {} $ geri verildi\n'.format(odenecekMiktar - self.kart.borc))
                        self.kart.bakiye -= self.kart.borc
                        self.kart.borc = 0

                    else:
                        print('Yeterli bakiyeniz yoktur. {} $ eksiğiniz var'.format(odenecekMiktar - self.kart.bakiye))
                        self.menuDonme()
                    

            
            
            if self.kart.borc > 0:
                print("{} $ borcunuzdan {} $ silindi. Geride {} $ borcunuz kaldi\n".format(self.kart.borc + odenecekMiktar,odenecekMiktar,self.kart.borc ))

            else:
                print('Ödenecek borcunuz kalmamıştır.\n')
                
        else:
            print('Ödeyecek borcunuz yoktur')

    
            



        self.menuDonme()
    

    def borcAlma(self):
        alinacakMiktar = int(input("Almak istediğiniz borc miktarını belirtiniz."))
        
        if alinacakMiktar <= self.kart.maxKredi:
            self.kart.maxKredi -= alinacakMiktar
            self.kart.bakiye += alinacakMiktar
            self.kart.borc += alinacakMiktar
            
            print("Kart bakiyenize {} $ eklendi. Mevcut bakiyeniz {} $'dır.".format(alinacakMiktar,self.kart.bakiye))
            self.menuDonme()
        
        else:
            print("Bu kadar çok kredi çekemezsiniz. Müşteri haklarını bir daha gözden geçirin :)")
            self.menuDonme()
    
    
    def elleOdeme(self):
        while True:
            odemeYolu = int(input("Parayı nakit olarak ödemek istiyorsaniz 1'i, hesap bakiyesinden ödemek istiyorsaniz 2'yi seçiniz.\n"))

            if odemeYolu == 1:
                return 'elle'
                           
            elif odemeYolu == 2:
                return 'bakiye'
            
            else:
                print("1 ve ya 2 rakami giriniz\n")
            
            
    def paraYatirma(self):

        yatirilanPara = abs(int(input('Yatırmak istediğiniz tutarı giriniz: ')))
        
        print('Paranız yatırılmıştır.')
    
        self.kart.bakiye += yatirilanPara

        print("Şimdiki Bakiyeniz {} $'dir \n".format(self.kart.bakiye))
        
        self.menuDonme()
        

    def paraCekme(self):

        cekilenPara = int(input('Çekmek istediğiniz tutarı giriniz: '))
        
        if cekilenPara > self.kart.bakiye:
            print('\nKartta yeterli bakiye bulunmamaktadır.\n')
            self.menuDonme()
            
        else:
            self.kart.bakiye -= cekilenPara
            print('\nParanız başarıyla çekilmiştir. Mevcut bakiyeniz: {}\n'.format(self.kart.bakiye))
            self.menuDonme()


    def bakiye(self):
        print("\n \n Hesap Bakiyeniz {} $'dır. Borcunuz ise {}'dır.".format(self.kart.bakiye, self.kart.borc))  
        self.menuDonme() 
             

    def cikis(self):
        print("\n  Çiftlik Bank ATM'yi kullandığınız için teşekkür eder, iyi günler dileriz.")
        exit()
        

    def menuDonme(self):

        while True:
            secim = int(input(f" \n Menüye dönmek istermisiniz? 1(Evet) ve ya 0 (Hayır) olarak cevaplayınız:  "))
            if secim == 1:
                print()
                self.anaFonksiyon()
            elif secim == 0:
                print("Banka ATM'yi kullandığınız için teşekkür ederiz. Tekrar bekleriz.")
                exit()
            else:
                print('1-0 arasında değer giriniz.')
                continue


    def kartNumaraDenetleme(self):

        girilenKartAd = input('Kartın adını giriniz: ')
        
        if girilenKartAd == "hasanKart":
            return hasanKart

        elif girilenKartAd == "yusufKart":
            return yusufKart

        elif girilenKartAd == "selimKart":
            return selimKart

        else:
            print('Girdiğiniz isimde kart bulunamamıştır.')
            exit()


selimKart = Kart('Mustafa Selim','Bal',1234567890123456,'1234',10,20,30000)

hasanKart = Kart("Hasan","Dadaszade",4169789766543245,"1234",20,10,30000) 

yusufKart = Kart("Yusif","Mirzəbəyli",8233080120091405,"1234",10,20,30000)

hesaplar = ["hasanKart","selimKart","yusufKart"]

calistir = ATM()

{% endhighlight %}

## Object-Oriented Approach

During the project, we decided to harness the object-oriented programming (OOP) capabilities of Python. This allowed us to write more modular and reusable code. By utilizing concepts like classes and objects, we were able to structure our ATM application in a more organized manner.

## Error Handling and Validation Controls

Throughout the development process, we emphasized error handling and validation controls to enhance the user experience. For example, we implemented error messages for incorrect PIN entries. Similarly, when a user attempted to perform a balance inquiry with insufficient funds, we displayed informative messages to guide them.

## Testing and Iteration

Finally, we completed the project and conducted thorough testing. We interacted with the ATM application using different accounts and achieved the expected results. Through this process, we gained a deeper understanding of the flexibility and power of the Python language. We iterated multiple times, going back to debug and improve our code, further refining our skills.

## Collaboration and Teamwork

Collaboration played a crucial role in successfully executing this project. With the support of my friends and the inspiration we provided each other, completing the project became an enjoyable journey. By assisting one another, we also honed our teamwork skills.

## Conclusion

In conclusion, using the Python programming language and embracing the principles of OOP, we developed an amateur ATM application. This project allowed us to explore the capabilities of Python, and through teamwork and shared enthusiasm, we accomplished our goal.

We look forward to further expanding our programming knowledge and exploring new projects in the future. Stay tuned for more exciting updates on our programming adventures!

Thank you for reading, and feel free to share your thoughts and questions in the comments below.

Keep coding and exploring!
