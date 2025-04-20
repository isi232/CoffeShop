from tkinter import *
from math import *
username = 'isi'
password = '1234'
class App():
    def __init__(self):
        self.root = Tk()
        self.root.title('MyCoffee')
        self.root.geometry('400x300')
        self.root.resizable(width='false',height='false')
        self.label = Label(self.root,text='Enter username:',font = ('Arial',14),)
        self.label.pack(pady = 5)
        
        self.entry_username = Entry(self.root,font =('Arial',14))
        self.entry_username.pack(pady=5)
        
        self.label = Label(self.root,text='Enter password:',font = ('Arial',14),)
        self.label.pack(pady =5)
        
        self.entry_password = Entry(self.root,font =('Arial',14),show='*')
        self.entry_password.pack(pady=5)
        
        self.login_button = Button(self.root,text ='Log in',font =('Arial',14),command=self.login)
        self.login_button.pack(pady=25)
        
        self.result_label = Label(self.root,text='',font =('Arial',14),fg = 'red')
        self.result_label.pack(pady=5)
    
    def login(self):
        if self.entry_username.get() == username and self.entry_password.get() == password:
            self.new_window()
        else:
            self.result_label.config(text='Şifrə yalnışdır!')
    def new_window(self):
        new_win = Toplevel(self.root)
        new_win.geometry('800x600')
        new_win.resizable(width='false',height='false')
        new_win.title('MyCoffee')
        self.entries = {}
        
        coffee_list = {'Espresso': '1.20 AZN', 
                       'Cappuccino': '1.50 AZN', 
                       'Latte': '2 AZN', 
                       'Americano': '2.20 AZN', 
                       'Mocha': '2.80 AZN', 
                       'Macchiato': '3.20 AZN'}

        for i,(coffee,price) in enumerate(coffee_list.items()):
            coffee_label = Label(new_win, text=f"{coffee} - {price}", font=('Arial', 14))
            coffee_label.pack(pady=2)   
            coffee_label.place(x=50,y=50+i*30)
           
            coffee_entry = Entry(new_win,font=('Arial', 14),width=5)
            coffee_entry.pack(pady=2)
            coffee_entry.place(x=280,y=50+i*30)
            
            price_float = float(price.split()[0])
            self.entries[coffee] = (coffee_entry, price_float)
            
            coffee_label = Label(new_win,text='---Enter a number',font=('Arial', 14))
            coffee_label.pack(pady=2)
            coffee_label.place(x=380,y=50+i*30)
        
        self.total_label = Label(new_win, text="Ümumi məbləğ: 0 AZN", font=('Arial', 16), fg='green')
        self.total_label.place(x=50, y=320)
        
        coffee_button = Button(new_win,text='Complate',font=('Arial', 14),command=self.button_click)
        coffee_button.pack()
        coffee_button.place(x=400,y=300)
        
    def button_click(self):
        total = 0
        for coffee, (coffee_entry, price) in self.entries.items():
            try:
                count = int(coffee_entry.get())
                total += count * price
            except:
                continue
        self.total_label.config(text=f"Ümumi məbləğ: {total:.2f} AZN")


        

            
      
app = App()
app.root.mainloop()
